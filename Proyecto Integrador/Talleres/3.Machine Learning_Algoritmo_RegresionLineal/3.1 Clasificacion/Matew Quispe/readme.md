# APLICACIÓN DE REGRESIÓN LINEAL AL ANÁLISIS DE CONCENTRACIONES DIARIAS DE SO₂ Y EL ÍNDICE DE CALIDAD DEL AIRE

## 1. Introducción

El dióxido de azufre (SO₂) es uno de los contaminantes criterio considerados en el Índice de Calidad del Aire (AQI, por sus siglas en inglés). La Agencia de Protección Ambiental de los Estados Unidos (EPA) dispone de la plataforma AirData para consultar y descargar datos recientes e históricos obtenidos por monitores de calidad del aire instalados en exteriores [1]. La herramienta de descarga diaria de AirData permite obtener estadísticas resumidas por contaminante y por monitor [2].

En este trabajo se aplicó un modelo de regresión lineal simple a datos diarios de SO₂ descargados de AirData. El propósito fue estudiar la relación entre la concentración máxima diaria de SO₂ y el valor diario del AQI, utilizando la concentración de SO₂ como variable predictora y el AQI como variable de respuesta. El análisis se realizó en Google Colab con Python y se evaluó mediante métricas de error, coeficiente de determinación, análisis de residuos y validación cruzada.

La interpretación del resultado debe considerar que el AQI de SO₂ se calcula a partir de la propia concentración del contaminante mediante puntos de corte establecidos por la EPA [3]. Por ello, la regresión se utiliza aquí principalmente como ejercicio de modelamiento y evaluación estadística, no como evidencia de una relación causal independiente.

## 2. Metodología

### 2.1. Fuente y descripción de los datos

La base de datos fue descargada desde AirData de la EPA [1], específicamente mediante el recurso de datos diarios [2]. El archivo analizado contiene **1 807 registros y 28 columnas** correspondientes al año 2022, desde el 1 de enero hasta el 31 de diciembre. Los registros proceden de cinco sitios de monitoreo y la concentración de SO₂ está expresada en partes por billón (ppb).

| Característica | Descripción |
|---|---|
| Registros | 1 807 |
| Columnas | 28 |
| Periodo | 1 de enero a 31 de diciembre de 2022 |
| Sitios de monitoreo | 5 |
| Variable predictora (X) | Daily Max SO2 Concentration |
| Variable de respuesta (y) | Daily AQI Value |
| Unidad de SO₂ | Partes por billón (ppb) |

### 2.2. Preparación y ajuste del modelo

Se realizó una exploración inicial mediante las funciones `head()`, `info()` y `describe()`. Las dos variables utilizadas en el modelo presentaron 1 807 observaciones válidas, por lo que no fue necesario eliminar registros por valores faltantes en estas columnas.

La concentración máxima diaria de SO₂ presentó una media de **2.12 ppb**, una mediana de **0.90 ppb** y un máximo de **58.70 ppb**; el AQI diario presentó una media de **2.34** y un máximo de **79**.

Los datos se dividieron en **70 % para entrenamiento y 30 % para prueba** mediante `train_test_split`, con `random_state = 101`. Esta partición produjo **1 264 observaciones de entrenamiento y 543 observaciones de prueba**.

Posteriormente se ajustó un modelo `LinearRegression` de Scikit-learn. Esta implementación corresponde a una regresión lineal por mínimos cuadrados ordinarios y estima los coeficientes minimizando la suma de los residuos cuadrados [4].

<img width="721" height="470" alt="image" src="https://github.com/user-attachments/assets/92ccd9bb-8fbc-4428-b08f-6a24e7096532" />


*Figura 1. Relación entre la concentración máxima diaria de SO₂ y el AQI.*

### 2.3. Evaluación

El desempeño del modelo se evaluó con el **error absoluto medio (MAE)**, el **error cuadrático medio (MSE)**, la **raíz del error cuadrático medio (RMSE)** y el **coeficiente de determinación (R²)**, métricas disponibles para problemas de regresión en Scikit-learn [5].

Además, se calcularon los residuos como la diferencia entre el AQI real y el AQI predicho.

Como verificación adicional se aplicó validación cruzada **K-Fold con cinco particiones**, mezcla aleatoria y `random_state = 42`. En este procedimiento, cada partición se utiliza una vez como conjunto de validación y las restantes como conjunto de entrenamiento [6].

## 3. Resultados

El modelo ajustado obtuvo un intercepto de **-0.6238** y un coeficiente de **1.3976** para la concentración máxima diaria de SO₂.

Por tanto, la ecuación estimada fue:

$$
AQI\ estimado = -0.6238 + 1.3976 \times (\text{concentración máxima diaria de SO₂})
$$

El coeficiente positivo indica que, dentro de los datos analizados, el AQI estimado aumenta conforme aumenta la concentración diaria de SO₂. Esta relación se observa también en la distribución de los puntos de la Figura 1.

### Tabla 1. Métricas obtenidas en el conjunto de prueba

| Métrica | Resultado |
|---|---:|
| MAE | 0.3545 |
| MSE | 0.1952 |
| RMSE | 0.4418 |
| R² | 0.9945 |

