# Informe interpretativo: Redes Neuronales 

## 1. CNN:
Las CNN son un tipo de red especializada en el procesamiento de datos con estructura espacial, como las imágenes. En lugar de conectar cada píxel de forma compacta, utilizan filtros pequeños llamados kernels que recorren la matriz de la imagen para extraer patrones jerárquicos (desde bordes y texturas simples en las capas iniciales hasta formas complejas en las profundas). 

### 1.1. Conceptos clave:
- Convolución (Conv2D): Aplica filtros para obtener mapas de características, detectando bordes, texturas y estructuras.
- Activación (ReLU): Introduce no linealidad ReLU(x) = max(0, x), anulando valores negativos y dejando intactos los positivos.
- Pooling (MaxPool): Reduce la resolución espacial conservando la información crítica, lo que disminuye el costo computacional y mejora la generalización.
- Capas Fully-Connected (Densas): Integran los mapas de características obtenidos para realizar la clasificación o regresión final.
  
### 1.2. Interpretación de la Imagen (Grad-CAM) :

<div align="center">
  <img width="840" height="298" alt="image" src="https://github.com/user-attachments/assets/ca0d0383-a7bd-4a4b-bac1-96711705f3f6" />
</div>


La visualización confirma que el modelo está tomando decisiones correctas basadas en la región relevante de la imagen:
- Imagen Original (label=0): Muestra el objeto de entrada (en este caso, una botella).
- Mapa Grad-CAM (pred=0): Resalta en colores cálidos (amarillo/verde claro) las zonas de la imagen donde el modelo concentró su atención para predecir la clase 0. Se observa que el enfoque principal recae en el cuerpo central de la botella.
- Superposición: Combina el mapa de calor sobre la imagen original, demostrando que la red neuronal aprendió a "mirar" la estructura del objeto y no se distrajo con el fondo, validando la eficacia del modelo

## 2. KERAS:
Keras es una API de redes neuronales de alto nivel, escrita en Python, capaz de ejecutarse sobre frameworks de bajo nivel como TensorFlow. Su diseño prioriza la simplicidad, la modularidad y la facilidad de uso, permitiendo construir y entrenar modelos complejos con pocas líneas de código.
No se programa desde cero
Construye y entrena redes neuronales de manera más sencilla 

### 2.1. Evaluación del Rendimiento:

Para supervisar el proceso de aprendizaje de un modelo en Keras, se extraen las métricas almacenadas en el historial de entrenamiento (modelb.history). El siguiente bloque de código procesa los valores de pérdida (loss) tanto para el entrenamiento como para la validación y genera una gráfica comparativa a lo largo de las épocas:

<div align="center">
  <img width="423" height="231" alt="image" src="https://github.com/user-attachments/assets/e35b09b7-7e57-491b-80ed-6f88631f8d48" />
</div>

### 2.2. Interpretación 
<div align="center">
  <img width="638" height="627" alt="image" src="https://github.com/user-attachments/assets/2f2a6019-e874-471a-9f14-6b19d12c2067" />
</div>

La visualización obtenida a partir del código anterior permite realizar el siguiente diagnóstico del modelo:

- Pérdida de entrenamiento (training): La línea azul continua desciende de manera constante y se aproxima a cero, lo que demuestra que el modelo está aprendiendo y ajustándose de forma exitosa a los datos con los que fue entrenado.
- Pérdida de validación (val): La línea naranja discontinua disminuye en las primeras épocas hasta alcanzar su punto óptimo alrededor de la época 5; sin embargo, a partir de ese momento comienza a incrementarse y a fluctuar hacia arriba.
- Diagnóstico de Sobreajuste (Overfitting): La divergencia entre ambas curvas evidencia un claro problema de sobreajuste. El modelo ha memorizado los datos de entrenamiento pero ha perdido su capacidad de generalizar correctamente ante datos nuevos de validación, lo que indica la necesidad de aplicar técnicas de regularización o parada temprana (Early Stopping).

## 3. PERCEPTRÓN
El perceptrón es la unidad básica de red neuronal capaz de resolver problemas de clasificación binaria siempre y cuando los datos sean linealmente separables. Las compuertas lógicas AND y OR pueden resolverse trazando una línea recta que aisle los resultados verdaderos de los falsos en un plano cartesiano. Por el contrario, la compuerta XOR carece de separabilidad lineal en una sola capa, evidenciando la necesidad de redes multicapa. 

### 3.1. Interpretación:
<div align="center">
  <img width="497" height="497" alt="image" src="https://github.com/user-attachments/assets/f4bcaee2-32d7-46f4-b9ee-ffdb5985086d" />
</div>

La representación visual obtenida permite comprobar de forma geométrica el funcionamiento del perceptrón como clasificador lineal:

- Puntos azules ((0,0), (0,1), (1,0), (1,1)): Ubican las combinaciones de entrada posibles en el espacio bidimensional de las compuertas lógicas.
- Línea de la compuerta AND (verde): Separa correctamente el punto superior derecho (1,1) del resto de los puntos ((0,0), (0,1) y (1,0)), cumpliendo la regla de que solo se activa si ambas entradas son verdaderas.
- Línea de la compuerta OR (roja): Aísla el punto inferior izquierdo (0,0) frente a los demás casos, demostrando que el perceptrón logra dividir satisfactoriamente los estados donde al menos una entrada es activa.

## Referencias:

- [1] MathWorks, “Introducción a las redes neuronales,” *MATLAB & Simulink*. . Disponible en:(https://la.mathworks.com/discovery/neural-network.html?utm_source=chatgpt.com). 

- [2] MathWorks, “¿Qué son las redes neuronales convolucionales?,” *MATLAB & Simulink*. Disponible en: (https://la.mathworks.com/discovery/convolutional-neural-network.html).



