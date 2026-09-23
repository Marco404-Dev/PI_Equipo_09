# YakuToring — Estimación del oxígeno disuelto con machine learning

## 1. ¿Qué queremos lograr?

En YakuToring queremos desarrollar un modelo que **estime cuánto oxígeno disuelto hay en el agua**, usando otras mediciones y la hora del día. El resultado se expresará en **miligramos por litro (mg/L)**.

El oxígeno disuelto, también llamado **OD**, es el oxígeno presente en el agua que utilizan muchos organismos acuáticos. Su cantidad cambia según las condiciones del ambiente. Por ejemplo, la temperatura y los procesos de fotosíntesis y respiración influyen en sus variaciones. [Fuente: USGS](https://www.usgs.gov/water-science-school/science/dissolved-oxygen-and-water).

Nuestro primer objetivo es estimar el OD **del momento de la medición**. Aunque en machine learning se utiliza la palabra “predecir”, en esta etapa no buscamos anunciar cuánto oxígeno habrá mañana. Pronosticar valores futuros sería un trabajo adicional.

## 2. ¿Por qué aplicaremos machine learning?

Queremos comprobar si un programa puede aprender relaciones entre las condiciones del agua y el oxígeno disuelto a partir de ejemplos reales.

Cada fila del dataset contiene mediciones de un momento determinado y el OD observado. Durante el entrenamiento, el modelo usará esos ejemplos para aprender. Después le presentaremos otras mediciones y compararemos su estimación con el OD real.

La idea es desarrollar un **sensor virtual**: un modelo que estime una variable a partir de otras. Esto podría apoyar el monitoreo cuando no se disponga de una medición continua de OD. Sin embargo, seguiremos necesitando un instrumento de referencia para entrenarlo y comprobar sus resultados.

No asumimos que machine learning sea automáticamente mejor que una fórmula sencilla. Lo compararemos con modelos básicos para comprobar si aporta una mejora real.

## 3. Dataset que utilizaremos

Usaremos el archivo **`data_Apalachicola Bay, FL.csv`**.

| Característica revisada | Resultado |
|---|---|
| Filas | 31 163 |
| Columnas | 10 |
| Primera fecha disponible | 1 de agosto de 2022, 00:00 EST |
| Última fecha disponible | 30 de diciembre de 2023, 18:15 EST |
| Fechas EST duplicadas | 0 |
| Celdas vacías | 0 |
| OD mínimo y máximo observados | 0,1 y 13,4 mg/L |

La ausencia de celdas vacías no demuestra que todas las mediciones sean perfectas. El archivo proviene de una selección filtrada de registros; por eso tiene huecos entre fechas y no representa una serie completa de todos los intervalos de 15 minutos.

Los datos proceden de **Apalachicola, Florida, Estados Unidos**. Las mediciones de agua corresponden a East Bay Bottom (`apaebwq`), mientras que presión y radiación PAR corresponden a la estación meteorológica East Bay (`apaebmet`). Se asociaron por fecha y hora. Son estaciones distintas y debemos considerar esa diferencia al interpretar los resultados.

Usaremos este dataset para desarrollar el primer modelo. **Sus resultados describirán el desempeño en los periodos evaluados de Apalachicola; no demostrarán todavía que funcione en Tumbes.**

## 4. ¿Cuáles son nuestras variables?

### Variables de entrada

Son los datos que el modelo utilizará para generar una estimación.

| Columna | Qué representa | Por qué la estudiaremos |
|---|---|---|
| `temperatura_agua_C` | Temperatura del agua en °C | Aporta información sobre las condiciones térmicas del agua |
| `pH` | Acidez o alcalinidad, sin unidad | Puede reflejar cambios relacionados con procesos del agua |
| `conductividad_especifica_mS_cm` | Conductividad específica en mS/cm | Aporta información relacionada con las sales disueltas |
| `presion_atmosferica_hPa` | Presión del aire en hPa | Es una de las condiciones físicas relacionadas con la solubilidad del oxígeno |
| `hora_del_dia` | Hora decimal en EST; 13,5 significa 13:30 | Permite explorar diferencias entre día y noche |
| `radiacion_PAR_mmol_m2_15min` | Luz útil para la fotosíntesis acumulada durante los 15 minutos previos, en mmol de fotones/m² | Aporta información sobre la luz disponible |
| `turbidez_FNU_NTU` | Qué tan turbia está el agua, en las unidades indicadas por la fuente | Puede aportar información sobre la claridad del agua |

La temperatura, la presión y la salinidad intervienen en la solubilidad del oxígeno; la luz y la claridad del agua influyen en la fotosíntesis. Esto justifica estudiar estas variables, pero **no asegura que todas mejoren el modelo**. [USGS: solubilidad del oxígeno](https://water.usgs.gov/water-resources/software/DOTABLES/) y [USGS: oxígeno disuelto](https://www.usgs.gov/water-science-school/science/dissolved-oxygen-and-water).

PAR no equivale a radiación solar total ni se expresa aquí en W/m². La conductividad específica tampoco debe confundirse con una lectura de conductividad sin la misma compensación de temperatura. Verificaremos que los sensores del prototipo entreguen magnitudes comparables. [Unidades de la fuente NERRS](https://nerrsdata.org/data/parameters.cfm).

### Variable objetivo

**`oxigeno_disuelto_mg_L`** es el valor que queremos estimar. Durante el entrenamiento funciona como la respuesta correcta de cada ejemplo. Cuando usemos el modelo con datos nuevos, ese valor no se entregará como entrada.

### Columnas de fecha

`fecha_hora_EST` y `fecha_hora_UTC` representan el mismo momento en dos horarios. Las usaremos para ordenar, separar y revisar los datos. No las incorporaremos automáticamente como dos entradas adicionales. La hora del día ya está representada en su propia columna.

## 5. Modelo inicial: Random Forest de regresión

Proponemos utilizar **Random Forest Regressor**. Se trata de un modelo de regresión porque queremos obtener un número, por ejemplo un OD estimado de 5,2 mg/L, y no una categoría como “vidrio” o “plástico”. Ese número es solo un ejemplo, no un resultado de entrenamiento.

Random Forest combina muchos árboles de decisión. Cada árbol hace preguntas sobre las variables y produce una estimación. El modelo promedia sus respuestas para obtener el resultado final. [Documentación de scikit-learn](https://scikit-learn.org/1.8/modules/generated/sklearn.ensemble.RandomForestRegressor.html).

Lo elegimos como primera opción porque permite estudiar relaciones que no siguen una línea recta y combinaciones entre variables. Por ejemplo, una misma temperatura puede coincidir con distintos niveles de oxígeno según la hora y las demás condiciones.

También tiene límites: puede aprender demasiado los ejemplos de entrenamiento y fallar con situaciones nuevas. Además, muchos árboles grandes pueden necesitar demasiada memoria para un ESP32. Ajustaremos su tamaño y comprobaremos su desempeño antes de decidir si será el modelo definitivo.

## 6. Objetivos que nos planteamos

**Objetivo general:** desarrollar y evaluar un modelo que estime el oxígeno disuelto a partir de mediciones ambientales, como primera etapa del sensor virtual de YakuToring.

Objetivos específicos:

1. Revisar las unidades, los rangos y la distribución de los datos, incluyendo las diferencias entre día y noche.
2. Entrenar un Random Forest y compararlo con alternativas sencillas.
3. Comprobar si añadir hora, PAR y turbidez mejora las estimaciones frente al modelo de cuatro entradas.
4. Medir el error con datos de periodos que el modelo no haya usado para aprender.
5. Revisar especialmente los errores cuando el OD medido es bajo, sin definir todavía un umbral de alerta ambiental.
6. Documentar qué variables necesita la versión elegida y si pueden medirse en el prototipo.

## 7. ¿Cómo entrenaremos y evaluaremos?

Primero ordenaremos los registros por fecha y revisaremos sus rangos y posibles problemas. Conservaremos los huecos reales: no inventaremos mediciones para completar los intervalos.

Después separaremos los datos en tres bloques de tiempo:
