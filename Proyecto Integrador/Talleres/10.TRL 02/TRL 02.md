# TRL 2. Formulación del concepto tecnológico

## 1. Descripción general de la propuesta

El proyecto propone desarrollar un sistema IoT para el monitoreo de la calidad del agua en ecosistemas acuáticos, inicialmente concebido para manglares y adaptable a humedales costeros con características ambientales similares. Para la adquisición de muestras y la evaluación experimental se considera como área de estudio los Pantanos de Villa, en Lima, Perú.

La propuesta busca estimar indirectamente la concentración de oxígeno disuelto (OD) mediante un modelo de *deep learning*, denominado sensor virtual, que utilizará información de variables fisicoquímicas y ambientales recopiladas por sensores (pH, conductividad eléctrica, temperatura y presión atmosférica). De esta manera, se plantea complementar el monitoreo convencional con una alternativa de estimación y visualización continua de la información.

## 2. Sustento científico y tecnológico

La propuesta se fundamenta en la relación entre las condiciones fisicoquímicas del agua y la concentración de oxígeno disuelto. Variables como la temperatura, el pH y la conductividad eléctrica han sido utilizadas en investigaciones para desarrollar modelos predictivos de OD.

Valizadeh Moghadam et al. [1] desarrollaron un modelo de red neuronal recurrente profunda para predecir la concentración de oxígeno disuelto en un río, empleando variables como temperatura, conductividad específica, caudal y pH. Por otro lado, Hadjisolomou et al. [2] aplicaron redes neuronales artificiales para estimar el OD en aguas costeras, considerando variables como temperatura, salinidad y pH. Asimismo, Lin et al. [3] estudiaron diferentes modelos de aprendizaje automático, incluidos modelos LSTM, para estimar la concentración de OD en ecosistemas lacustres.

Estos antecedentes respaldan la posibilidad de utilizar técnicas de aprendizaje automático para estimar el oxígeno disuelto a partir de variables ambientales. Sin embargo, sus resultados no pueden extrapolarse directamente a los Pantanos de Villa, por lo que será necesario recopilar datos y evaluar el desempeño del modelo en el entorno de estudio.

En cuanto al monitoreo mediante dispositivos IoT, Blanco-Gómez et al. [4] desarrollaron un sistema de bajo costo integrado en una boya para medir conductividad eléctrica y temperatura, demostrando la aplicación de sensores multiparamétricos en plataformas flotantes. Este antecedente permite sustentar la viabilidad conceptual de integrar sensores y componentes electrónicos en una estructura de monitoreo acuático.

## 3. Arquitectura conceptual del sistema

La solución tecnológica contempla dos estaciones comunicadas mediante tecnología LoRa:

### 3.1. Boya de monitoreo

Consiste en una estructura de geometría circular que incorpora los sensores adquiridos para medir:

- pH.
- Temperatura del agua.
- Conductividad eléctrica.
- Presión atmosférica.

Los sensores estarán conectados a un microcontrolador ESP32, encargado de recopilar las mediciones y transmitirlas mediante un módulo de comunicación LoRa. La estructura física considera un cuerpo flotante y una sección inferior destinada a alojar o sostener los componentes que estarán en contacto con el agua.

### 3.2. Estación en tierra

Contará con un segundo ESP32 y un módulo LoRa, cuya función será recibir los datos transmitidos desde la boya y permitir su envío hacia la plataforma digital.

**Figura 1.** Estación de adquisición y Gateway para monitoreo de calidad del agua. Fuente: adaptado de [5].

<img width="208" height="52" alt="image" src="https://github.com/user-attachments/assets/c3ea1199-dec8-407f-aeb2-b6b74390860f" />

## 4. Procesamiento y estimación de oxígeno disuelto

El sistema contempla el desarrollo de un modelo de aprendizaje profundo que será entrenado previamente en una computadora utilizando registros de datos. Una vez entrenado, el modelo se utilizará para estimar la concentración de OD a partir de las variables recopiladas por la boya.

La información recibida en la estación terrestre formará parte del flujo de datos destinado a la estimación y posterior visualización. Se contempla utilizar AWS para almacenar las mediciones y los valores estimados de OD, además de una aplicación móvil para consultar los resultados. También se plantea integrar un mecanismo de notificaciones mediante WhatsApp para comunicar posibles situaciones de interés.