El **MAE de 0.3545** indica una diferencia absoluta promedio cercana a **0.35 unidades de AQI** entre las predicciones y los valores observados. El RMSE fue **0.4418**.

Por su parte, el **R² alcanzó 0.9945**, lo que muestra que el modelo reprodujo aproximadamente el **99.45 % de la variabilidad observada del AQI** en el conjunto de prueba.

<img width="662" height="371" alt="image" src="https://github.com/user-attachments/assets/2dbfaf93-c596-4226-9007-0ff734854284" />

*Figura 2. Comparación entre los valores reales y predichos de AQI.*

La comparación entre los valores reales y predichos muestra una alta proximidad respecto de la línea de igualdad, de acuerdo con el elevado R².

El análisis de residuos mostró errores de magnitud reducida alrededor de cero, aunque la distribución no debe interpretarse de manera aislada porque el AQI está directamente vinculado a la concentración utilizada como predictor.

<img width="617" height="372" alt="image" src="https://github.com/user-attachments/assets/68a96ae2-f404-4081-acb8-15854fab7ddd" />

*Figura 3. Distribución de los residuos del modelo de regresión lineal.*

### Tabla 2. Coeficiente R² en la validación cruzada de cinco particiones

| Partición | R² |
|---|---:|
| 1 | 0.9933 |
| 2 | 0.9946 |
| 3 | 0.9933 |
| 4 | 0.9953 |
| 5 | 0.9967 |
| **Promedio** | **0.9946** |
| **Desviación estándar** | **0.0013** |

Los cinco valores de R² se encontraron entre **0.9933 y 0.9967**. El promedio fue **0.9946** y la desviación estándar fue **0.0013**, lo que indica poca variación del desempeño entre las distintas particiones utilizadas en la validación cruzada.

## 4. Discusión

Los resultados muestran un ajuste muy elevado entre la concentración máxima diaria de SO₂ y el AQI. Sin embargo, este desempeño debe interpretarse a la luz de la metodología oficial de cálculo del AQI.

La EPA establece puntos de corte que convierten la concentración de cada contaminante en un valor de AQI; para SO₂, el extremo inferior del índice utiliza la concentración máxima diaria de una hora, y cuando esta concentración es inferior a **305 ppb** se aplican los puntos de corte correspondientes [3].

En la base analizada, la concentración máxima observada fue **58.7 ppb**. Por tanto, todos los registros se encuentran por debajo del umbral de 305 ppb señalado por la EPA para el uso de la concentración máxima diaria de una hora en el cálculo del AQI [3].

Esto explica en gran medida el **R² de 0.9945**: la variable de respuesta no es independiente de la variable predictora, sino que se obtiene mediante una transformación reglada de la concentración de SO₂.

Además, la conversión oficial del AQI es definida por intervalos o puntos de corte y no por una única recta para todo el rango de concentraciones [3]. En consecuencia, el modelo de regresión lineal funciona como una aproximación muy precisa dentro del rango observado, pero no debe emplearse como sustituto general de la fórmula oficial del AQI ni extrapolarse a concentraciones fuera del conjunto analizado.

Desde el punto de vista académico, el ejercicio sí permite demostrar de manera coherente las etapas de un problema de regresión: exploración de datos, selección de variables, partición en entrenamiento y prueba, ajuste por mínimos cuadrados, generación de predicciones, evaluación mediante métricas, análisis de residuos y validación cruzada.

La principal limitación es precisamente la dependencia matemática entre el predictor y la variable objetivo, por lo que futuros trabajos orientados a predicción ambiental deberían considerar un objetivo que no sea calculado directamente a partir de la misma concentración utilizada como entrada.

## 5. Referencias

[1] U.S. Environmental Protection Agency, “AirData: Air Quality Data Collected at Outdoor Monitors Across the US,” *U.S. EPA*, actualizado el 21 de julio de 2026. [En línea]. Disponible en: https://www.epa.gov/outdoor-air-quality-data. [Consulta: 18-sep-2026].

[2] U.S. Environmental Protection Agency, “Download Daily Data,” *U.S. EPA*. [En línea]. Disponible en: https://www.epa.gov/outdoor-air-quality-data/download-daily-data. [Consulta: 18-sep-2026].

[3] U.S. Environmental Protection Agency, *Technical Assistance Document for the Reporting of Daily Air Quality - the Air Quality Index (AQI)*, EPA-454/B-24-002, mayo de 2024. [En línea]. Disponible en: https://nepis.epa.gov/Exe/ZyPURL.cgi?Dockey=P101AP0Q.TXT. [Consulta: 18-sep-2026].

[4] Scikit-learn Developers, “LinearRegression,” *Scikit-learn Documentation*. [En línea]. Disponible en: https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LinearRegression.html. [Consulta: 18-sep-2026].

[5] Scikit-learn Developers, “sklearn.metrics - Regression metrics,” *Scikit-learn Documentation*. [En línea]. Disponible en: https://scikit-learn.org/stable/api/sklearn.metrics.html. [Consulta: 18-sep-2026].

[6] Scikit-learn Developers, “KFold,” *Scikit-learn Documentation*. [En línea]. Disponible en: https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.KFold.html. [Consulta: 18-sep-2026].
