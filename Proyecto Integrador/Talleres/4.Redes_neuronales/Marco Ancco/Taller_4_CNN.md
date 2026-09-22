# Taller 4 — Redes Neuronales Convolucionales (CNN)

## 1. Introducción

En este taller se desarrollaron modelos de aprendizaje profundo para clasificar imágenes de residuos en dos categorías: vidrio (*glass*) y plástico (*plastic*). El trabajo abarca la preparación de datos, la construcción de una CNN, el entrenamiento, la evaluación y la comparación con un modelo preentrenado.

Este informe se basa en la sección de CNN del notebook `Redes_neuronales_ss.ipynb`. Las métricas corresponden a las salidas guardadas en el archivo; no se realizó un nuevo entrenamiento. Las secciones posteriores de clasificación de reseñas con Keras y perceptrones corresponden a otros ejercicios.

## 2. Objetivos

- Comprender cómo las capas convolucionales extraen características de las imágenes.
- Preparar conjuntos de entrenamiento, validación y prueba.
- Entrenar una CNN desde cero mediante el ajuste de sus pesos.
- Comparar el entrenamiento básico, el aumento de datos y la transferencia de aprendizaje.
- Evaluar los modelos con accuracy, ROC-AUC, precisión, recall, F1 y matrices de confusión.
- Explorar la interpretación de predicciones mediante Grad-CAM.

## 3. Entorno de trabajo

Se utilizó Google Colab con Python, PyTorch y torchvision. También se emplearon NumPy, Matplotlib, scikit-learn, tqdm y Pillow. La ejecución guardada detectó una GPU compatible con CUDA.

El notebook importa la clase `TrashDataset` desde el módulo externo `trash_dataset.py`. Este archivo debe estar disponible para reproducir el ejercicio; su implementación no está incluida en el notebook proporcionado.

## 4. Dataset y preparación de las imágenes

Se trabajó con las categorías de vidrio y plástico de TrashNet. Aunque el archivo descargado contiene más categorías, este ejercicio utiliza únicamente dos:

| Etiqueta | Categoría | Material |
|---|---|---|
| 0 | `glass` | Vidrio |
| 1 | `plastic` | Plástico |

La carpeta de datos configurada en Colab es `/content/dataset-resized`. Dentro de ella se utilizan las subcarpetas `glass/` y `plastic/`.

### 4.1. División de datos

Las particiones se solicitan mediante el argumento `split` de `TrashDataset`.

| Conjunto | Imágenes | Porcentaje aproximado | Función |
|---|---:|---:|---|
| Entrenamiento | 687 | 69,89 % | Ajustar los pesos |
| Validación | 147 | 14,95 % | Observar el desempeño durante el entrenamiento |
| Prueba | 149 | 15,16 % | Evaluar el modelo al finalizar |
| **Total** | **983** | **100 %** | |

Las cantidades son las registradas en el notebook. Sin el módulo externo no se puede confirmar el algoritmo de separación, su semilla ni los porcentajes configurados internamente.

### 4.2. Transformación y carga

Para la CNN básica se aplica `T.ToTensor()`. Los lotes observados tienen forma `[128, 1, 384, 512]`: hasta 128 imágenes, un canal y resolución de 384 × 512 píxeles. Esto confirma que el modelo recibe imágenes en escala de grises; la conversión interna realizada por `TrashDataset` no es visible en el archivo.

```python
transform_basic = T.Compose([
    T.ToTensor()
])

train_dataset = DataClass(
    root=DATA_DIR,
    split="train",
    transform=transform_basic)

val_dataset = DataClass(
    root=DATA_DIR,
    split="val",
    transform=transform_basic)

test_dataset = DataClass(
    root=DATA_DIR,
    split="test",
    transform=transform_basic)

len(train_dataset), len(val_dataset), len(test_dataset)
```

El cargador de entrenamiento mezcla los ejemplos con `shuffle=True`; los de validación y prueba mantienen su orden. El tamaño de lote utilizado es 128.

![Ejemplos de vidrio y plástico extraídos del notebook](Taller_4_CNN_assets/dataset_ejemplos.png)

## 5. Fundamentos y arquitectura de la CNN

Una red neuronal combina entradas mediante pesos y funciones de activación para producir una salida. Durante el entrenamiento, esos pesos se modifican para reducir una función de pérdida.

