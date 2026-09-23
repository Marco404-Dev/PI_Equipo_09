# **REDES NEURONALES**

Las redes neuronales son un modelo de inteligencia artificial (IA) que reconoce patrones y resuelve problemas comunes a partir de datos. Por lo que deben ser entrenados para aprender las características presentes en los datos, permitiendo clasificarlos datos y realizar predicciones \[1\].

### **CNN (Redes neuronales convolucionales)**  
Es un tipo de red especializada en procesar datos estructurados en cuadrículas, como imágenes. Pueden tener decenas o cientos de capas, y cada una aprende a detectar diferentes características de una imagen \[2\].

<img width="990" height="356" alt="image" src="https://github.com/user-attachments/assets/46ee1327-fd9b-43b4-986c-f684d4c662c3" />

- **Interpretación:**  
  Se puede observar tres imágenes:  
1. Imagen (label=0): Se muestra la entrada original (botella de vidrio en escalas de grises).  
2. Grad-CAM (pred=0): Nos indica que el modelo clasifica correctamente la imagen en la categoría 0\. Las cuadriculas de color amarillo y verde claro son regiones con mayor activación e influencia en la predicción, mientras que las azul oscuro y morado presentan una menor contribución.  
3. Superposición: Al combinar ambas imágenes, se aprecia que el modelo se centró en el cuerpo central de la botella y la etiqueta para tomar su decisión, ignorando el fondo irrelevante.

### **KERAS**  
Keras es una biblioteca de alto nivel desarrollada en Python para la creación y el entrenamiento de modelos de aprendizaje profundo. Su importancia radica en que proporciona una interfaz sencilla para trabajar con TensorFlow, facilitando el desarrollo, la experimentación y la implementación de redes neuronales profundas de manera eficiente \[3\].

<img width="835" height="813" alt="image" src="https://github.com/user-attachments/assets/84c60325-437d-4f67-a743-27d6d391c596" />

- **Interpretación:**  
  En la gráfica se compara la pérdida de validación a lo largo de 20 épocas entre el modelo original (naranja) y el modelo con dropout (azul). Durante el entrenamiento, el dropout desactiva aleatoriamente el 50% de las neuronas, lo que obliga a la red a no depender de conexiones específicas y a aprender con diferentes combinaciones, reduciendo el sobreajuste (overfitting).   A pesar que el modelo original reduce su error más rápido al inicio, ambos comienzan a sobreajustarse a partir de la época 10\.

### **PERCEPTRÓN**  
Es una unidad neuronal de procesamiento en el aprendizaje profundo (Deep Learning) \[4\]. Es una representación matemática de una neurona biológica que recibe múltiples entradas, les aplica un peso (weight), suma un sesgo (bias) y pasa el resultado por una función de activación para producir una salida \[4\].

<img width="503" height="505" alt="image" src="https://github.com/user-attachments/assets/51682fec-1dc1-4b54-a563-8360b4168f61" />

- **Interpretación:**  
  Los círculos blancos representan los casos donde XOR \= 0 en (0,0) y (1,1), mientras que los círculos azules representan XOR \= 1 en (0,1) y (1,0) y cada línea azul continua representa la frontera de decisión de una neurona (perceptrón).  
- 1 perceptrón: Imposible de resolver porque solo puede trazar una línea recta y los datos no son linealmente separables.  
- 2 perceptrones \+ capa de salida: Se puede resolver, ya que los dos perceptrones de la capa oculta crean las dos fronteras de decisión paralelas que delimitan el área de las entradas positivas, y la neurona de salida combina estas decisiones para clasificar correctamente los datos.

## **Referencias:**

**\[1\]** MathWorks, “Introducción a las redes neuronales,” *MATLAB & Simulink*. \[En línea\]. Disponible en: [https://la.mathworks.com/discovery/neural-network.html](https://la.mathworks.com/discovery/neural-network.html?utm_source=chatgpt.com). \[Accedido: 22-sep-2026\].

**\[2\]** MathWorks, “¿Qué son las redes neuronales convolucionales?,” *MATLAB & Simulink*. \[En línea\]. Disponible en: [https://la.mathworks.com/discovery/convolutional-neural-network.html](https://la.mathworks.com/discovery/convolutional-neural-network.html). \[Accedido: 22-sep-2026\].

**\[3\]** Ultralytics, “¿Qué es Keras? Guía de la API de aprendizaje profundo,” *Ultralytics*. \[En línea\]. Disponible en: [https://www.ultralytics.com/es/glossary/keras](https://www.ultralytics.com/es/glossary/keras?utm_source=chatgpt.com) 

**\[4\]** J. Suze, “Perceptrón: ¿qué es y para qué sirve?,” *Liora*, 7 de marzo de 2022\. \[En línea\]. Disponible en: [https://liora.io/es/perceptron-que-es-y-para-que-sirve](https://liora.io/es/perceptron-que-es-y-para-que-sirve). \[Accedido: 22-sep-2026\].  

