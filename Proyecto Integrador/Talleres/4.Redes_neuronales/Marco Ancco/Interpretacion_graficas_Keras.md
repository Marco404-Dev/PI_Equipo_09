# Interpretación de las gráficas 6, 8, 9 y 10 — Keras

Estas gráficas corresponden a la clasificación de reseñas de películas de IMDB como positivas o negativas mediante una red de capas densas. Son un ejercicio diferente de la CNN que clasifica vidrio y plástico. Los números 6, 8, 9 y 10 corresponden a los apartados del Colab, no al orden de las imágenes adjuntas.

Las lecturas numéricas siguientes son aproximadas y corresponden a las capturas compartidas. Algunos valores difieren de las salidas guardadas en el notebook; no deben mezclarse como si pertenecieran a una misma ejecución.

## ¿Qué gráficas conviene incluir?

| Apartado | Gráfica | Prioridad | Qué aporta |
|---|---|---|---|
| 6 | Entrenamiento frente a validación | Esencial | Permite identificar el sobreajuste |
| 8 | Modelo pequeño frente al original | Esencial | Muestra el efecto de reducir la capacidad del modelo |
| 9 | Regularización L2 | Complementaria, con corrección | Permite analizar una penalización sobre los pesos; la leyenda actual tiene un error |
| 10 | Dropout frente al original | Alta | Muestra que la técnica retrasa el deterioro, pero no elimina el sobreajuste |

Para un informe breve, incluiría 6, 8 y 10. Para explicar todos los experimentos del Colab, incluiría las cuatro después de corregir la 9.

En todas las figuras el eje horizontal representa las épocas y el vertical la pérdida. Una menor pérdida de validación indica un mejor resultado en ese criterio para los datos de validación. La pérdida no es un porcentaje de errores ni equivale a `1 - accuracy`.

## 6. Entrenamiento frente a validación

![Pérdida de entrenamiento y validación del modelo original](Taller_4_CNN_assets/keras_06_sobreajuste.png)

**Interpretación.** La pérdida de entrenamiento disminuye de aproximadamente 0,51 hasta valores cercanos a 0,01. La pérdida de validación baja inicialmente y alcanza su mínimo alrededor de la época 5, cerca de 0,28. Después aumenta hasta aproximadamente 0,56 al finalizar, mientras la pérdida de entrenamiento continúa disminuyendo.

La separación sostenida entre ambas curvas es evidencia de sobreajuste: mejorar sobre los ejemplos usados para ajustar los pesos deja de traducirse en una mejora sobre los ejemplos de validación. El mejor punto según esta curva está cerca de la época 5, no en la última época.

**Importancia.** Esta figura justifica la necesidad de controlar la duración del entrenamiento y comparar estrategias de regularización. No permite afirmar por sí sola cómo evoluciona la accuracy, porque representa pérdida.

**Código que explica la figura:**

```python
model = models.Sequential()
model.add(layers.Dense(16, activation='relu', input_shape=(10000,)))
model.add(layers.Dense(16, activation='relu'))
model.add(layers.Dense(1, activation='sigmoid'))
model.compile(optimizer='rmsprop',
              loss='binary_crossentropy',
              metrics=['accuracy'])
```

Cada reseña se representa mediante 10 000 indicadores de presencia de palabras. Esta representación es multi-hot: varias posiciones pueden valer 1. Las dos capas de 16 neuronas aprenden combinaciones de esos indicadores; ReLU aporta no linealidad. La salida sigmoid produce una puntuación entre 0 y 1 para la clase positiva. La entropía cruzada binaria penaliza las predicciones incorrectas, especialmente las realizadas con mucha confianza. RMSprop ajusta los pesos a partir de los gradientes.

En el Colab, `fit` usa 20 épocas, lotes de 512 y `validation_data=(x_val, y_val)`. La validación se mide durante el entrenamiento, pero sus ejemplos no se usan para calcular las actualizaciones de los pesos.

## 8. Modelo más pequeño frente al original

