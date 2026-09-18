# Regresión lineal aplicada a PM10 (2022–2023)
# County: AL, Jefferson County 

## Introducción

El material particulado PM10 forma parte de los contaminantes monitoreados por la Agencia de Protección Ambiental de los Estados Unidos (EPA). Para este trabajo se utilizaron datos obtenidos de **AirData**, plataforma de la EPA que permite acceder a información histórica y reciente registrada por estaciones de monitoreo de calidad del aire [1].

El conjunto analizado corresponde a mediciones de PM10 realizadas entre el **1 de enero de 2022 y el 31 de diciembre de 2023**. La base contiene **3430 registros y 28 variables**, provenientes de **5 estaciones de monitoreo**. La variable de interés es `Daily Mean PM10 Concentration`, expresada en microgramos por metro cúbico (µg/m³).

El objetivo principal fue evaluar si la **latitud, longitud y elevación de las estaciones** permiten estimar la concentración diaria de PM10 mediante un modelo de regresión lineal. Como complemento, se utilizaron datos artificiales generados específicamente para regresión con el fin de comparar el comportamiento de una relación lineal conocida con el comportamiento observado en los datos reales.

---

## 1. Metodología

### 1.1. Carga y exploración del conjunto de datos

El archivo fue cargado con `pandas` y posteriormente se revisó su estructura mediante `head()`, `info()` y `describe()`.

<img width="901" height="135" alt="Screenshot 2026-09-18 182754" src="https://github.com/user-attachments/assets/674b58de-4e70-4700-b3c7-574b2a2a488d" />


La exploración mostró **3430 filas y 28 columnas**. El periodo comprendido en el archivo va de 2022-01-01 a 2023-12-31 y se identificaron cinco estaciones distintas.

También se verificaron registros duplicados, unidades, fechas y cantidad de estaciones.

<img width="760" height="350" alt="Screenshot 2026-09-18 182947" src="https://github.com/user-attachments/assets/a13a5413-7235-48f8-be24-7d11aefd6963" />


No se encontraron duplicados exactos. Las concentraciones de PM10 están expresadas en `Micrograms/cubic meter (25 C)`.



---

### 1.2. Limpieza de datos

La limpieza se limitó a eliminar duplicados exactos y registros sin fecha o concentración válida. La columna `Date` fue convertida a formato de fecha y la concentración de PM10 a formato numérico.

<img width="832" height="336" alt="Screenshot 2026-09-18 183017" src="https://github.com/user-attachments/assets/52b74057-f4c8-430f-abbc-ddac07de4e1c" />


Después de este procedimiento se conservaron los **3430 registros**, por lo que no fue necesario retirar filas.

---

### 1.3. Distribución de la concentración de PM10

Se utilizaron un histograma y un diagrama de caja para observar la distribución de la variable objetivo.
<img width="768" height="457" alt="Screenshot 2026-09-18 183143" src="https://github.com/user-attachments/assets/39881abd-83d3-464c-8bdc-1511b14c5bed" />



Las concentraciones se concentran principalmente entre valores bajos y medios. La mediana es aproximadamente **18 µg/m³**, mientras que el rango observado va de **2 a 110 µg/m³**. La distribución presenta asimetría hacia la derecha y existen observaciones altas que pueden representar episodios de mayor concentración.

<img width="1557" height="567" alt="Screenshot 2026-09-18 183156" src="https://github.com/user-attachments/assets/d3ee452b-c15f-4b0d-8c84-aeab6201ee93" />


---

### 1.4. Análisis de correlación

Se analizó la correlación entre PM10, AQI y las características geográficas de las estaciones.
<img width="697" height="353" alt="Screenshot 2026-09-18 183406" src="https://github.com/user-attachments/assets/08d377ac-97ec-4bf4-b0e8-b112e65dc891" />



La concentración de PM10 presenta una correlación positiva muy alta con `Daily AQI Value`. Sin embargo, esta variable no fue utilizada como predictor porque el AQI se obtiene a partir de las concentraciones de contaminantes mediante los procedimientos establecidos por la EPA [2]. Utilizarla como entrada para estimar PM10 introduciría información directamente relacionada con la variable objetivo.

Las variables geográficas mostraron correlaciones lineales débiles con PM10: aproximadamente **0.05 para latitud**, **-0.04 para longitud** y **-0.12 para elevación**.
<img width="920" height="736" alt="descarga" src="https://github.com/user-attachments/assets/ecea325d-456f-4018-a0db-81b2af647574" />


---

### 1.5. Preparación de los datos

Las variables predictoras utilizadas fueron:

- `Site Latitude`
- `Site Longitude`
- `Elevation (m)`