La ubicación definitiva del procesamiento del modelo dentro de esta arquitectura deberá precisarse durante el desarrollo del sistema.

## 5. Alimentación energética

Se contempla una alternativa de alimentación mediante pila y panel solar. La configuración definitiva deberá considerar la compatibilidad entre ambos elementos, los requerimientos energéticos de los componentes y la autonomía necesaria para el funcionamiento de la boya.

## 6. Antecedentes tecnológicos y análisis preliminar de patentes

Además de la revisión de investigaciones científicas, se consideran antecedentes de propiedad industrial relacionados con el monitoreo multiparamétrico del agua y el uso de sensores virtuales. La revisión permite identificar soluciones tecnológicas existentes y reconocer aspectos similares o diferenciadores respecto a la propuesta.

Entre los antecedentes identificados se encuentran:

### 6.1. Sistema IoT multiparamétrico y monoparamétrico para el monitoreo de la calidad del agua (CO2022004253A1)

Describe un sistema que integra sensores de variables como turbidez, conductividad eléctrica, temperatura y pH. También contempla módulos alimentados mediante paneles solares y baterías, transmisión de datos a través de una puerta de enlace y almacenamiento en la nube [6].

Este antecedente guarda relación con la arquitectura de monitoreo y transmisión de datos propuesta.

### 6.2. Virtual Sensor Performance Monitoring Device and Method (US20260072716A1)

Presenta un sistema de sensor virtual basado en redes neuronales artificiales que utiliza información ambiental de instalaciones acuícolas para predecir la concentración de oxígeno disuelto [7].

Este documento constituye un antecedente especialmente relacionado con el componente de aprendizaje profundo del proyecto.

La revisión de estos documentos permite reconocer que existen desarrollos previos tanto en sistemas IoT para el monitoreo de calidad del agua como en modelos de estimación virtual de oxígeno disuelto. Por ello, será necesario analizar las características técnicas, el alcance de las reivindicaciones y las diferencias entre dichas soluciones y la propuesta desarrollada.

## 7. Referencias bibliográficas

**Formato IEEE:**

[1] S. V. Moghadam, A. Sharafati, H. Feizi, S. M. S. Marjaie, S. B. H. S. Asadollah, and D. Motta, “An efficient strategy for predicting river dissolved oxygen concentration: Application of deep recurrent neural network model,” *Environmental Monitoring and Assessment*, vol. 193, no. 12, Art. no. 798, 2021, doi: 10.1007/s10661-021-09586-x.

[2] E. Hadjisolomou et al., “Predicting coastal dissolved oxygen values with the use of artificial neural networks: A case study for Cyprus,” *IOP Conference Series: Earth and Environmental Science*, vol. 1123, Art. no. 012083, 2022, doi: 10.1088/1755-1315/1123/1/012083.

[3] S. Lin, D. C. Pierson, R. Ladwig, B. M. Kraemer, and F. R. S. Hu, “Multi-model machine learning approach accurately predicts lake dissolved oxygen with multiple environmental inputs,” *Earth and Space Science*, vol. 11, no. 7, Art. no. e2023EA003473, 2024, doi: 10.1029/2023EA003473.

[4] P. Blanco-Gómez, J. L. Jiménez-García, and J. M. Cecilia, “Low-cost automated GPS, electrical conductivity and temperature sensing device (EC + T Track) and Android platform for water quality monitoring campaigns,” *HardwareX*, vol. 13, Art. no. e00381, 2023, doi: 10.1016/j.ohx.2022.e00381.

[5] “Project EEL,” *Hackster.io*, Jun. 1, 2021. [En línea]. Disponible en: Project EEL – Hackster.io.

[6] “Multi-parameter and single-parameter IoT system for water quality monitoring,” Patente CO2022004253A1, publicada el 29 de abril de 2022. [En línea]. Disponible en: Google Patents – CO2022004253A1.

[7] H. J. Shin, H. Park, J. Y. Jung, and S. K. Jo, “Virtual sensor performance monitoring device and method,” Patente US20260072716A1, publicada el 12 de marzo de 2026. [En línea]. Disponible en: Google Patents – US20260072716A1.
