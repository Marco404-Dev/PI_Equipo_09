# Regresión lineal aplicada a PM10 (2022–2023)

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

```python
exploracion = [
    objetivo,
    'Daily AQI Value',
    'Site Latitude',
    'Site Longitude',
    'Elevation (m)'
]

sns.heatmap(
    df[exploracion].corr(),
    annot=True,
    fmt='.2f',
    cmap='coolwarm',
    vmin=-1,
    vmax=1
)
```

La concentración de PM10 presenta una correlación positiva muy alta con `Daily AQI Value`. Sin embargo, esta variable no fue utilizada como predictor porque el AQI se obtiene a partir de las concentraciones de contaminantes mediante los procedimientos establecidos por la EPA [2]. Utilizarla como entrada para estimar PM10 introduciría información directamente relacionada con la variable objetivo.

Las variables geográficas mostraron correlaciones lineales débiles con PM10: aproximadamente **0.05 para latitud**, **-0.04 para longitud** y **-0.12 para elevación**.

**Imagen 3 – Matriz de correlación**

![Matriz de correlación](Capturas/matriz_correlacion.png)

*Figura 3. Correlaciones entre PM10, AQI y características geográficas.*

---

### 1.5. Preparación de los datos

Las variables predictoras utilizadas fueron:

- `Site Latitude`
- `Site Longitude`
- `Elevation (m)`

La variable objetivo fue:

- `Daily Mean PM10 Concentration`

```python
variables = [
    'Site Latitude',
    'Site Longitude',
    'Elevation (m)'
]

X = df[variables]
y = df['Daily Mean PM10 Concentration']
```

Los datos se dividieron aleatoriamente en **70 % para entrenamiento y 30 % para prueba**, utilizando `random_state=123` para mantener la reproducibilidad [3].

```python
X_train, X_test, y_train, y_test = train_test_split(
    X,
    y,
    test_size=0.30,
    random_state=123
)
```

---

### 1.6. Regresión lineal con los datos reales de PM10

Se utilizó `LinearRegression()` de Scikit-learn para ajustar un modelo lineal mediante mínimos cuadrados ordinarios [4].

```python
lm = LinearRegression()
lm.fit(X_train, y_train)

predicciones = lm.predict(X_test)
```

El modelo fue evaluado mediante **MAE** y **R²**. El MAE mide el error absoluto promedio y su mejor valor es 0 [5]. El coeficiente R² permite medir la proporción de variabilidad explicada por el modelo.

Los resultados obtenidos fueron:

| Métrica | Resultado |
|---|---:|
| MAE | 7.23 µg/m³ |
| R² | 0.0598 |

El modelo presentó un error absoluto promedio de aproximadamente **7.23 µg/m³** y un **R² de 0.0598**. Esto indica que las variables geográficas utilizadas explican solamente una pequeña parte de las variaciones diarias observadas en PM10.

Los coeficientes obtenidos fueron:

| Variable | Coeficiente |
|---|---:|
| Site Latitude | -532.1994 |
| Site Longitude | 81.8109 |
| Elevation (m) | -1.7880 |

El intercepto fue aproximadamente **25300.55**. Estos coeficientes describen el ajuste matemático del modelo para las estaciones incluidas en el conjunto analizado; debido al bajo R², no deben interpretarse de forma aislada como relaciones causales.

---

### 1.7. Comparación entre valores reales y predichos

Se compararon los valores reales de PM10 con las predicciones generadas por el modelo.

```python
plt.figure(figsize=(10,7))

plt.title("PM10 real vs. Predicción")
plt.xlabel("PM10 real")
plt.ylabel("PM10 predicho")

plt.scatter(
    x=y_test,
    y=predicciones
)

plt.show()
```

Los puntos forman principalmente bandas horizontales y no una tendencia diagonal. Esto indica que el modelo genera valores similares para determinadas ubicaciones aunque las concentraciones reales cambien entre días.

**Imagen 4 – PM10 real frente a predicción**

![PM10 real vs predicción](Capturas/real_vs_predicho.png)

*Figura 4. Comparación entre valores reales y predichos de PM10.*

---

### 1.8. Análisis de residuos

Los residuos se calcularon como la diferencia entre la concentración real y la predicción.

```python
residuos = y_test - predicciones

sns.histplot(
    residuos,
    kde=True
)

plt.show()
```

La distribución se concentra alrededor de cero, pero presenta una **asimetría positiva y una cola hacia la derecha**. Esto evidencia que existen concentraciones elevadas que el modelo tiende a subestimar.

También se analizaron los residuos respecto a los valores predichos.

