**TALLER DE REDES NEURONALES**

**INTRODUCCIÓN**
En este taller se analiza la ejecución de un código para distintos modelos de deep learning de redes neuronales tales como CNN, KERAS y perceptrón. 
Con el fin de evaluar los diferentes desempeños entre los modelos, se realizaron simulaciones para cada uno y con los resultados obtenidos se realizan interpretaciones.

**OBJETIVO**
Realizar simulaciones para cada modelo de Deep Learning e interpretar las salidas obtenidas de cada uno.

**METODOLOGÍA**
El código proporcionado al inicio de la clase por los docentes es ejecutado por las distintas secciones de los modelos. Las salidas como tablas o gráficos son posteriormente analizadas con el fin de obtener la interpretación de los datos mostrados. Finalmente se realiza un informe breve con respecto a lo observado.
[añadir funciones por modelo]

**RESULTADOS E INTERPRETACIÓN**

*Sección 1: CNN*
Este ejemplo tiene la finalidad de clasificar botellas por tipo de material, ya sea vidrio (0) o plástico (1) mediante el entrenamiento con imágenes proporcionadas de los objetos.

Figura 1. Ejemplos utilizados para el entrenamiento del modelo <img width="989" height="661" alt="image" src="https://github.com/user-attachments/assets/a02639c4-1eb3-4933-aaef-62b90e135532" />

Tabla 1. Datos input para entrenamiento
https://colab.research.google.com/drive/11kyOy5sTqgfCFsDJJ7kXE24vVb7NQUG8#scrollTo=GSu6WpOWxEkd&fullscreenOutput=true
"Epoch 01 | train_loss=0.6933 | val_acc=0.5986 | val_auc=0.6889
Epoch 02 | train_loss=0.6904 | val_acc=0.5102 | val_auc=0.6772
Epoch 03 | train_loss=0.6896 | val_acc=0.5102 | val_auc=0.6720
Epoch 04 | train_loss=0.6872 | val_acc=0.5102 | val_auc=0.6704
Epoch 05 | train_loss=0.6820 | val_acc=0.5986 | val_auc=0.6767
Epoch 06 | train_loss=0.6786 | val_acc=0.5782 | val_auc=0.6720
Epoch 07 | train_loss=0.6777 | val_acc=0.6259 | val_auc=0.6713
Epoch 08 | train_loss=0.6767 | val_acc=0.6259 | val_auc=0.6694"


Figura 2. Curvas de entrenamiento <img width="872" height="395" alt="image" src="https://github.com/user-attachments/assets/7ef472bc-5c9f-460f-99dc-c6ae25f2eea9" />


Tabla 2. Resultados de evaluación
Test accuracy: 0.6174
Test ROC-AUC:  0.6119

              precision    recall  f1-score   support

           0     0.7436    0.3816    0.5043        76
           1     0.5727    0.8630    0.6885        73

    accuracy                         0.6174       149
   macro avg     0.6582    0.6223    0.5964       149
weighted avg     0.6599    0.6174    0.5946       149

array([[29, 47],
       [10, 63]])
       
En el conjunto de prueba, la CNN clasificó correctamente el 61.74% de las imágenes. El ROC-AUC de 0.6119 indica una capacidad limitada para distinguir entre vidrio y plástico. Por tanto, aunque el modelo aprendió ciertos patrones durante el entrenamiento, su capacidad de generalización es todavía reducida.


Figura 3. Matriz de confusión de CNN desde cero (5.4 en el código) <img width="364" height="341" alt="image" src="https://github.com/user-attachments/assets/76f31742-7e02-464d-95f6-136c9a373dee" />
De las 76 imágenes de vidrio, 29 fueron clasificadas correctamente y 47 fueron confundidas con plástico. En cambio, de las 73 imágenes de plástico, 63 fueron clasificadas correctamente y 10 fueron confundidas con vidrio. La matriz evidencia que el principal problema del modelo es la identificación del vidrio.


Figura 4. Gráfico de sobrecorrección <img width="826" height="813" alt="copyImage" src="https://github.com/user-attachments/assets/882b9bf4-10a2-4b72-8395-5a310dfe4941" />




























