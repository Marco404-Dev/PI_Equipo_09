
# *ESTADO DEL ARTE*

## 1. Estimación del oxígeno disuelto mediante inteligencia artificial

El oxígeno disuelto (OD) es un parámetro importante para evaluar la calidad del agua, debido a su relación con los procesos biológicos y fisicoquímicos de los ecosistemas acuáticos. Su concentración depende de diversos factores ambientales, entre ellos la temperatura, las condiciones hidrológicas y la actividad biológica. Aunque existen instrumentos específicos para medirlo, su costo puede limitar la implementación de sistemas de monitoreo de bajo presupuesto. Ante esta situación, diferentes investigaciones han explorado el uso de modelos computacionales capaces de estimar su concentración a partir de otras variables ambientales.

Zhi et al. [1] estudiaron la capacidad de las redes neuronales recurrentes de tipo *Long Short-Term Memory* (LSTM) para predecir el OD en diferentes cuencas hidrográficas de Estados Unidos. Su investigación utilizó datos de calidad del agua e información hidrometeorológica para analizar si los modelos podían aprender las dinámicas del oxígeno disuelto a distintas escalas espaciales. Este trabajo constituye un antecedente relevante para el uso de datos ambientales históricos en el desarrollo de modelos predictivos. Sin embargo, su aplicación en otros ecosistemas requiere evaluar la capacidad de generalización del modelo.

Posteriormente, Azma et al. [2] propusieron modelos híbridos que combinan redes neuronales artificiales con algoritmos de optimización para predecir la concentración diaria de OD. Los autores emplearon registros históricos de calidad del agua y compararon el desempeño de diferentes configuraciones. Sus resultados mostraron que la optimización de las redes neuronales puede mejorar el desempeño predictivo y permitir la obtención de una expresión matemática aproximada del modelo. Este antecedente demuestra que existen alternativas basadas en aprendizaje automático para estimar el oxígeno disuelto sin depender exclusivamente de una medición directa durante cada predicción.

Rocha et al. [3] investigaron modelos de *deep learning* basados en grafos y arquitecturas Transformer para pronosticar el OD en sistemas fluviales. Su trabajo considera las relaciones espaciales y temporales presentes en los datos, destacando la importancia de representar adecuadamente la estructura de los sistemas acuáticos. No obstante, la utilidad de estas arquitecturas depende de la disponibilidad de información compatible con el tipo de modelo y de la definición del problema predictivo.

Más recientemente, Xu et al. [4] propusieron el modelo híbrido WT-DSE-LSTM para predecir la concentración de OD mediante la combinación de transformada wavelet, mecanismos de ponderación de características y redes LSTM. La propuesta busca representar las fluctuaciones temporales y las relaciones entre distintas variables. Este estudio evidencia la evolución de los modelos de predicción hacia arquitecturas híbridas; sin embargo, una mayor complejidad computacional no garantiza necesariamente mejores resultados en todos los conjuntos de datos.

Por su parte, Sadler et al. [5] evaluaron métodos de *deep learning* guiados por procesos físicos para predecir concentraciones de OD en ríos. La investigación destaca una limitación de los modelos puramente basados en datos: pueden identificar asociaciones estadísticas sin representar explícitamente los procesos ambientales que intervienen en la dinámica del oxígeno disuelto. Este antecedente refuerza la necesidad de evaluar los modelos con datos independientes y de comprobar su comportamiento en condiciones diferentes de las utilizadas durante el entrenamiento.

En conjunto, estas investigaciones muestran que el uso de redes neuronales y otros métodos de aprendizaje automático constituye una línea activa de investigación para la estimación del oxígeno disuelto. También evidencian que la selección de variables, la calidad de los datos y la validación del modelo son factores determinantes para evaluar su utilidad.

## 2. Sensores virtuales para el monitoreo de la calidad del agua

Un sensor virtual es un modelo computacional que estima una variable a partir de otras mediciones disponibles. En el monitoreo ambiental, este enfoque permite explorar la estimación de parámetros que requieren instrumentación específica mediante modelos entrenados con datos históricos.

Para el caso del OD, un sensor virtual puede utilizar variables como temperatura, pH y conductividad eléctrica o salinidad para producir una estimación de su concentración. Su implementación puede integrarse con sensores físicos, unidades de procesamiento y plataformas de visualización, de modo que las mediciones disponibles alimenten el modelo y sus resultados se presenten junto con los datos ambientales registrados.

No obstante, la estimación indirecta presenta limitaciones. La relación entre las variables de entrada y el OD puede variar entre ecosistemas, estaciones y condiciones ambientales. Por ello, un modelo entrenado con registros de una región no necesariamente conservará el mismo desempeño cuando se aplique a otro lugar. Además, la estimación computacional debe distinguirse de una medición directa y evaluarse mediante métricas de error apropiadas.


## Referencias:

[1] W. Zhi, D. Feng, W.-P. Tsai, G. Sterle, A. Harpold, C. Shen y L. Li, “From hydrometeorology to river water quality: Can a deep learning model predict dissolved oxygen at the continental scale?,” Environmental Science & Technology, vol. 55, no. 4, pp. 2357–2368, 2021, doi: 10.1021/acs.est.0c06783.

[2] A. Azma, Y. Liu, M. Azma, M. Saadat, D. Zhang, J. Cho y S. Rezania, “Hybrid machine learning models for prediction of daily dissolved oxygen,” Journal of Water Process Engineering, vol. 55, art. no. 103957, 2023, doi: 10.1016/j.jwpe.2023.103957.

[3] P. A. C. Rocha, V. O. Santos, J. V. Griensven Thé y B. Gharabaghi, “New graph-based and transformer deep learning models for river dissolved oxygen forecasting,” Environments, vol. 10, no. 12, art. no. 217, 2023, doi: 10.3390/environments10120217.

[4] X. Xu, C. Guo, P. Wan, H. Xu, Y. Yu y J. Fan, “WT-DSE-LSTM: A hybrid model for the multivariate prediction of dissolved oxygen,” Alexandria Engineering Journal, vol. 124, pp. 285–296, 2025, doi: 10.1016/j.aej.2025.03.075.

[5] B. Sadler et al., “Evaluating a process-guided deep learning approach for predicting dissolved oxygen in streams,” Hydrological Processes, vol. 38, no. 9, art. no. e15270, 2024, doi: 10.1002/hyp.15270.
