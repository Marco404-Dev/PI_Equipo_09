Análisis de Tablas del Taller de Regresión Lineal (modelo base de ML)

📊 Tabla 1: Estadísticas Descriptivas (df.describe())

Estadístico Temperatura Horas_Operation Carga Humedad Consumo_Energia
count 5000 5000 5000 5000 5000
mean — — — — —
std — — — — —
min — — — — —
25% — — — — —
50% — — — — —
75% — — — — —
max — — — — —

🔍 Interpretación a grandes rasgos

· count = 5000 en todas las columnas, por ende no hay valores nulos.
· Todas las variables son float64, no se requiere codificación.
· Los valores de mean, std, min y max permiten detectar:
  · Escalas muy distintas entre features, es posible necesidad de normalización.
  · Outliers (si max está muy alejado del percentil 75).
  · Distribuciones sesgadas (si mean ≠ 50%).



📋 Tabla 2: Coeficientes del Modelo Lineal (Datos Reales)

Feature Coefficient Standard Error t-statistic
Temperatura 0.137 — —
Horas_Operation 1.669 — —
Carga 0.096 — —
Humedad 0.027 — —
Intercepto 2.741 — —

🔍 Interpretación

Coeficientes (Coefficients)

· Representan el cambio esperado en Consumo_Energia por cada unidad de aumento en la feature, manteniendo las demás constantes.
· Horas_Operation (1.669) es la variable más influyente: cada hora adicional de operación incrementa el consumo en ~1.67 unidades.
· Temperatura (0.137), Carga (0.096) y Humedad (0.027) tienen efectos mucho menores.
· El intercepto (2.741) es el valor base de consumo cuando todas las features son 0 (puede o no tener sentido físico).

Error Estándar (Standard Error)

· Mide la precisión de cada coeficiente estimado.
· Un error estándar pequeño → estimación confiable.
· Fórmula usada:
  SE(\hat\beta_i) = \sqrt{\frac{\sum (y - \hat y)^2 / (n-k)}{\sum (x_i - \bar x_i)^2}}
· Un feature con mayor varianza produce un SE más pequeño (mejor estimación).

Estadístico t (t-statistic)

· Se calcula como Coeficiente / Error Estándar.
· Regla práctica: si |t| > 2 → el coeficiente es estadísticamente significativo (p-value < 0.05 aproximadamente).
· Permite decidir qué variables aportan al modelo y cuáles podrían eliminarse.


🧪 Tabla 3: Coeficientes Verdaderos (Datos Sintéticos)

Generados con make_regression(n_features=6, n_informative=3, coef=True):

Feature Coeficiente Verdadero ¿Influye?
x1 78.586 ✅ Sí
x2 97.724 ✅ Sí
x3 52.306 ✅ Sí
x4 0.000 ❌ No
x5 0.000 ❌ No
x6 0.000 ❌ No

🔍 Interpretación

· Solo 3 de 6 features son informativas (n_informative=3).
· Los coeficientes de x4, x5, x6 son exactamente 0 → no aportan información.
· Este dataset sirve como prueba de validación: si el modelo ajustado recupera coeficientes cercanos a estos valores, el pipeline funciona correctamente.


📈 Tabla 4: Resultados de Predicción (Test Set)

Métrica Valor
Tipo de objeto numpy.ndarray
Tamaño de predicciones (1500,)
Tamaño de y_test (1500,)
test_size 0.3 (30% de 5000)
random_state 123

🔍 Interpretación

· El conjunto de prueba tiene 1500 observaciones (30% del total).
· Las predicciones son un array de numpy de igual tamaño que y_test, lo que permite comparación directa.
· La semilla random_state=123 garantiza reproducibilidad del split.


🎯 Tabla 5: Diagnóstico del Modelo (Gráficos)

Aunque no son tablas numéricas, los tres gráficos de diagnóstico son equivalentes a una tabla de validación:

Gráfico Qué evalúa Qué esperar si el modelo es bueno
Real vs Predicho Ajuste global Puntos cerca de la diagonal y = x
Histograma de residuos Normalidad Forma de campana centrada en 0
Residuos vs Predichos Homocedasticidad Nube aleatoria sin patrón
Scatter feature vs target Linealidad Tendencia lineal clara (si no, transformar)


🛠️ Recomendaciones para Mejorar el Análisis

1. Agregar statsmodels para obtener p-values automáticamente.
2. Calcular R², RMSE y MAE en el test set para cuantificar el ajuste.
3. Estandarizar features si las escalas son muy distintas.
4. Revisar multicolinealidad con VIF (Variance Inflation Factor).
5. Validación cruzada (k-fold) para una estimación más robusta del desempeño.
