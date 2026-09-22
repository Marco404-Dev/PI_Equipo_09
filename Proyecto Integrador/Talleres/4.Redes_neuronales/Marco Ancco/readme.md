# Taller 4 - Redes Neuronales

## 1. Descripción del proyecto

En este taller se desarrolló un modelo basado en Deep Learning utilizando Redes Neuronales Convolucionales (CNN) para realizar una clasificación de imágenes.

El objetivo principal fue comprender el funcionamiento de una red neuronal, desde la preparación del conjunto de datos hasta el entrenamiento y evaluación del modelo.

El proyecto utiliza imágenes de residuos para clasificar dos categorías:

- Glass (vidrio)
- Plastic (plástico)

El modelo aprende características visuales de las imágenes para poder identificar automáticamente la clase correspondiente de un nuevo dato.

---

## 2. Objetivos del taller

- Comprender el funcionamiento de una red neuronal artificial.
- Analizar la arquitectura de una Red Neuronal Convolucional (CNN).
- Preparar datos para un modelo de Deep Learning.
- Entrenar un modelo de clasificación de imágenes.
- Evaluar el rendimiento mediante métricas de aprendizaje automático.

---

## 3. Conceptos aprendidos

### Redes Neuronales Artificiales

Una red neuronal artificial es un modelo de aprendizaje automático compuesto por capas de neuronas artificiales.

Cada neurona recibe valores de entrada, aplica pesos y genera una salida. Durante el entrenamiento, la red ajusta sus pesos para reducir el error entre la predicción realizada y el resultado esperado.

---

### Deep Learning

Deep Learning es una rama del Machine Learning que utiliza redes neuronales con múltiples capas para aprender patrones complejos de los datos.

A diferencia de métodos tradicionales, permite que el modelo extraiga automáticamente características importantes sin necesidad de definirlas manualmente.

---

## 4. Dataset utilizado

Para el desarrollo del modelo se utilizó un conjunto de imágenes de residuos clasificado en dos categorías:

| Clase | Etiqueta |
|-------|----------|
| Glass | 0 |
| Plastic | 1 |

El dataset fue dividido en tres grupos:

- Train: 70% de los datos utilizados para entrenar el modelo.
- Validation: 15% utilizados para ajustar y verificar el aprendizaje.
- Test: 15% utilizados para evaluar el rendimiento final.

### Imagen del dataset

(Agregar captura del conjunto de imágenes)

```
Aquí colocar imagen:
dataset_ejemplo.png
```

---

## 5. Procesamiento de datos

Antes del entrenamiento, las imágenes fueron preparadas para que puedan ser procesadas por la red neuronal.

Proceso:

```
Imagen original

        ↓

Transformación de imagen

        ↓

Conversión a valores numéricos

        ↓

Entrada del modelo CNN
```

Las imágenes fueron convertidas a escala de grises para mantener compatibilidad con la arquitectura utilizada.

### Ejemplo de procesamiento

(Agregar captura de imágenes antes y después del procesamiento)

```
Aquí colocar imagen:
procesamiento_imagen.png
```

---

# 6. Arquitectura de la Red Neuronal Convolucional (CNN)

La arquitectura utilizada sigue el siguiente flujo:

```
Imagen de entrada

        ↓

Capa convolucional (Conv2D)

        ↓

Función de activación

        ↓

Pooling

        ↓

Capas totalmente conectadas

        ↓

Clasificación final
```

## Capas convolucionales

Las capas convolucionales permiten extraer características importantes de las imágenes.

Las primeras capas detectan características simples:

- Bordes.
- Líneas.
- Texturas.

Las capas más profundas permiten identificar patrones más complejos:

- Formas.
- Estructuras.
- Características propias del material.

### Arquitectura del modelo

(Agregar captura de la arquitectura de la red)

```
Aquí colocar imagen:
arquitectura_cnn.png
```

---

# 7. Proceso de entrenamiento

El aprendizaje del modelo ocurre mediante diferentes etapas.

## Forward Propagation

La imagen pasa por las capas de la red y genera una predicción.

Ejemplo:

```
Imagen

 ↓

Red neuronal

 ↓

Predicción

Vidrio: 90%
Plástico: 10%
```

---

## Función de pérdida (Loss Function)

La predicción obtenida se compara con la respuesta correcta.

La función de pérdida mide qué tan alejada está la predicción del valor real.

---

## Backpropagation

El error calculado permite actualizar los pesos de las neuronas.

Proceso:

```
Error

 ↓

Cálculo del fallo

 ↓

Actualización de pesos

 ↓

Nueva predicción
```

Este proceso se repite durante varias épocas de entrenamiento hasta mejorar el rendimiento del modelo.

---

# 8. Evaluación del modelo

Para evaluar el rendimiento de la red neuronal se utilizan diferentes métricas.

## Accuracy

Representa el porcentaje de predicciones correctas realizadas por el modelo.

## Loss

Permite observar cómo disminuye el error durante el entrenamiento.

## Matriz de confusión

Permite analizar:

- Clasificaciones correctas.
- Errores entre categorías.

### Resultados obtenidos

(Agregar gráficos de entrenamiento)

```
Aquí colocar imágenes:

accuracy_grafico.png

loss_grafico.png

matriz_confusion.png
```

---

# 9. Técnicas de mejora

## Data Augmentation

Consiste en generar nuevas variaciones de las imágenes originales para aumentar la diversidad del dataset.

Ejemplos:

- Rotaciones.
- Cambios de posición.
- Transformaciones.

Su objetivo es mejorar la capacidad de generalización del modelo.

---

## Transfer Learning

Consiste en utilizar un modelo previamente entrenado y adaptarlo a un nuevo problema.

Permite:

- Reducir tiempo de entrenamiento.
- Aprovechar características aprendidas previamente.
- Mejorar resultados cuando existen pocos datos.

### Comparación de modelos

(Agregar tabla o imagen de resultados)

```
Aquí colocar imagen:
comparacion_modelos.png
```

---

# 10. Conclusiones

Durante este taller se comprendió que una red neuronal aprende patrones mediante el entrenamiento con datos, ajustando sus pesos a partir del error obtenido.

Los principales aprendizajes fueron:

- Importancia de la preparación del dataset.
- Funcionamiento de las capas convolucionales.
- Proceso de entrenamiento mediante propagación hacia adelante y retropropagación.
- Evaluación del rendimiento mediante métricas.
- Aplicación del Deep Learning para clasificación de imágenes.

El desarrollo permitió comprender el flujo completo de un proyecto basado en Redes Neuronales Convolucionales, desde la preparación de datos hasta la predicción final.