![Comparación de la pérdida de validación del modelo pequeño y el original](Taller_4_CNN_assets/keras_08_modelo_pequeno.png)

**Interpretación.** Ambas líneas representan pérdida de validación. El modelo original mejora más rápido al inicio, pero después de aproximadamente cinco épocas su pérdida aumenta marcadamente. El modelo pequeño aprende más despacio, alcanza un mínimo cercano a 0,276 alrededor de la época 10 y termina aproximadamente en 0,32.

El modelo pequeño muestra un deterioro posterior mucho menor y un intervalo más amplio de pérdidas bajas. También presenta señales de sobreajuste al final, por lo que reducir su tamaño no elimina completamente el problema.

**Importancia.** La figura demuestra que aumentar la complejidad de una red no garantiza una mejor generalización. En esta ejecución, una arquitectura más sencilla mantiene un desempeño de validación más estable.

**Código que explica el cambio:**

```python
model2 = models.Sequential()
model2.add(layers.Dense(4, activation='relu', input_shape=(10000,)))
model2.add(layers.Dense(1, activation='sigmoid'))
```

Se reemplazan las dos capas ocultas de 16 neuronas por una sola de 4. Esto reduce los parámetros entrenables de 160 305 a 40 009, contando pesos y sesgos. Se mantienen los mismos conjuntos de datos: lo que disminuye es el tamaño del modelo, no el tamaño de la muestra. Por ello, en el informe conviene usar “modelo más pequeño” en lugar de “muestra más pequeña”.

## 9. Regularización L2

![Gráfica original de regularización L2 con advertencia sobre la leyenda](Taller_4_CNN_assets/keras_09_l2_original.png)

**Advertencia sobre la figura.** La línea azul está etiquetada como entrenamiento con regularización, pero el código del notebook toma esos valores de `modelb.history['loss']`, que corresponde al modelo original. No se debe interpretar esa línea como la pérdida de entrenamiento del modelo L2.

**Interpretación válida.** La línea naranja representa la pérdida de validación del modelo con L2 y la verde la del original. La naranja alcanza un mínimo próximo a 0,33 alrededor de la época 5, luego aumenta y presenta oscilaciones. En varias épocas finales se mantiene por debajo del original, pero su mínimo observado no es inferior al mínimo del original.

Además, la pérdida del modelo L2 incluye la penalización de regularización. Por eso, comparar directamente sus valores con la pérdida sin penalización no permite atribuir toda la diferencia a la calidad de las predicciones. Conviene complementar esta figura con accuracy y una métrica de pérdida predictiva calculada de igual forma para ambos modelos.

El pico de la época 16 muestra una variación de la pérdida de validación. La curva por sí sola no permite identificar su causa exacta.

**Código relevante del modelo:**

```python
layers.Dense(16, activation='relu',
             kernel_regularizer=regularizers.l2(0.001))
```

En el notebook esta penalización se aplica a los pesos de las dos capas ocultas. Añade al objetivo un término proporcional a la suma de sus pesos al cuadrado. Su propósito es desalentar pesos grandes; no desactiva neuronas ni garantiza eliminar el sobreajuste.

**Corrección propuesta para generar la gráfica:**

```python
epocas = range(1, len(modelb3.history['loss']) + 1)
plt.figure(figsize=(8, 5))
plt.plot(epocas, modelb3.history['loss'], '.-', label='L2: entrenamiento')
plt.plot(epocas, modelb3.history['val_loss'], '.-', label='L2: validación')
plt.plot(range(1, len(modelb.history['val_loss']) + 1),
         modelb.history['val_loss'], '--', label='Original: validación')
plt.xlabel('Época')
plt.ylabel('Pérdida (L2 incluye penalización)')
plt.title('Regularización L2')
plt.legend()
plt.grid(alpha=0.2)
plt.show()
```

Este código debe ejecutarse después de entrenar los modelos correspondientes. Aquí se conserva la captura original como evidencia del problema; no se presenta como una gráfica ya corregida.

## 10. Dropout frente al original