```python
plt.scatter(
    x=predicciones,
    y=y_test - predicciones
)

plt.axhline(y=0, linestyle="--")
plt.show()
```

La aparición de bandas y residuos alejados de cero respalda la conclusión de que la latitud, longitud y elevación no son suficientes para representar la variación diaria de PM10.

**Imagen 5 – Análisis de residuos**

![Residuos](Capturas/residuos.png)

*Figura 5. Distribución de los residuos del modelo de PM10.*

---

### 1.9. Análisis complementario con datos artificiales

Debido al bajo desempeño obtenido con las características geográficas de los datos reales, se realizó un análisis complementario con datos artificiales generados mediante `make_regression()`. Esta función permite crear un problema de regresión con una relación lineal controlada [6].

Se generaron:

- 100 muestras.
- 6 características.
- 3 características informativas.
- Ruido de 20.
- `random_state=20`.

```python
X_artificial, y_artificial, coef_reales = make_regression(
    n_samples=100,
    n_features=6,
    n_informative=3,
    noise=20,
    shuffle=False,
    coef=True,
    random_state=20
)
```

Los coeficientes reales utilizados en la generación fueron aproximadamente:

```text
x1 = 78.59
x2 = 97.72
x3 = 52.31
x4 = 0
x5 = 0
x6 = 0
```

Esto permitió comprobar el comportamiento de la regresión cuando los datos sí contienen una relación lineal definida.

---

### 1.10. Comparación entre regresión lineal y árbol de decisión

Los datos artificiales se dividieron nuevamente en 70 % para entrenamiento y 30 % para prueba.

La regresión lineal obtuvo:

| Modelo | MAE | R² |
|---|---:|---:|
| Regresión lineal | 16.2615 | 0.9756 |

También se entrenó un `DecisionTreeRegressor` con una profundidad máxima de 5 [7].

```python
arbol_art = DecisionTreeRegressor(
    max_depth=5,
    random_state=10
)
```

La comparación fue:

| Modelo | MAE | R² |
|---|---:|---:|
| Regresión lineal | 16.2615 | 0.9756 |
| Árbol de decisión | 69.8909 | 0.5459 |

En este conjunto artificial, la regresión lineal presentó un desempeño considerablemente superior porque los datos fueron generados bajo una estructura lineal.

El análisis de importancia del árbol mostró que `x2`, `x1` y `x3` fueron las variables con mayor aporte, coincidiendo con las características informativas usadas para crear el conjunto.

**Imagen 6 – Importancia de variables en el árbol**

![Importancia de variables](Capturas/importancia_variables.png)

*Figura 6. Importancia relativa de las variables en el árbol de decisión.*

---

### 1.11. Análisis mediante mínimos cuadrados ordinarios

Como complemento estadístico se utilizó `statsmodels` para ajustar un modelo de mínimos cuadrados ordinarios (OLS) sobre los datos artificiales [8].

```python
Xs_art = sm.add_constant(X_train_art)
ols_art = sm.OLS(y_train_art, Xs_art).fit()

print(ols_art.summary())
```

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

[2] U.S. Environmental Protection Agency, “How is the AQI calculated?,” *U.S. EPA*. [Online]. Available: https://www.epa.gov/outdoor-air-quality-data/how-aqi-calculated. [Accessed: Sep. 18, 2026].

[3] Scikit-learn Developers, “train_test_split,” *Scikit-learn Documentation*. [Online]. Available: https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.train_test_split.html. [Accessed: Sep. 18, 2026].

[4] Scikit-learn Developers, “LinearRegression,” *Scikit-learn Documentation*. [Online]. Available: https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LinearRegression.html. [Accessed: Sep. 18, 2026].

[5] Scikit-learn Developers, “mean_absolute_error,” *Scikit-learn Documentation*. [Online]. Available: https://scikit-learn.org/stable/modules/generated/sklearn.metrics.mean_absolute_error.html. [Accessed: Sep. 18, 2026].

[6] Scikit-learn Developers, “make_regression,” *Scikit-learn Documentation*. [Online]. Available: https://scikit-learn.org/stable/modules/generated/sklearn.datasets.make_regression.html. [Accessed: Sep. 18, 2026].

[7] Scikit-learn Developers, “DecisionTreeRegressor,” *Scikit-learn Documentation*. [Online]. Available: https://scikit-learn.org/stable/modules/generated/sklearn.tree.DecisionTreeRegressor.html. [Accessed: Sep. 18, 2026].

[8] Statsmodels Developers, “Linear Regression,” *Statsmodels Documentation*. [Online]. Available: https://www.statsmodels.org/stable/regression.html. [Accessed: Sep. 18, 2026].
