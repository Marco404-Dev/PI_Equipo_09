# Informe de Análisis: Regresión Lineal Temporal del Ozono (Colorado 2022-2023)
---
## 1. Introducción
El ozono troposférico (O_3) es uno de los contaminantes atmosféricos más importantes debido a su impacto en la salud humana y los ecosistemas. A diferencia de otros contaminantes, el ozono no se emite directamente en su mayoría, sino que se forma mediante reacciones fotoquímicas complejas entre óxidos de nitrógeno (NO_x) y compuestos orgánicos volátiles (COV) en presencia de luz solar. Por esta razón, presenta una fuerte dependencia estacional, alcanzando concentraciones máximas durante las épocas cálidas del año. Este informe analiza el comportamiento diario del ozono máximo en el estado de Colorado durante el período 2022-2023 mediante técnicas de ciencia de datos y regresión lineal simple.
## 2. Metodología
Para realizar este análisis se siguieron los siguientes pasos computacionales y estadísticos en Google Colab:
 * Obtención y carga de datos: Se utilizó un conjunto de datos consolidado de la EPA (AirData) para el estado de Colorado abarcando los años 2022 y 2023, con un total inicial de aproximadamente 29,000 registros provenientes de diversas estaciones de monitoreo (Local Site Name).
 * Limpieza y transformación: Se seleccionaron las columnas clave (Date y Daily Max Ozone Concentration). Se eliminaron los valores nulos (.dropna()) y se transformó la variable de fecha a un índice numérico secuencial (Day_Index) que representa los días transcurridos desde el inicio del registro.
 * Modelo de Regresión Lineal:
   * Se dividió el conjunto de datos en un 80% para entrenamiento y un 20% para prueba utilizando train_test_split.
   * Se implementó el algoritmo de Regresión Lineal Simple de la librería scikit-learn, tomando el índice de tiempo (X) como variable independiente para predecir la concentración máxima diaria de ozono (Y).
 * Evaluación y Visualización: Se calcularon métricas de error y desempeño (como el Error Cuadrático Medio y el coeficiente de determinación R^2) y se generó una gráfica de dispersión con la línea de tendencia temporal.
 * Código Fuente: El script ejecutable completo de este análisis puede consultarse en el siguiente enlace de Google Colab: https://colab.research.google.com/drive/1pD6PM8lBeRYKBEwnvv1dSyJOlKG25Dmg?authuser=4#scrollTo=dEnqz2BwqbuB
## 3. Resultados
 * Comportamiento general: El modelo de regresión lineal generó una línea de tendencia global prácticamente horizontal a lo largo de los dos años analizados.
 * Estacionalidad: La visualización gráfica permitió identificar claramente dos ciclos anuales bien definidos (correspondientes a los veranos de 2022 y 2023), donde las concentraciones de ozono experimentan incrementos drásticos en comparación con los meses de invierno.
 * Dispersión: Debido a la inclusión de múltiples estaciones de monitoreo con distintas condiciones geográficas y de altitud en todo Colorado, los puntos reales muestran una dispersión considerable alrededor de la tendencia central.
> Figura 1. Regresión Lineal: Ozono vs. Tiempo (Colorado 2022-2023).
<div align="center">
  <img width="842" height="453" alt="image" src="https://github.com/user-attachments/assets/0e76a8c8-40e8-44e4-804f-301b4882bebf" />
</div>
## 4. Discusión
Aunque la pendiente de la regresión lineal global muestra una estabilidad casi nula entre 2022 y 2023, el valor real del análisis radica en la estacionalidad. Una regresión lineal simple basada estrictamente en el tiempo tiende a promediar los ciclos estacionales, lo que resulta en un coeficiente de determinación (R^2) bajo para capturar variaciones diarias, pero excelente para demostrar visualmente el fenómeno fotoquímico anual. Para futuros análisis más precisos, se recomendaría filtrar estaciones individuales (por ejemplo, zonas urbanas específicas como Denver) o incorporar variables meteorológicas independientes como la temperatura ambiente y la radiación solar.
## 5. Referencias (Formato IEEE)
[1] U. S. Environmental Protection Agency (EPA), "AirData: Access Air Data" [En línea]. Disponible en: https://www.epa.gov/outdoor-air-quality-data.
