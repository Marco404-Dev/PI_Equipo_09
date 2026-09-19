# Análisis estadístico y regresión lineal de datos de dióxido de nitrógeno (NO₂)

## 1. Introducción
La calidad del aire constituye un aspecto importante para la evaluación de las condiciones ambientales, debido a la presencia de contaminantes que pueden afectar tanto al ambiente como a la salud de la población. Entre estos contaminantes se encuentra el dióxido de nitrógeno (NO₂), un gas asociado principalmente a procesos de combustión y que forma parte de los contaminantes atmosféricos monitoreados mediante sistemas de vigilancia de la calidad del aire.
Para el presente análisis se utilizaron datos obtenidos de **AirData**, plataforma de la Agencia de Protección Ambiental de Estados Unidos (U.S. Environmental Protection Agency, EPA), que proporciona información de calidad del aire recopilada mediante estaciones de monitoreo ambiental. Los datos de AirData proceden principalmente del **Air Quality System (AQS)** y permiten consultar información horaria, diaria y anual sobre concentraciones de contaminantes y valores del índice de calidad del aire (AQI) [1], [2].
El objetivo del presente trabajo fue realizar un análisis exploratorio de datos de NO₂ y desarrollar un modelo de **regresión lineal** para analizar la relación entre la concentración máxima diaria de NO₂ y el valor diario del AQI. Para ello se emplearon herramientas de Python, principalmente las bibliotecas Pandas, Seaborn, Matplotlib y Scikit-learn.
El conjunto analizado contiene **357 registros diarios** correspondientes al monitoreo de NO₂ en el sitio identificado como **150030010**, ubicado en Kapolei. La concentración máxima diaria de NO₂ presenta una media de **9.039 ppb**, mientras que el valor diario del AQI presenta una media de **8.199**.

## 2. Metodología
### 2.1. Obtención y preparación de los datos
Los datos fueron obtenidos de la plataforma **AirData de la U.S. EPA**, específicamente mediante los datos diarios de calidad del aire. AirData permite descargar estadísticas diarias de calidad del aire correspondientes a contaminantes criterio y asociadas a estaciones de monitoreo específicas [1].
El archivo utilizado contiene **28 variables y 357 observaciones**. Entre las variables principales se encuentran:

* Fecha (`Date`).
* Identificación de la estación (`Site ID`).
* Concentración máxima diaria de NO₂ (`Daily Max NO2 Concentration`).
* Unidades de concentración (`Units`).
* Valor diario del AQI (`Daily AQI Value`).
* Número de observaciones diarias (`Daily Obs Count`).
* Porcentaje de datos completos (`Percent Complete`).
* Coordenadas geográficas.
* Elevación.
* Altura de la sonda.
* Información relacionada con el método y la estación de monitoreo.

La variable `Daily Max NO2 Concentration` se encuentra expresada en **partes por mil millones (ppb)**. Los registros corresponden al mismo sitio de monitoreo, con una latitud de aproximadamente **21.324°** y longitud de **−158.089°**.
Para la exploración inicial se empleó la función `info()` de Pandas con la finalidad de identificar el número de registros, las variables disponibles, sus tipos de datos y la presencia de valores nulos. También se empleó `describe()` para obtener medidas estadísticas descriptivas.

### 2.2. Análisis descriptivo
Se calcularon estadísticas descriptivas para las variables numéricas. Para la concentración máxima diaria de NO₂ se obtuvo:

* Número de observaciones: **357**
* Media: **9.039 ppb**
* Desviación estándar: **5.131 ppb**
* Mínimo: **2.0 ppb**
* Primer cuartil: **5.4 ppb**
* Mediana: **7.6 ppb**
* Tercer cuartil: **11.2 ppb**
* Máximo: **34.3 ppb**

Para el AQI diario:

* Número de observaciones: **357**
* Media: **8.199**
* Desviación estándar: **4.721**
* Mínimo: **2**
* Primer cuartil: **5**
* Mediana: **7**
* Tercer cuartil: **10**
* Máximo: **32**

También se elaboró un diagrama de caja y bigotes para observar la distribución de la concentración de NO₂ y del AQI e identificar posibles valores alejados de la distribución central.

<img width="543" height="413" alt="image" src="https://github.com/user-attachments/assets/81eb3398-8fba-48d9-ac39-ca8a20fe9e5e" />


### 2.3. Modelo de regresión lineal

Se utilizó un modelo de **regresión lineal simple**, tomando como variable independiente:
X = Daily Max NO2 Concentration
y como variable dependiente:
Y = Daily AQI Value
Los datos fueron divididos en un conjunto de entrenamiento y uno de prueba utilizando `train_test_split`, con un **30 % de los datos destinado a prueba** y un `random_state = 42`, lo que permite reproducir la misma división de los datos [3].
Posteriormente, se utilizó el algoritmo `LinearRegression` de Scikit-learn para ajustar el modelo. Finalmente, se generaron predicciones sobre el conjunto de prueba.
La evaluación se realizó mediante dos métricas de regresión:

* **Coeficiente de determinación (R²)**.
* **Error cuadrático medio (MSE)**.

Estas métricas son apropiadas para evaluar modelos de regresión; R² representa la proporción de variabilidad de la variable dependiente explicada por el modelo, mientras que MSE cuantifica el error cuadrático promedio entre los valores observados y predichos [4], [5].

## 3. Resultados
### 3.1. Análisis descriptivo
El conjunto de datos presentó 357 observaciones y 28 variables. La información del archivo mostró que las variables principales de concentración y AQI no presentan valores faltantes.
La concentración máxima diaria de NO₂ tuvo un valor promedio de **9.039 ppb**, con valores comprendidos entre **2.0 y 34.3 ppb**. La mediana fue de **7.6 ppb**, lo que indica que la mitad de las observaciones presentó concentraciones iguales o inferiores a este valor.
Por otro lado, el AQI diario presentó una media de **8.199** y una mediana de **7**, con valores entre **2 y 32**.
El 50 % central de las observaciones de concentración de NO₂ se encontró entre **5.4 y 11.2 ppb**, mientras que para el AQI este intervalo estuvo entre **5 y 10**.

<img width="562" height="455" alt="image" src="https://github.com/user-attachments/assets/2e11f167-1880-4999-acd7-6ac9cd7a1199" />

### 3.2. Regresión lineal
El modelo desarrollado utilizó la concentración máxima diaria de NO₂ como variable predictora del AQI diario.
Los resultados obtenidos fueron:

| Métrica |   Resultado |
| ------- | ----------: |
| R²      | **0.99447** |
| MSE     | **0.15050** |

El valor de **R² = 0.99447** indica que aproximadamente el **99.45 % de la variabilidad observada en el AQI del conjunto de prueba es explicada por el modelo utilizando la concentración máxima diaria de NO₂ como variable predictora**.
El valor de **MSE = 0.15050** representa el error cuadrático medio de las predicciones. Debido a que el MSE se expresa en unidades cuadráticas de la variable dependiente, su magnitud debe interpretarse considerando la escala del AQI.
La representación gráfica de la regresión muestra los valores observados de concentración y la línea de tendencia obtenida mediante el modelo lineal.

## 4. Discusión
Los resultados obtenidos muestran una relación lineal muy elevada entre la concentración máxima diaria de NO₂ y el valor diario del AQI dentro del conjunto de datos analizado. El coeficiente R² obtenido, de **0.99447**, indica que el modelo reproduce con un ajuste muy elevado la variación del AQI en los datos de prueba.
Sin embargo, este resultado debe interpretarse con precaución. El AQI no constituye una variable completamente independiente de la concentración de contaminantes. La EPA señala que el AQI se calcula a partir de las concentraciones de contaminantes y que, para cada contaminante medido, se calcula un índice; el valor máximo de esos índices determina el AQI correspondiente [6]. Por esta razón, la elevada asociación observada entre la concentración de NO₂ y el AQI es coherente con la forma en que se construye este índice.
En los datos analizados, además, el AQI presenta valores que aumentan conforme aumenta la concentración de NO₂. Esto permite que la regresión lineal produzca un ajuste elevado. Por tanto, el resultado no debe interpretarse como evidencia de que la concentración de NO₂ sea la única causa de las variaciones en la calidad del aire, sino como una relación estadística dentro de este conjunto de datos y entre estas dos variables.
El análisis descriptivo mostró una concentración media de **9.039 ppb**, mientras que el máximo registrado fue de **34.3 ppb**. La diferencia entre estos valores evidencia que existe variabilidad en las concentraciones registradas durante el periodo estudiado. Asimismo, el diagrama de caja permite identificar la dispersión y posibles observaciones alejadas de la distribución central.
Otro aspecto importante es que los datos corresponden a **un único sitio de monitoreo**, identificado como Site ID 150030010. Por ello, los resultados describen las observaciones de este monitor y no deben generalizarse automáticamente a otras estaciones, ciudades o regiones.
Además, la metodología empleada utiliza una división aleatoria de los datos en entrenamiento y prueba. Debido a que las observaciones corresponden a fechas sucesivas, una alternativa metodológica para estudios temporales podría consistir en separar los datos cronológicamente, utilizando las primeras observaciones para entrenamiento y las posteriores para evaluación. Esto permitiría estudiar con mayor claridad la capacidad del modelo para realizar predicciones sobre periodos futuros.
En conjunto, el modelo desarrollado demuestra una relación estadística muy fuerte entre las dos variables seleccionadas, aunque su interpretación debe considerar que el AQI se encuentra directamente relacionado con las concentraciones de contaminantes y que el análisis se limita a un sitio de monitoreo específico.

## 5. Referencias

[1] U.S. Environmental Protection Agency, “AirData: Air Quality Data Collected at Outdoor Monitors Across the US,” EPA, 2026. [En línea]. Disponible en: https://www.epa.gov/outdoor-air-quality-data.
