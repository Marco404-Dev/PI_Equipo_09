# TRL 3. Prueba experimental de concepto

## 1. Objetivo de la prueba experimental

El objetivo de esta etapa es demostrar experimentalmente la viabilidad de los principios tecnológicos que sustentan el sistema IoT propuesto para el monitoreo de la calidad del agua y la estimación indirecta de oxígeno disuelto (OD).

Para ello, se plantea evaluar de manera preliminar el funcionamiento de los sensores fisicoquímicos, la adquisición y transmisión de datos mediante microcontroladores ESP32 y la capacidad de un modelo de *deep learning* para estimar la concentración de OD a partir de variables ambientales.

La prueba de concepto permitirá identificar las limitaciones técnicas de los componentes, comprobar la compatibilidad entre las etapas del sistema y determinar si la arquitectura propuesta puede avanzar hacia un prototipo integrado.
De acuerdo con los criterios de madurez tecnológica establecidos por NASA, el TRL 3 comprende la demostración analítica y experimental de funciones o características críticas, mediante estudios y pruebas que permitan validar las predicciones del concepto tecnológico [1].

## 2. Hipótesis tecnológica

Es posible estimar preliminarmente la concentración de oxígeno disuelto en muestras de agua mediante un modelo de *deep learning* entrenado con registros históricos de variables ambientales y alimentado con mediciones fisicoquímicas obtenidas mediante sensores integrados a un sistema IoT.

Se plantea que la integración de sensores de pH, temperatura, conductividad eléctrica y presión atmosférica permitirá obtener información ambiental útil para el desarrollo del modelo predictivo. Asimismo, la comparación de las estimaciones con mediciones de referencia permitirá evaluar su desempeño en muestras procedentes de los Pantanos de Villa.

## 3. Metodología de validación experimental

La prueba de concepto se desarrollará mediante tres etapas principales:

### 3.1. Validación de la adquisición de variables fisicoquímicas

Se realizarán pruebas individuales de los sensores adquiridos para comprobar su funcionamiento y la obtención de mediciones correspondientes a las variables consideradas en el diseño conceptual:

- pH del agua.
- Temperatura del agua.
- Conductividad eléctrica.
- Presión atmosférica.

Los sensores serán conectados a un microcontrolador ESP32, encargado de recopilar las mediciones y generar registros digitales.

Se evaluará la estabilidad de las lecturas, la continuidad de adquisición de datos y la correspondencia entre las mediciones obtenidas y los valores de referencia disponibles para cada variable.

Esta etapa permitirá identificar posibles errores de medición, problemas de calibración e incompatibilidades entre los sensores y el sistema electrónico.

### 3.2. Desarrollo y evaluación preliminar del modelo de *deep learning*

Se desarrollará un modelo de aprendizaje profundo para estimar la concentración de oxígeno disuelto utilizando registros históricos de calidad del agua y variables ambientales.

Para el entrenamiento inicial se contempla utilizar información de NOAA NERRS, debido a la disponibilidad de registros ambientales que pueden servir como base para establecer relaciones entre las variables de entrada y la concentración de OD.

El procedimiento comprenderá las siguientes actividades:

1. **Recopilación de datos:** identificación y descarga de registros históricos que contengan mediciones de oxígeno disuelto y variables fisicoquímicas compatibles con las disponibles en el sistema.
2. **Preprocesamiento:** revisión de datos faltantes, valores atípicos, unidades de medida y consistencia temporal de los registros.
3. **Selección de variables:** identificación de las variables de entrada que presenten disponibilidad y relevancia para la estimación del OD.
4. **Entrenamiento:** desarrollo de un modelo de *deep learning* que permita establecer relaciones entre las variables ambientales y la concentración de oxígeno disuelto.
5. **Validación:** evaluación del modelo utilizando datos que no hayan sido empleados durante el entrenamiento.
6. **Evaluación del desempeño:** comparación entre los valores estimados y los valores reales de OD mediante métricas estadísticas.

La utilización de modelos de aprendizaje profundo para estimar el oxígeno disuelto cuenta con antecedentes científicos en sistemas acuáticos. Zhi et al. [2] demostraron la aplicación de redes neuronales recurrentes LSTM para predecir la concentración de OD a escala continental, utilizando información hidrometeorológica y de calidad del agua. Asimismo, Xu et al. [3] desarrollaron un modelo híbrido WT-DSE-LSTM para la predicción multivariable de OD. Estos trabajos respaldan la aplicación de arquitecturas de aprendizaje profundo al problema planteado, aunque la selección del modelo definitivo deberá responder a las características del conjunto de datos disponible.
El programa System-Wide Monitoring Program de NOAA NERRS proporciona registros estandarizados de parámetros ambientales y de calidad del agua, incluyendo temperatura, salinidad, pH, oxígeno disuelto y presión barométrica [4]. La disponibilidad de estas variables permite considerar esta fuente para el entrenamiento inicial, previa evaluación de la compatibilidad entre sus registros y las variables medidas por los sensores del proyecto
Se considerarán las siguientes métricas para evaluar el modelo:

- **MAE (Mean Absolute Error):** permite determinar el error absoluto promedio entre las concentraciones estimadas y las observadas.
- **RMSE (Root Mean Squared Error):** permite evaluar la magnitud de los errores, otorgando mayor penalización a las desviaciones elevadas.
- **Coeficiente de determinación (R²):** permite evaluar qué proporción de la variabilidad de los valores observados es explicada por el modelo.

La utilización conjunta de MAE y RMSE permite analizar diferentes características de los errores de predicción. Mientras que el MAE representa el error absoluto promedio, el RMSE otorga mayor influencia a los errores de mayor magnitud [5], [6]. Por tanto, ambas métricas proporcionarán información complementaria sobre el comportamiento del modelo.

La selección de la arquitectura definitiva dependerá de la disponibilidad, estructura y cantidad de registros históricos. Asimismo, se deberá comprobar que las variables utilizadas durante el entrenamiento sean compatibles con las mediciones que proporcionará el sistema físico.

### 3.3. Validación con muestras de agua de los Pantanos de Villa

La medición de oxígeno disuelto requiere especial atención debido a que su concentración puede variar durante la recolección y manipulación de las muestras. El USGS establece procedimientos específicos para su medición, calibración instrumental y control de calidad [7]. Asimismo, señala que parámetros como el oxígeno disuelto, el pH y la temperatura pueden modificarse después de la recolección, por lo que las mediciones deben realizarse lo más cerca posible del momento y lugar de muestreo [8].
Se contempla realizar una evaluación experimental con muestras de agua recolectadas en los Pantanos de Villa, en Lima, Perú.

Las muestras serán caracterizadas mediante los sensores disponibles para obtener mediciones de pH, temperatura y conductividad eléctrica. Paralelamente, se determinará la concentración de oxígeno disuelto mediante un instrumento de referencia Hach en laboratorio.

Los valores obtenidos permitirán comparar las estimaciones generadas por el modelo con las mediciones de referencia y analizar su comportamiento frente a muestras de un ecosistema diferente de aquellos utilizados para el entrenamiento inicial.

Se deberá controlar el tiempo transcurrido entre la recolección, el transporte y la medición de las muestras, debido a que la manipulación puede modificar la concentración de oxígeno disuelto.

Esta etapa permitirá identificar diferencias entre los registros históricos utilizados para el entrenamiento y las condiciones fisicoquímicas de las muestras locales.

## 4. Prueba de integración del sistema IoT

Una vez comprobado el funcionamiento individual de los sensores, se evaluará la integración preliminar de los componentes electrónicos y de comunicación.

La prueba comprenderá los siguientes elementos:

- **Adquisición:** conexión de los sensores fisicoquímicos al ESP32 para recopilar las mediciones.
- **Transmisión:** comunicación entre la boya y la estación terrestre mediante módulos LoRa.
- **Recepción:** utilización de un segundo ESP32 como Gateway para recibir los registros transmitidos.
- **Almacenamiento:** evaluación de la transferencia de información hacia una plataforma en la nube, considerando AWS como alternativa.
- **Procesamiento:** integración conceptual de los registros con el modelo de estimación de OD.
- **Visualización:** evaluación preliminar de la presentación de las mediciones y estimaciones mediante una aplicación móvil.

También se analizarán los requerimientos energéticos de los componentes para evaluar la viabilidad de la alternativa de alimentación mediante batería y panel solar.

La integración completa de las notificaciones mediante WhatsApp y la autonomía energética de la boya podrán abordarse en etapas posteriores del desarrollo.

## 5. Resultados esperados

A partir de las pruebas experimentales se espera obtener:

1. Registros digitales de las variables fisicoquímicas obtenidas mediante los sensores disponibles.
2. Evidencia del funcionamiento de la comunicación inalámbrica entre la boya y la estación terrestre mediante LoRa.
3. Un primer modelo de *deep learning* entrenado con registros históricos y capaz de generar estimaciones de concentración de oxígeno disuelto.
4. Resultados de evaluación del modelo mediante MAE, RMSE y R².
5. Una comparación preliminar entre las estimaciones del modelo y las mediciones de OD obtenidas mediante el instrumento Hach en muestras de los Pantanos de Villa.
6. Identificación de las principales limitaciones relacionadas con la adquisición de datos, la transmisión inalámbrica, el procesamiento y la variabilidad ambiental.

Estos resultados permitirán determinar si los principios tecnológicos propuestos cuentan con evidencia experimental suficiente para continuar hacia el desarrollo de un prototipo integrado.

## 6. Limitaciones y consideraciones técnicas

Durante esta etapa deberán considerarse las siguientes limitaciones:

- **Generalización del modelo:** los registros históricos de NOAA NERRS pueden presentar características ambientales diferentes de las condiciones de los Pantanos de Villa. Por ello, el desempeño del modelo deberá evaluarse con datos locales.
- **Disponibilidad de variables:** la selección definitiva de las variables de entrada dependerá de su disponibilidad en los registros históricos y de su correspondencia con los sensores físicos.
- **Variabilidad del oxígeno disuelto:** la concentración de OD puede modificarse por factores ambientales y biológicos que no necesariamente estarán representados en las variables utilizadas por el modelo.
- **Mediciones de referencia:** el transporte y la manipulación de las muestras pueden alterar su concentración de OD, afectando la comparación experimental.
- **Comunicación inalámbrica:** el alcance y la estabilidad de la transmisión LoRa deberán evaluarse considerando las condiciones del entorno.
- **Alimentación energética:** será necesario determinar el consumo eléctrico del sistema y la capacidad de generación y almacenamiento de energía para establecer su autonomía.

En consecuencia, las estimaciones del modelo deberán interpretarse como resultados de un sensor virtual y no como mediciones directas de oxígeno disuelto.

## 7. Criterios de evaluación de la prueba de concepto

La demostración experimental se considerará satisfactoria si se obtiene evidencia verificable de los siguientes aspectos:

| Componente | Criterio de evaluación |
|---|---|
| Sensores fisicoquímicos | Obtención de mediciones estables y coherentes con valores de referencia. |
| Adquisición de datos | Registro digital de las variables mediante el ESP32. |
| Comunicación LoRa | Transmisión y recepción satisfactoria de los datos entre ambas estaciones. |
| Modelo de *deep learning* | Generación de estimaciones de OD a partir de las variables de entrada. |
| Validación estadística | Obtención de métricas de error y evaluación del desempeño predictivo. |
| Validación experimental | Comparación de las estimaciones con mediciones de referencia Hach. |
| Integración preliminar | Compatibilidad funcional entre las etapas de adquisición, transmisión y procesamiento. |

Los valores de aceptación cuantitativos deberán establecerse a partir de los resultados de calibración, las especificaciones de los sensores y los requerimientos de precisión del sistema.

## 8. Conclusión

La prueba experimental de concepto permitirá evaluar la viabilidad de los principios tecnológicos que sustentan el sistema IoT propuesto, particularmente la adquisición de variables fisicoquímicas, su transmisión inalámbrica y la estimación indirecta de oxígeno disuelto mediante técnicas de aprendizaje profundo.

La combinación de registros históricos de NOAA NERRS con mediciones experimentales de muestras de los Pantanos de Villa permitirá estudiar la capacidad de generalización del modelo y reconocer las diferencias entre las condiciones ambientales de entrenamiento y las del ecosistema de aplicación.

La evidencia obtenida durante esta etapa constituirá la base para determinar la factibilidad de integrar los componentes en un prototipo funcional y avanzar hacia los siguientes niveles de madurez tecnológica.

## 9. Referencias bibliográficas

[1] NASA, “Technology Readiness Levels,” NASA Science and Technology, Sep. 27, 2023. [En línea]. Disponible en: https://www.nasa.gov/directorates/somd/space-communications-navigation-program/technology-readiness-levels/

[2] W. Zhi, D. Feng, W.-P. Tsai, G. Sterle, A. Harpold, C. Shen y L. Li, “From hydrometeorology to river water quality: Can a deep learning model predict dissolved oxygen at the continental scale?,” *Environmental Science & Technology*, vol. 55, no. 4, pp. 2357–2368, 2021, doi: 10.1021/acs.est.0c06783.

[3] X. Xu, C. Guo, P. Wan, H. Xu, Y. Yu y J. Fan, “WT-DSE-LSTM: A hybrid model for the multivariate prediction of dissolved oxygen,” *Alexandria Engineering Journal*, vol. 124, pp. 285–296, 2025, doi: 10.1016/j.aej.2025.03.075.

[4] NOAA Office for Coastal Management, “National Estuarine Research Reserve System-Wide Monitoring Program Data,” NOAA. [En línea]. Disponible en: https://www.coast.noaa.gov/digitalcoast/data/nerr.html

[5] C. J. Willmott y K. Matsuura, “Advantages of the mean absolute error (MAE) over the root mean square error (RMSE) in assessing average model performance,” *Climate Research*, vol. 30, pp. 79–82, 2005, doi: 10.3354/cr030079.

[6] T. Chai y R. R. Draxler, “Root mean square error (RMSE) or mean absolute error (MAE)? – Arguments against avoiding RMSE in the literature,” *Geoscientific Model Development*, vol. 7, pp. 1247–1250, 2014, doi: 10.5194/gmd-7-1247-2014.

[7] F. D. Wilde, “Chapter A6.2. Dissolved oxygen,” en *National Field Manual for the Collection of Water-Quality Data*, U.S. Geological Survey, 2020. [En línea]. Disponible en: https://doi.org/10.3133/tm9A6.2

[8] U.S. Geological Survey, “Preparing for a Sampling Run,” *National Field Manual for the Collection of Water-Quality Data*. [En línea]. Disponible en: https://pubs.usgs.gov/of/2000/of00-213/manual_eng/prepare.html