En una CNN, los filtros convolucionales recorren regiones de la imagen y aprenden patrones útiles para la clasificación. ReLU introduce no linealidad y MaxPool reduce la resolución espacial de las representaciones.

| Etapa | Configuración | Salida por imagen |
|---|---|---|
| Entrada | Imagen en escala de grises | 1 × 384 × 512 |
| Bloque 1 | Conv2d 1 → 16, ReLU, MaxPool2d(2) | 16 × 192 × 256 |
| Bloque 2 | Conv2d 16 → 32, ReLU, MaxPool2d(2) | 32 × 96 × 128 |
| Bloque 3 | Conv2d 32 → 64, ReLU | 64 × 96 × 128 |
| Promedio adaptativo | AdaptiveAvgPool2d((1, 1)) | 64 × 1 × 1 |
| Clasificador | Flatten y Linear(64, 2) | 2 puntuaciones |

Las convoluciones utilizan kernels de 3 × 3 y padding de 1. La salida del clasificador son dos *logits*, no probabilidades. La evaluación aplica softmax para obtener la probabilidad de la clase plástico.

```python
import torch.nn as nn
import torch.nn.functional as F

num_classes = len(DataClass.classes)

class SimpleCNN(nn.Module):
    def __init__(self, num_classes):
        super().__init__()
        self.features = nn.Sequential(
            nn.Conv2d(1, 16, kernel_size=3, padding=1),
            nn.ReLU(),
            nn.MaxPool2d(2),

            nn.Conv2d(16, 32, kernel_size=3, padding=1),
            nn.ReLU(),
            nn.MaxPool2d(2),

            nn.Conv2d(32, 64, kernel_size=3, padding=1),
            nn.ReLU(),
            nn.AdaptiveAvgPool2d((1, 1))
        )
        self.classifier = nn.Sequential(
            nn.Flatten(),
            nn.Linear(64, num_classes)
        )

    def forward(self, x):
        x = self.features(x)
        x = self.classifier(x)
        return x

model_scratch = SimpleCNN(num_classes=num_classes).to(device)
model_scratch
```

## 6. Entrenamiento y ajuste de pesos

El aprendizaje se realiza mediante estos pasos:

1. El modelo recibe un lote de imágenes y genera sus logits.
2. `CrossEntropyLoss` compara esas salidas con las etiquetas reales.
3. `loss.backward()` calcula los gradientes del error respecto de los parámetros.
4. Adam actualiza los parámetros mediante `optimizer.step()`.
5. El proceso se repite con los lotes y las épocas siguientes.

Fragmento del ciclo de entrenamiento del notebook:

```python
def train_one_epoch(model, loader, optimizer, criterion):
    model.train()
    losses = []
    for x, y in loader:
        x = x.to(device)
        y = y.to(device).long()

        optimizer.zero_grad()
        logits = model(x)
        loss = criterion(logits, y)
        loss.backward()
        optimizer.step()

        losses.append(loss.item())
    return float(np.mean(losses))
```

La CNN básica se entrenó durante **8 épocas**, con Adam y una tasa de aprendizaje de **0,001**. La pérdida de entrenamiento disminuyó de **0,6943** a **0,6718**. La accuracy de validación terminó en **63,27 %**, mientras que el ROC-AUC de validación terminó en **0,6748**.

![Pérdida de entrenamiento de la CNN básica](Taller_4_CNN_assets/perdida_entrenamiento.png)

![Accuracy y ROC-AUC de validación de la CNN básica](Taller_4_CNN_assets/metricas_validacion.png)

La accuracy de validación permanece en 0,5102 durante las primeras cinco épocas y mejora desde la sexta. El descenso de la pérdida indica aprendizaje, pero las métricas muestran un desempeño limitado. Estas curvas, por sí solas, no permiten confirmar sobreajuste: no se registra una curva de pérdida de validación para este experimento.

## 7. Evaluación de la CNN básica

La evaluación utiliza `model.eval()` y desactiva el cálculo de gradientes. Una probabilidad de plástico mayor o igual que 0,5 se clasifica como plástico; en caso contrario, como vidrio.

```python
test_acc, test_auc, y_true, y_pred, y_prob = evaluate(model_scratch, test_loader)
print(f"Test accuracy: {test_acc:.4f}")
print(f"Test ROC-AUC:  {test_auc:.4f}")
print()
print(classification_report(y_true, y_pred, digits=4))
cm = confusion_matrix(y_true, y_pred)
cm
```

Las métricas utilizadas se interpretan así:

- **Accuracy:** proporción total de predicciones correctas.
- **ROC-AUC:** capacidad de ordenar las imágenes de plástico por encima de las de vidrio según su puntuación, considerando diferentes umbrales.
- **Precisión:** proporción de predicciones de una clase que son correctas.
- **Recall:** proporción de ejemplos reales de una clase identificados correctamente.
- **F1:** media armónica de precisión y recall.

En las **149 imágenes de prueba**, la CNN básica obtuvo **55,03 % de accuracy** y **0,6191 de ROC-AUC**.

| Clase | Precisión | Recall | F1 | Imágenes |
|---|---:|---:|---:|---:|
| Vidrio | 0,5672 | 0,5000 | 0,5315 | 76 |
| Plástico | 0,5366 | 0,6027 | 0,5677 | 73 |

### Matriz de confusión

Las filas representan la clase real y las columnas la predicción.

| Clase real | Predicción: vidrio | Predicción: plástico |
|---|---:|---:|
| Vidrio | 38 | 38 |
| Plástico | 29 | 44 |

El modelo clasificó correctamente **82 imágenes** y se equivocó en **67**.

![Matriz de confusión de la CNN básica](Taller_4_CNN_assets/matriz_confusion.png)

## 8. Aumento de datos

El segundo experimento conserva la arquitectura `SimpleCNN` y aplica transformaciones aleatorias al conjunto de entrenamiento: rotaciones de hasta 10 grados y traslaciones de hasta el 5 % en cada eje.

```python
transform_aug = T.Compose([
    T.RandomRotation(degrees=10),
    T.RandomAffine(degrees=0, translate=(0.05, 0.05)),
    T.ToTensor()
])
```

Estas transformaciones generan variaciones de los ejemplos durante su carga, con el propósito de mejorar la generalización. La validación y la prueba conservan las transformaciones básicas.

Esta CNN se entrenó durante **6 épocas**. Su pérdida final de entrenamiento fue **0,6856**, y su accuracy final de validación fue **65,31 %**. En prueba alcanzó **56,38 % de accuracy** y **0,6411 de ROC-AUC**.

La mejora observada frente a la CNN básica es pequeña: aproximadamente **1,35 puntos porcentuales** de accuracy. Como los experimentos tienen distinta duración y no se documentan varias repeticiones, esta diferencia no permite aislar el efecto del aumento de datos.

## 9. Transferencia de aprendizaje y ajuste fino

El tercer experimento utiliza **ResNet18 con pesos preentrenados**. Las imágenes se redimensionan a **224 × 224 píxeles** y se repite el canal de gris tres veces para adaptar la entrada al modelo. Esta repetición proporciona tres canales, pero no recupera el color original.

Los lotes son de 64 imágenes. En entrenamiento se mantienen las rotaciones y traslaciones; en validación y prueba solo se redimensiona, convierte a tensor y repite el canal.

### 9.1. Entrenamiento del clasificador

Se sustituye la capa final por una capa lineal con dos salidas. Se congelan los parámetros del modelo y se habilita el entrenamiento de los de `fc`.

```python
resnet = models.resnet18(weights=models.ResNet18_Weights.DEFAULT)
in_features = resnet.fc.in_features
resnet.fc = nn.Linear(in_features, num_classes)
resnet = resnet.to(device)

for name, param in resnet.named_parameters():
    param.requires_grad = False

for param in resnet.fc.parameters():
    param.requires_grad = True

resnet
```

Esta etapa dura **4 épocas**, con Adam y tasa de aprendizaje de **0,001**. El ROC-AUC de validación pasa de **0,7152** a **0,8207**. La accuracy fluctúa y termina en **57,82 %**: una mejora de AUC no implica necesariamente una mejora de accuracy con el umbral fijo utilizado.

### 9.2. Ajuste fino

Se habilitan los parámetros de `layer4` y `fc`, y se entrena durante otras **4 épocas** con tasa de aprendizaje de **0,0001**.

Al finalizar, la pérdida de entrenamiento es **0,0890**, la accuracy de validación es **88,44 %** y el ROC-AUC de validación es **0,9676**.

### 9.3. Resultados de prueba

ResNet18 con ajuste fino alcanza **86,58 % de accuracy** y **0,9562 de ROC-AUC**.

| Clase | Precisión | Recall | F1 | Imágenes |
|---|---:|---:|---:|---:|
| Vidrio | 0,8182 | 0,9474 | 0,8780 | 76 |
| Plástico | 0,9344 | 0,7808 | 0,8507 | 73 |

| Clase real | Predicción: vidrio | Predicción: plástico |
|---|---:|---:|
| Vidrio | 72 | 4 |
| Plástico | 16 | 57 |

Se clasifican correctamente **129 imágenes** y se cometen **20 errores**. El modelo identifica una mayor proporción de los vidrios que de los plásticos; el error más frecuente es clasificar plástico como vidrio.

## 10. Comparación de resultados

| Modelo | Épocas | Pérdida final de entrenamiento | Accuracy en prueba | ROC-AUC en prueba |
|---|---:|---:|---:|---:|
| CNN desde cero | 8 | 0,6718 | 55,03 % | 0,6191 |
| CNN con aumento de datos | 6 | 0,6856 | 56,38 % | 0,6411 |
| ResNet18 con ajuste fino | 4 + 4 | 0,0890 | **86,58 %** | **0,9562** |

ResNet18 presenta el mejor desempeño en esta ejecución y supera a la CNN básica en aproximadamente **31,55 puntos porcentuales** de accuracy. La comparación corresponde a configuraciones que también difieren en arquitectura, resolución, tamaño de lote y entrenamiento; no mide únicamente el efecto de los pesos preentrenados.

La pérdida indicada pertenece al entrenamiento. El notebook no reporta la pérdida final de prueba de estos modelos.

## 11. Interpretabilidad mediante Grad-CAM

El notebook implementa una versión simplificada de Grad-CAM sobre `layer4` de ResNet18. Combina activaciones y gradientes para obtener un mapa de las regiones que contribuyen a la puntuación de una clase.

Los colores más intensos permiten explorar qué regiones influyen en la salida. El mapa es una herramienta de interpretación; no demuestra por sí solo que la red reconozca correctamente el material.

El notebook guarda una visualización de Grad-CAM. Su superposición requiere redimensionar el mapa al tamaño de la imagen o ajustar la extensión de ambos gráficos para garantizar su alineación espacial.

## 12. Guardado y reproducción

El notebook guarda los diccionarios de parámetros de los modelos en:

- `models/cnn_scratch.pth`
- `models/cnn_aug.pth`
- `models/resnet_transfer.pth`

Para volver a utilizarlos es necesario reconstruir la arquitectura correspondiente y cargar su `state_dict`. El archivo proporcionado contiene el código de guardado, pero no una demostración de recarga ni los archivos de pesos adjuntos.

Para reproducir el experimento deben prepararse las dependencias, los datos y el módulo `trash_dataset.py` antes de crear los datasets. También conviene documentar la semilla y el procedimiento de partición. En la sección de ResNet18 no aparece una normalización explícita de entrada; además, congelar parámetros no impide que las estadísticas internas de BatchNorm se actualicen cuando se llama a `model.train()`.

## 13. Conclusiones

El taller permitió recorrer el proceso de clasificación de imágenes: carga y transformación de datos, construcción de una CNN, cálculo del error, actualización de pesos y evaluación con ejemplos de prueba.

La CNN desde cero obtuvo un rendimiento limitado y el aumento de datos produjo una mejora pequeña en la ejecución registrada. El mejor resultado se obtuvo con ResNet18 y ajuste fino: **86,58 % de accuracy y 0,9562 de ROC-AUC**.

La matriz de confusión permitió identificar los errores por material, mientras que Grad-CAM introdujo una aproximación a la interpretación visual. Los resultados respaldan la utilidad de la transferencia de aprendizaje en este ejercicio, aunque sería necesario repetir los experimentos con particiones y semillas controladas para evaluar su estabilidad.

---

**Fuente:** sección CNN, celdas 1–59 según el índice del archivo `Redes_neuronales_ss.ipynb` (contado desde cero). Las figuras se extrajeron de sus salidas guardadas. Los fragmentos de código son extractos del notebook y dependen del entorno y las definiciones de ese archivo.