La variable objetivo fue:

- `Daily Mean PM10 Concentration`

Los datos se dividieron aleatoriamente en **70 % para entrenamiento y 30 % para prueba**, utilizando `random_state=123` para mantener la reproducibilidad [3].

<img width="553" height="150" alt="Screenshot 2026-09-18 183856" src="https://github.com/user-attachments/assets/74464bf5-46eb-491c-987c-54324a1fcbe5" />


---

### 1.6. Regresión lineal con los datos reales de PM10

Se utilizó `LinearRegression()` de Scikit-learn para ajustar un modelo lineal mediante mínimos cuadrados ordinarios [4].

<img width="622" height="282" alt="Screenshot 2026-09-18 183928" src="https://github.com/user-attachments/assets/c3e4570b-7881-4c1c-a770-c3b2fe5bf6bb" />


El modelo fue evaluado mediante **MAE** y **R²**. El MAE mide el error absoluto promedio y su mejor valor es 0 [5]. El coeficiente R² permite medir la proporción de variabilidad explicada por el modelo.

Los resultados obtenidos fueron:


<img width="243" height="45" alt="Screenshot 2026-09-18 184003" src="https://github.com/user-attachments/assets/e22ed346-246a-4b50-bd34-bfd1782c9631" />


El modelo presentó un error absoluto promedio de aproximadamente **7.23 µg/m³** y un **R² de 0.0598**. Esto indica que las variables geográficas utilizadas explican solamente una pequeña parte de las variaciones diarias observadas en PM10.

Los coeficientes obtenidos fueron:

<img width="612" height="157" alt="Screenshot 2026-09-18 184131" src="https://github.com/user-attachments/assets/0aa19840-191b-4df7-8123-734eacbbaa36" />



---

### 1.7. Comparación entre valores reales y predichos

Se compararon los valores reales de PM10 con las predicciones generadas por el modelo.


Los puntos forman principalmente bandas horizontales y no una tendencia diagonal. Esto indica que el modelo genera valores similares para determinadas ubicaciones aunque las concentraciones reales cambien entre días.


<img width="295" height="397" alt="Screenshot 2026-09-18 184314" src="https://github.com/user-attachments/assets/1e924343-680f-40cf-a98d-4d14612ce29b" />

---

### 1.8. Análisis de residuos

Los residuos se calcularon como la diferencia entre la concentración real y la predicción.

La distribución se concentra alrededor de cero, pero presenta una **asimetría positiva y una cola hacia la derecha**. Esto evidencia que existen concentraciones elevadas que el modelo tiende a subestimar.

<img width="852" height="647" alt="descarga (1)" src="https://github.com/user-attachments/assets/8cb5e728-c096-4222-b52b-934a89b13cd7" />


La aparición de bandas y residuos alejados de cero respalda la conclusión de que la latitud, longitud y elevación no son suficientes para representar la variación diaria de PM10.



---

### 1.9. Análisis complementario con datos artificiales

Debido al bajo desempeño obtenido con las características geográficas de los datos reales, se realizó un análisis complementario con datos artificiales generados mediante `make_regression()`. Esta función permite crear un problema de regresión con una relación lineal controlada [6].

Se generaron:

- 100 muestras.
- 6 características.
- 3 características informativas.
- Ruido de 20.
- `random_state=20`.

<img width="616" height="497" alt="Screenshot 2026-09-18 184630" src="https://github.com/user-attachments/assets/60dd9644-2c38-4b4d-974a-f2fb4a49ef54" />


Los coeficientes reales utilizados en la generación fueron aproximadamente:
<img width="697" height="265" alt="Screenshot 2026-09-18 184635" src="https://github.com/user-attachments/assets/14e26d2c-23c1-482c-ad5c-d54c2c42fb05" />


Esto permitió comprobar el comportamiento de la regresión cuando los datos sí contienen una relación lineal definida.

---

### 1.10. Comparación entre regresión lineal y árbol de decisión

Los datos artificiales se dividieron nuevamente en 70 % para entrenamiento y 30 % para prueba.
<img width="676" height="300" alt="Screenshot 2026-09-18 184902" src="https://github.com/user-attachments/assets/b08c55e4-7413-4f1a-b7d3-80d55b0a41fa" />



También se entrenó un `DecisionTreeRegressor` con una profundidad máxima de 5 [7].

<img width="707" height="512" alt="Screenshot 2026-09-18 184744" src="https://github.com/user-attachments/assets/7b22caad-ade6-41c1-b422-b134f4502308" />


La comparación fue:

<img width="392" height="113" alt="Screenshot 2026-09-18 184727" src="https://github.com/user-attachments/assets/3d4c8ecf-56e5-4624-865f-51a0023f27cb" />


En este conjunto artificial, la regresión lineal presentó un desempeño considerablemente superior porque los datos fueron generados bajo una estructura lineal.

El análisis de importancia del árbol mostró que `x2`, `x1` y `x3` fueron las variables con mayor aporte, coincidiendo con las características informativas usadas para crear el conjunto.

<img width="900" height="450" alt="Screenshot 2026-09-18 184956" src="https://github.com/user-attachments/assets/09b60472-65e4-4c88-a20e-9c726fcb3607" />


---

### 1.11. Análisis mediante mínimos cuadrados ordinarios

Como complemento estadístico se utilizó `statsmodels` para ajustar un modelo de mínimos cuadrados ordinarios (OLS) sobre los datos artificiales [8].

<img width="837" height="607" alt="Screenshot 2026-09-18 185037" src="https://github.com/user-attachments/assets/b12f6d10-b645-47e0-82c9-a65c7557d82e" />


El modelo obtuvo:

- **R² = 0.974**
- **R² ajustado = 0.972**
- **70 observaciones de entrenamiento**

Los coeficientes de `x1`, `x2` y `x3` fueron los de mayor magnitud y presentaron valores p muy pequeños en el resumen OLS, mientras que `x4`, `x5` y `x6` no mostraron el mismo comportamiento. Esto concuerda con la forma en que se generaron los datos artificiales, donde únicamente las tres primeras variables fueron definidas como informativas.

---

## 2. Resultados

El conjunto de datos real estuvo compuesto por **3430 registros, 28 columnas y cinco estaciones de monitoreo**, correspondientes al periodo 2022–2023. La concentración media diaria de PM10 fue aproximadamente **20.10 µg/m³**, con una mediana de **18 µg/m³** y valores comprendidos entre **2 y 110 µg/m³**.

El modelo construido con latitud, longitud y elevación obtuvo un **MAE de 7.23 µg/m³** y un **R² de 0.0598**. Por lo tanto, estas tres características geográficas explicaron una proporción reducida de la variabilidad diaria de PM10.

Los gráficos de valores reales frente a predichos y el análisis de residuos mostraron que las predicciones presentan poca variación y que el modelo tiende a subestimar algunas concentraciones altas.

En el análisis complementario, la regresión lineal aplicada a los datos artificiales obtuvo un **R² de 0.9756**, mientras que el árbol de decisión alcanzó **0.5459**. El modelo OLS aplicado sobre los datos de entrenamiento artificiales produjo un **R² de 0.974** y un R² ajustado de **0.972**.

La diferencia entre los resultados reales y artificiales muestra que el bajo desempeño sobre PM10 no se debe al procedimiento de regresión en sí, sino a que las variables geográficas seleccionadas contienen poca información sobre los cambios diarios de concentración.

---

## 3. Discusión

La regresión lineal aplicada a los datos reales presentó un R² bajo. Este resultado coincide con el análisis de correlación y con los gráficos de dispersión, en los cuales no se observó una relación lineal fuerte entre PM10 y latitud, longitud o elevación.

Estas características describen principalmente la ubicación fija de cada estación. Por ello, permiten diferenciar sitios de monitoreo, pero no incorporan factores que cambian diariamente y que podrían relacionarse con las fluctuaciones de PM10. Dentro del conjunto analizado, esto limita su capacidad predictiva.

La alta correlación entre `Daily AQI Value` y PM10 no se utilizó para mejorar artificialmente el modelo. La EPA indica que el AQI se calcula a partir de los datos de concentración de contaminantes [2]; por esta razón, utilizar AQI como predictor de PM10 supondría incorporar información derivada de la propia concentración que se desea estimar.

El análisis con datos artificiales permitió contrastar esta situación. Debido a que `make_regression()` genera una variable objetivo mediante una combinación lineal de características informativas, la regresión lineal obtuvo un R² elevado. El árbol de decisión presentó un rendimiento inferior en este conjunto específico, mientras que el análisis OLS confirmó que las tres variables informativas fueron las principales asociadas a la respuesta.

Como limitación, la división de los datos reales se realizó de forma aleatoria. Por tanto, los resultados evalúan el desempeño sobre registros separados aleatoriamente y no constituyen una validación específica para pronosticar fechas futuras.

---

## 4. Referencias

[1] U.S. Environmental Protection Agency, “AirData: Air Quality Data Collected at Outdoor Monitors Across the US,” *U.S. EPA*. [Online]. Available: https://www.epa.gov/outdoor-air-quality-data. [Accessed: Sep. 18, 2026].


