# Análisis Exploratorio y Evaluación de Modelos

---

## 1. Histograma de Consumo de Energía
### Código: 
df['Consumo_Energia'].plot.hist(bins=25, figsize=(8,4))
'''
Histograma: ¿Cómo se distribuyen los datos por intervalos?

'''
<img width="691" height="369" alt="image" src="https://github.com/user-attachments/assets/4375a0ee-2e91-49b3-ba5b-22aa097ec867" />

### Descripción: 
Este histograma divide la variable Consumo_Energia en 25 intervalos (barras) y cuenta cuántas veces (frecuencia en el eje vertical) se repiten los valores dentro de cada rango.

### Interpretación: 
- Los datos tienen una forma de campana (distribución aproximadamente normal).
- La mayoría de los datos se concentran en la parte central, específicamente entre los valores de 20 y 30, teniendo su punto más alto (el pico de mayor frecuencia) alrededor de 25-26.
- Los consumos muy bajos (cercanos a 10) o muy altos (cercanos a 40) son poco frecuentes en este conjunto de datos.

- ¿Cuándo se recomienda usarlo? Se recomienda utilizarlo durante el Análisis Exploratorio de Datos (EDA) para entender el comportamiento de las variables numéricas, detectar valores atípicos (outliers) y ver si los datos están sesgados o siguen una distribución normal antes de entrenar un modelo.

---

## 2. Gráfico de Dispersión (Valores Reales vs. Predicciones) y MSE
### Código: 
from sklearn import metrics
test_pred = tree_model.predict(X_test)
plt.scatter(x=y_test, y = test_pred)
print("Mean square error (MSE):", metrics.mean_squared_error(y_test,test_pred))

<img width="561" height="426" alt="image" src="https://github.com/user-attachments/assets/22ea4542-6c3d-4515-aa7a-f1cdaff3b641" />

### Descripción: 
Es un gráfico de dispersión que enfrenta los valores reales (y_test en el eje horizontal) contra lo que predijo el modelo de árbol de decisión (test_pred en el eje vertical). Además, calcula el Error Cuadrático Medio (MSE), que en este caso es de aproximadamente 7931.57.

### Interpretación: 
- Tendencia: Se observa una ligera diagonal ascendente (de abajo hacia la izquierda, hacia arriba y a la derecha). Esto nos indica que el modelo sí capta la tendencia general de los datos (cuando el valor real es grande, el modelo tiende a predecir un valor grande).
- Dispersión y Error: Los puntos no forman una línea perfecta, sino que están dispersos. Esto significa que el modelo comete errores en sus estimaciones individuales. El valor del MSE (7931.57) cuantifica numéricamente qué tan grande es ese error global (al elevar al cuadrado las diferencias); un número alto nos dice que hay margen de mejora y que las predicciones se alejan considerablemente de los valores reales en algunos puntos.
  
- ¿Cuándo se recomienda usarlo? Se recomienda al evaluar modelos de regresión (cuando tu objetivo es predecir un valor numérico continuo, como precios, temperaturas o consumos), ya que te permite visualizar gráficamente si el modelo acierta o si sobreestima/subestima ciertos rangos de datos.


