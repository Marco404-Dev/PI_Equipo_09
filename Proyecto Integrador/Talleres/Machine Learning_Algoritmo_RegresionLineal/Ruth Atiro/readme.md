# Inteligencia Artificial **(IA)**
La inteligencia artificial es un campo o disciplina de la informática que se encarga de desarrollar programas y sistemas capaces de percibir su entorno, procesar información, razonar y tomar decisiones que emiten el comportamiento y la inteligencia humana.

Durante la clase práctica, usamos el Machine Learning en un cuaderno de Colab mediante el algoritmo de "Regresión Lineal" de la libreria _scikit-learn_. En el código _lm.flit(x_train, y_train)_, es donde se realiza el entrenamiento del modelo; la "IA" aprende a partir de los datos proporcionados la relación matemática entre el consumo de energía y los factores operativos y ambientales, calculando los pesos óptimos para la realización de predicciones.

## Análisis y Evaluación
1. Densidad: ¿Dónde están concentrados los datos?
   
   <img width="576" height="413" alt="image" src="https://github.com/user-attachments/assets/478faa75-d745-4f64-b7f2-61f6d5b1d3a0" />

   - Código: df['Consumo_Energia'].plot.density()
             '''
             Densidad: ¿Dónde están concentrados los datos?
             '''
     
   - Descripción: El gráfico representa la distribución de los valores de "Consumo_Energia" registrados en el dataset (archivo csv), los cuales se encuentran aproximadamente entre 10 y 40 unidades en el eje X. El eje Y (densidad) indica la densidad de probabilidad relativa, por lo que mientras más alta sea la curva en un determinado valor del eje X, mayor será la concentración de observaciones alrededor de ese valor. La curva presenta una forma aproximadamente "simétrica y acampanada", similar a una **distribución normal o curva de Gauss**, lo que permite observar de manera visual en qué valores se concentra principalmente el consumo de energía.
     
   - Interpretación: El gráfico muestra una concentración central cuyo punto más alto se encuentra alrededor de 26 unidades, lo que indica que gran parte de los registros presenta valores de consumo de energía cercanos a este valor, ubicándose la media y la mediana en esta zona central. Además, la mayor densidad de datos se encuentra aproximadamente entre 20 y 32 unidades, representando el rango de consumo habitual del sistema durante su operación. En los extremos, la curva desciende progresivamente hacia cero, tanto para valores cercanos a 10 unidades como para valores entre 40 y 45 unidades, lo que indica que los consumos muy bajos, menores a 15, o muy altos, mayores a 38, aparecen con menor frecuencia en los datos analizados. Finalmente, esta distribución continua, suave y sin sesgos marcados permite observar que la variable Consumo_Energia presenta un comportamiento adecuado para ser analizado mediante un modelo de Regresión Lineal, sin que sea necesario aplicar previamente transformaciones como una escala logarítmica.

   2. hm

      - Código:
        l = list(cdf.index)

from matplotlib import gridspec
fig = plt.figure(figsize=(18,10))
gs= gridspec.GridSpec(2,2)

ax0=plt.subplot(gs[0])
ax0.scatter(df[l[0]], df['Consumo_Energia'])
ax0.set_title(l[0] + "vs. Consumo_Energia", fontdict= {'fontsize':20})

ax1=plt.subplot(gs[1])
ax1.scatter(df[l[1]], df['Consumo_Energia'])
ax1.set_title(l[1] + "vs. Consumo_Energia", fontdict= {'fontsize':20})

ax2=plt.subplot(gs[2])
ax2.scatter(df[l[2]], df['Consumo_Energia'])
ax2.set_title(l[2] + "vs. Consumo_Energia", fontdict= {'fontsize':20})

ax3=plt.subplot(gs[3])
ax3.scatter(df[l[3]], df['Consumo_Energia'])
ax3.set_title(l[3] + "vs. Consumo_Energia", fontdict= {'fontsize':20})


