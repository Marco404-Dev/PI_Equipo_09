# TRL 2. Formulación del concepto tecnológico

## 1. Descripción general de la propuesta

El proyecto propone desarrollar un sistema IoT para el monitoreo de la calidad del agua en ecosistemas acuáticos, inicialmente concebido para manglares y adaptable a humedales costeros con características ambientales similares. Para la adquisición de muestras y la evaluación experimental se considera como área de estudio los Pantanos de Villa, en Lima, Perú.

La propuesta busca estimar indirectamente la concentración de oxígeno disuelto (OD) mediante un modelo de aprendizaje profundo, denominado sensor virtual, que utilizará información de variables fisicoquímicas y ambientales recopiladas por sensores (pH, conductividad eléctrica, temperatura y presión atmosférica). De esta manera, se plantea complementar el monitoreo convencional con una alternativa de estimación y visualización continua de la información.

## 2. Sustento científico y tecnológico

La propuesta se fundamenta en la relación entre las condiciones fisicoquímicas del agua y la concentración de oxígeno disuelto. Variables como la temperatura, el pH y la conductividad eléctrica han sido utilizadas en investigaciones para desarrollar modelos predictivos de OD.

Valizadeh Moghadam et al. [1] desarrollaron un modelo de red neuronal recurrente profunda para predecir la concentración de oxígeno disuelto en un río, empleando variables como temperatura, conductividad específica, caudal y pH. Por otro lado, Hadjisolomou et al. [2] aplicaron redes neuronales artificiales para estimar el OD en aguas costeras, considerando variables como temperatura, salinidad y pH. Asimismo, Lin et al. [3] estudiaron diferentes modelos de aprendizaje automático, incluidos modelos LSTM, para estimar la concentración de OD en ecosistemas lacustres.

Estos antecedentes respaldan la posibilidad de utilizar técnicas de aprendizaje automático para estimar el oxígeno disuelto a partir de variables ambientales. Sin embargo, sus resultados no pueden extrapolarse directamente a los Pantanos de Villa, por lo que será necesario recopilar datos y evaluar el desempeño del modelo en el entorno de estudio.

En cuanto al monitoreo mediante dispositivos IoT, Blanco-Gómez et al. [4] desarrollaron un sistema de bajo costo integrado en una boya para medir conductividad eléctrica y temperatura, demostrando la aplicación de sensores multiparamétricos en plataformas flotantes. Este antecedente permite sustentar la viabilidad conceptual de integrar sensores y componentes electrónicos en una estructura de monitoreo acuático.

## 3. Análisis funcional y formulación del concepto tecnológico

### 3.1. Caja negra del sistema

El análisis funcional mediante la caja negra permite identificar las principales entradas y salidas del sistema, sin profundizar todavía en el funcionamiento interno de cada componente. Se consideran como entradas la energía eléctrica, las acciones de encendido y apagado, y las muestras de agua del entorno. Como salidas se contemplan las mediciones procesadas, la estimación de oxígeno disuelto y las alertas o notificaciones generadas a partir de la información recopilada.

<p align="center">
  <img src="https://github.com/user-attachments/assets/6c32908d-8eb5-4d32-86c1-fea8d096d5f4" width="650">
</p>

<p align="center">
  **Figura 1. Caja negra del sistema YakuToring.**
</p>

### 3.2. Matriz morfológica y selección de alternativas

La matriz morfológica permite identificar distintas alternativas para cumplir las funciones principales del sistema, considerando aspectos como la adquisición de datos, el procesamiento, la comunicación, la alimentación energética y la estructura física. A partir de las opciones planteadas, se seleccionaron las alternativas que conforman el concepto tecnológico propuesto, buscando integrar los componentes en un sistema de monitoreo funcional.

<p align="center">
  <img src="https://github.com/user-attachments/assets/abfcba42-3ab4-46b9-8077-a357fb85b7fb" width="650">
</p>

<p align="center">
  **Figura 2. Matriz morfológica y selección de alternativas del sistema.**
</p>

## 4. Diseño conceptual del sistema

### 4.1. Bocetos iniciales

Se elaboraron bocetos preliminares para explorar distintas configuraciones de la boya, considerando su geometría, distribución de componentes y disposición de los sensores. Estos diseños sirvieron como referencia para definir la estructura general del dispositivo y orientar el posterior modelado tridimensional.

<p align="center">
  <img src="https://github.com/user-attachments/assets/f9a404be-0aaa-4dae-8e39-b0f910220881" width="300">
  <img src="https://github.com/user-attachments/assets/98fc5416-c04b-4f9a-854b-953cbc7f51b1" width="300">
</p>

<p align="center">
  **Figura 3 y 4. Bocetos preliminares de la estructura de la boya.**
</p>

### 4.2. Modelo tridimensional

Se desarrolló un modelo tridimensional de la boya mediante el software Onshape, con el propósito de representar su geometría y visualizar la distribución de los espacios destinados a los componentes electrónicos y sensores. Este diseño constituye una referencia para la futura fabricación de la estructura y permite evaluar preliminarmente su organización física.

