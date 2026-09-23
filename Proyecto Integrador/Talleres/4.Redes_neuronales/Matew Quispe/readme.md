# Informe de resultados y comentarios - Redes Neuronales

## 1. Introducción

En este Colab aprendí cómo funcionan diferentes tipos de redes neuronales y cómo pueden utilizarse para resolver problemas de clasificación. Se trabajó desde modelos más complejos como las redes convolucionales para imágenes hasta un modelo más sencillo como el perceptrón.

Lo que más me llamó la atención fue observar que, aunque existen modelos avanzados, todos parten de una idea básica: una neurona recibe informacion, realiza operaciones matemáticas y genera una respuesta




# 2. Redes neuronales convolucionales 

En esta parte aprendí cómo funcionan las redes neuronales convolucionales, son utilizadas mas que nada para trabajar con img

La CNN utiliza capas como **Conv2D, ReLU y Pooling** para poder encontrar características importantes dentro de una imagen. 

Me pareció interesante que la red pueda aprender estas características por sí misma, ya que nosotros no le indicamos exactamente qué debe buscar, sino que mediante el entrenamiento ajusta sus pesos para encontrar patrones importantes

<img width="1081" height="518" alt="image" src="https://github.com/user-attachments/assets/fca63ed2-276a-4fb8-ae30-37b5419be122" />


---

# 3. Dataset TrashNet y clasificación de residuos

Para probar la CNN se utilizó el dataset TrashNet, donde se trabajo con imágenes clasificadas en diferentes tipos de residuos.

En este caso, la red tenía que aprender a diferenciar entre imágenes de vidrio y plástico. Debido a que cada material tiene características visuales diferentes, el modelo intenta encontrar patrones que permitan separar correctamente ambas clases.

Mediante estos patrones pude entender como funciona una computadora, pues transforma en datos numéricos para poder analizarlos

<img width="980" height="792" alt="image" src="https://github.com/user-attachments/assets/60c2771d-4b48-4149-95ef-375911ef3602" />


---

# 4. Resultados de la CNN entrenada desde cero

Luego del entrenamiento de la CNN se observó que el modelo logró aprender algunas características de las imagenes.

El resultado obtenido fue aproximadamente un **63.27% de accuracy**, lo cual indica que el modelo logró reconocer ciertos patrones, aunque todavía presentaba errores en algunas predicciones.

Este resultado me permitió entender que entrenar una red neuronal no significa obtener resultados perfectos automáticamente, ya que depende de factores como la cantidad de datos, la arquitectura utilizada y el proceso de entrenamiento.

<img width="742" height="207" alt="image" src="https://github.com/user-attachments/assets/b405b58e-73f1-4c65-be15-f037222217c5" />
<img width="1077" height="697" alt="image" src="https://github.com/user-attachments/assets/cc10fd81-e6f7-41b3-b201-3bd92782c9f4" />


---

# 5. Data Augmentation y Transfer Learning

Aqui aprendi las dos tecnicas para mejorar el modelo

El **Data Augmentation** permite crear nuevas variaciones de las imágenes originales mediante cambios como rotaciones o modificaciones, debido a que normalmente no se cuenta con una cantidad muy grande de datos.

Por otro lado, el **Transfer Learning** me parecio una de las tecnicas mas curioso, ya que permite utilizar un modelo que anteriormente fue entrenado con muchos datos y adaptarlo a un nuevo problema.

Esto ayuda porque la red ya tiene cierto conocimiento previo, debido a que aprendio características generales que pueden servir para nuevas tareas.

<img width="1052" height="815" alt="image" src="https://github.com/user-attachments/assets/4fae3c7c-004f-45fd-9d97-32991ef601be" />


---

# 6. Interpretación con Grad-CAM

fue una de las herramientas que más ayudó a comprender el comportamiento del modelo.

Esta tecnica permite observar qué zonas de la imagen fueron más importantes para que la red tome una decisión.

Me pareció interesante porque normalmente solo observamos la predicción final, pero con grad-CAM podemos tener una idea de por qué el modelo clasific una imagen de cierta manera.

<img width="885" height="771" alt="image" src="https://github.com/user-attachments/assets/7b2fc7a2-9e49-4377-abfd-229599f2ed95" />
<img width="912" height="841" alt="image" src="https://github.com/user-attachments/assets/80e248a4-b2ac-4ef0-9dbb-8e27723cb2b6" />

Esta gráfica muestra la evolución del error (loss) durante el entrenamiento de tres modelos diferentes:

Azul: regularization - train → error del modelo con regularización usando los datos de entrenamiento.
Naranja: regularization - validation → error del modelo con regularización usando datos que nunca vio durante el entrenamiento (validación).
Verde punteado: original → modelo sin regularización.

---

# 7. Clasificación de textos con Keras

Se trabaj con una red neuronal para clasificar reseñas de películas como positivas o negativas

El modelo logró aproximadamente un **86.1% de exactitud**, mostrando que pudo aprender patrones dentro de los textos.

Tambien se observo el problema del sobreajuste, debido a que el modelo puede aprender demasiado los datos de entrenamiento y tener dificultades cuando recibe información nueva.

Para mejorar esto se aplicaron técnicas como regularización y Dropout
<img width="1005" height="822" alt="image" src="https://github.com/user-attachments/assets/d86fd65d-5976-4d33-a36c-e4aefabfc4b0" />


---

# 8. Perceptrón: la parte que más me llamó la atención

La parte que más me llamó la atención fue el perceptrón, porque permite comprender la idea básica de cómo funcionan las redes neuronales.

Aunque es un modelo sencillo, tiene elementos fundamentales como:

- Entradas.
- Pesos.
- Suma ponderada.
- Función de activación.
- Salida.

Me pareció interesante observar que una máquina puede tomar una decisión utilizando solamente operaciones matemáticas.

Por ejemplo, al ingresar valores como temperatura y vibración, el perceptrón puede determinar si existe una alerta o no. Esto demuestra que incluso un modelo simple puede representar una decisión basada en datos.

También aprendí que un perceptrón puede resolver problemas simples como las compuertas **AND y OR**, pero no puede resolver directamente el problema **XOR**, debido a que necesita una separación más compleja.

Por esta razón fueron necesarias redes con más neuronas y capas, dando origen a modelos más avanzados.

<img width="1177" height="728" alt="image" src="https://github.com/user-attachments/assets/ca38886a-2678-4974-84b5-b9abf3de84d2" />
<img width="844" height="578" alt="image" src="https://github.com/user-attachments/assets/8dabb4f6-6ab9-427c-9db1-d183e1773e94" />


---

# 9. Conclusión personal

Despues de realizar este Colab comprendí que las redes neuronales aprenden mediante ejemplos y ajustes internos

La CNN permitió entender cómo una máquina puede analizar imágenes y encontrar patrones, mientras que el perceptrón permitió comprender la base de una neurona artificial.

Lo que más aprendi fue que no solamente importa obtener una predicción, sino también analizar los resultados y comprender cómo el modelo llega a una determinada respuesta.

EN sintesis, considero que el perceptron fue la parte más importante para entender todo el tema, ya que representa la idea inicial de cómo una red neuronal aprende y toma decisiones.