![Comparación de la pérdida de validación con dropout y sin dropout](Taller_4_CNN_assets/keras_10_dropout.png)

**Interpretación.** Ambas curvas representan pérdida de validación. El modelo con dropout empieza con una pérdida mayor, desciende hasta aproximadamente 0,273 alrededor de la época 7 y después empeora de manera sostenida hasta aproximadamente 0,54. La curva original alcanza su mínimo antes, alrededor de la época 5, y termina cerca de 0,56.

En esta captura, dropout retrasa el mínimo y reduce la pérdida durante buena parte de las épocas posteriores, pero el sobreajuste continúa. Su ventaja al final es pequeña. No sería correcto concluir que dropout resuelve por completo el problema o que es la mejor estrategia sin una evaluación comparable de los modelos seleccionados.

**Código que explica el cambio:**

```python
model4 = models.Sequential()
model4.add(layers.Dense(16, activation='relu', input_shape=(10000,)))
model4.add(layers.Dropout(0.5))
model4.add(layers.Dense(16, activation='relu'))
model4.add(layers.Dropout(0.5))
model4.add(layers.Dense(1, activation='sigmoid'))
```

Cada capa Dropout anula aleatoriamente una fracción de sus activaciones durante el entrenamiento, con una tasa del 50 %. Esto dificulta que el modelo dependa siempre de las mismas combinaciones de activaciones. En validación y predicción, dropout se desactiva automáticamente. La técnica no elimina permanentemente neuronas ni reduce el número de parámetros del modelo.

## Mejoras propuestas para el informe y el experimento

1. **Separar los ejercicios.** Mantener los resultados de TrashNet/CNN en una sección y los de IMDB/Keras en otra, indicando dataset, entrada, arquitectura y objetivo de cada uno.
2. **Explicar cada figura con evidencia.** Indicar qué representa cada eje, dónde aparece el mínimo, qué sucede después y qué decisión permite tomar. Agregar títulos y nombres de ejes a las gráficas del Colab.
3. **Corregir la gráfica de L2.** Usar el historial del modelo regularizado para su curva de entrenamiento y aclarar que su pérdida incluye una penalización.
4. **Seleccionar la época con validación.** Aplicar parada temprana y restaurar los mejores pesos; entrenar durante más épocas no siempre mejora el modelo.
5. **Comparar modelos seleccionados, no solo la última época.** Presentar una tabla con arquitectura, parámetros, mejor época, métrica de validación y evaluación final en prueba. Comparar la pérdida predictiva bajo una misma definición.
6. **Controlar la variabilidad.** Mantener particiones iguales, registrar semillas y repetir los experimentos para comprobar si las diferencias se sostienen. Evitar combinar capturas de una ejecución con métricas de otra.
7. **Reservar prueba para la evaluación final.** Elegir arquitectura y ajustes con validación; después reportar accuracy, precisión, recall, F1 y matriz de confusión en prueba.

Ejemplo propuesto de parada temprana para un modelo recién construido y compilado:

```python
from keras.callbacks import EarlyStopping

parada_temprana = EarlyStopping(
    monitor='val_loss',
    patience=2,
    restore_best_weights=True
)

historial = model.fit(
    partial_x_train,
    partial_y_train,
    epochs=20,
    batch_size=512,
    validation_data=(x_val, y_val),
    callbacks=[parada_temprana]
)
```

`patience=2` permite dos épocas consecutivas sin mejora antes de detener el entrenamiento. `restore_best_weights=True` recupera los pesos de la mejor época observada. Para comparar desde el inicio, se debe reconstruir el modelo antes de ejecutar este fragmento; reutilizar un modelo ya entrenado continuaría su entrenamiento.

**Conclusión:** la gráfica 6 identifica el problema; la 8 muestra el beneficio observado de reducir la capacidad; la 10 muestra el alcance y los límites de dropout; y la 9 permite analizar L2 después de corregir el historial utilizado. El informe gana valor al conectar cada cambio de código con su resultado y reconocer lo que las gráficas no demuestran.