<p align="center">
  <img src="https://github.com/user-attachments/assets/d1167050-7863-4e87-9d5e-5d5c392036bd" width="450">
</p>

<p align="center">
  **Figura 5. Modelo tridimensional conceptual de la boya desarrollado en Onshape.**
</p>

### 4.3. Diseño de la placa electrónica (PCB)

Se elaboró un diseño preliminar de la placa electrónica (PCB) para organizar las conexiones entre el microcontrolador, los sensores y los demás componentes del sistema. El diseño contempla la distribución de los elementos y las conexiones necesarias para su integración, y se presenta mediante su representación esquemática, bidimensional y tridimensional.

#### 4.3.1. Esquemático

<p align="center">
  <img src="https://github.com/user-attachments/assets/cf62504f-114d-44ee-90a8-c8ba58e476d2" width="650">
</p>

<p align="center">
  **Figura 6. Esquemático del circuito electrónico propuesto.**
</p>

#### 4.3.2. Diseño 2D

<p align="center">
  <img src="https://github.com/user-attachments/assets/f97872e7-8144-4518-b649-cc531ce1d542" width="450">
</p>

<p align="center">
  **Figura 7. Distribución bidimensional de los componentes de la PCB.**
</p>

#### 4.3.3. Diseño 3D

<p align="center">
  <img src="https://github.com/user-attachments/assets/8e2f895a-b6b9-4487-8453-e9d909d46e17" width="450">
</p>

<p align="center">
  **Figura 8. Representación tridimensional de la PCB.**
</p>

## 5. Arquitectura conceptual del sistema

### 5.1. Esquemático general del sistema

La arquitectura conceptual del sistema se representa mediante un esquema funcional que muestra la distribución de sus principales componentes y la relación entre las etapas de adquisición, transmisión, procesamiento y visualización de los datos. Se consideran dos estaciones comunicadas mediante tecnología LoRa: una boya de monitoreo y una estación terrestre, vinculadas con una plataforma digital para el almacenamiento y consulta de la información.

<p align="center">
  <img src="https://github.com/user-attachments/assets/a1a6bf46-09bb-4162-9661-20e042b3668f" width="700">
</p>

<p align="center">
  **Figura 9. Esquemático general de la arquitectura del sistema YakuToring.**
</p>

### 5.2. Boya de monitoreo

Consiste en una estructura de geometría circular que incorpora los sensores adquiridos para medir:

- pH.
- Temperatura del agua.
- Conductividad eléctrica.
- Presión atmosférica.

Los sensores estarán conectados a un microcontrolador ESP32, encargado de recopilar las mediciones y transmitirlas mediante un módulo de comunicación LoRa. La estructura física considera un cuerpo flotante y una sección inferior destinada a alojar o sostener los componentes que estarán en contacto con el agua.

### 5.3. Estación en tierra

Contará con un segundo ESP32 y un módulo LoRa, cuya función será recibir los datos transmitidos desde la boya y permitir su envío hacia la plataforma digital.

<p align="center">
  <img src="https://github.com/user-attachments/assets/db3f1d79-a7e6-4d00-b3d1-2d7e051aa67f" width="600">
</p>

<p align="center">
  **Figura 10. Estación de adquisición y Gateway para monitoreo de calidad del agua.**
</p>

Fuente: Adaptado de [5].

### 5.4. Procesamiento y comunicación de datos

El flujo de información contempla la adquisición de las variables mediante los sensores instalados en la boya y su transmisión hacia la estación terrestre a través de LoRa. Posteriormente, los datos serán enviados a una plataforma digital para su almacenamiento y procesamiento. A partir de las variables recopiladas, se realizará la estimación del oxígeno disuelto mediante el modelo de aprendizaje profundo, cuyos resultados podrán visualizarse en la aplicación y utilizarse para generar notificaciones al usuario.

<p align="center">
  <img src="https://github.com/user-attachments/assets/e9fe87cd-6bb3-4b7f-9e21-1ee6766afa0a" width="750">
</p>

<p align="center">
  **Figura 11. Flujo conceptual de procesamiento y comunicación de datos del sistema.**
</p>

## 6. Diseño conceptual de la aplicación e interacción con el usuario

Se plantea una aplicación móvil que permitirá al usuario consultar la información recopilada por el sistema de monitoreo. El flujo de interacción contempla el acceso a la plataforma, la visualización de las variables fisicoquímicas medidas, la consulta de las estimaciones de oxígeno disuelto y la revisión de notificaciones sobre posibles situaciones de interés.

### 6.1. Diagrama de flujo de navegación del usuario

Los diagramas representan las principales etapas de navegación e interacción previstas para la aplicación, desde el ingreso del usuario hasta la consulta de los datos y las notificaciones generadas por el sistema.

<p align="center">
  <img src="https://github.com/user-attachments/assets/b08218ae-92a1-4f47-a070-6b2118bc4b27" width="350">
  <img src="https://github.com/user-attachments/assets/b97aa8bb-034d-445a-a5cb-3cad2c8a475d" width="350">
</p>

<p align="center">
  **Figura 12 y 13. Diagramas conceptuales de navegación e interacción del usuario con la aplicación.**
</p>

## 7. Procesamiento y estimación de oxígeno disuelto

El sistema contempla el desarrollo de un modelo de aprendizaje profundo que será entrenado previamente en una computadora utilizando registros de datos. Una vez entrenado, el modelo se utilizará para estimar la concentración de OD a partir de las variables recopiladas por la boya.

La información recibida en la estación terrestre formará parte del flujo de datos destinado a la estimación y posterior visualización. Se contempla utilizar AWS para almacenar las mediciones y los valores estimados de OD, además de una aplicación móvil para consultar los resultados. También se plantea integrar un mecanismo de notificaciones mediante WhatsApp para comunicar posibles situaciones de interés.

La ubicación definitiva del procesamiento del modelo dentro de esta arquitectura deberá precisarse durante el desarrollo del sistema.

## 8. Alimentación energética

Se contempla una alternativa de alimentación mediante batería recargable y panel solar. La configuración definitiva deberá considerar la compatibilidad entre ambos elementos, los requerimientos energéticos de los componentes y la autonomía necesaria para el funcionamiento de la boya.

## 9. Antecedentes tecnológicos y análisis preliminar de patentes

Además de la revisión de investigaciones científicas, se consideran antecedentes de propiedad industrial relacionados con el monitoreo multiparamétrico del agua y el uso de sensores virtuales. La revisión permite identificar soluciones tecnológicas existentes y reconocer aspectos similares o diferenciadores respecto a la propuesta.

Entre los antecedentes identificados se encuentran:

### 9.1. Sistema IoT multiparamétrico y monoparamétrico para el monitoreo de la calidad del agua (CO2022004253A1)

Describe un sistema que integra sensores de variables como turbidez, conductividad eléctrica, temperatura y pH. También contempla módulos alimentados mediante paneles solares y baterías, transmisión de datos a través de una puerta de enlace y almacenamiento en la nube [6].

Este antecedente guarda relación con la arquitectura de monitoreo y transmisión de datos propuesta.

### 9.2. Dispositivo y método de monitorización del rendimiento de sensores virtuales (US20260072716A1)

Presenta un sistema de sensor virtual basado en redes neuronales artificiales que utiliza información ambiental de instalaciones acuícolas para predecir la concentración de oxígeno disuelto [7].

Este documento constituye un antecedente especialmente relacionado con el componente de aprendizaje profundo del proyecto.

La revisión de estos documentos permite reconocer que existen desarrollos previos tanto en sistemas IoT para el monitoreo de calidad del agua como en modelos de estimación virtual de oxígeno disuelto. Por ello, será necesario analizar las características técnicas, el alcance de las reclamaciones y las diferencias entre dichas soluciones y la propuesta desarrollada.

## 10. Referencias bibliográficas

[1] SV Moghadam, A. Sharafati, H. Feizi, SMS Marjaie, SBHS Asadollah y D. Motta, “Una estrategia eficiente para predecir la concentración de oxígeno disuelto en ríos: Aplicación de un modelo de red neuronal recurrente profunda”, *Environmental Monitoring and Assessment*, vol. 193, n.º 12, art. n.º 798, 2021, doi: 10.1007/s10661-021-09586-x.

[2] E. Hadjisolomou et al., “Predicción de valores de oxígeno disuelto costero con el uso de redes neuronales artificiales: un estudio de caso para Chipre”, *IOP Conference Series: Earth and Environmental Science*, vol. 1123, art. n.º 012083, 2022, doi: 10.1088/1755-1315/1123/1/012083.

[3] S. Lin, D. C. Pierson, R. Ladwig, B. M. Kraemer y F. R. S. Hu, “Un enfoque de aprendizaje automático multimodelo predice con precisión el oxígeno disuelto en lagos con múltiples entradas ambientales”, *Earth and Space Science*, vol. 11, n.º 7, art. n.º e2023EA003473, 2024, doi: 10.1029/2023EA003473.

[4] P. Blanco-Gómez, J. L. Jiménez-García y J. M. Cecilia, “Dispositivo automatizado de bajo costo para GPS, conductividad eléctrica y detección de temperatura (EC + T Track) y plataforma Android para campañas de monitoreo de la calidad del agua”, *HardwareX*, vol. 13, art. n.º e00381, 2023, doi: 10.1016/j.ohx.2022.e00381.

[5] “Project EEL”, *Hackster.io*, 1 de junio de 2021. [En línea]. Disponible en: Proyecto EEL – Hackster.io.

[6] “Sistema IoT multiparamétrico y monoparamétrico para monitoreo de la calidad del agua”, Patente CO2022004253A1, publicada el 29 de abril de 2022. [En línea]. Disponible en: Patentes de Google – CO2022004253A1.

[7] H. J. Shin, H. Park, J. Y. Jung y S. K. Jo, “Dispositivo y método de monitoreo del rendimiento del sensor virtual”, Patente US20260072716A1, publicada el 12 de marzo de 2026. [En línea]. Disponible en: Patentes de Google – US20260072716A1.
