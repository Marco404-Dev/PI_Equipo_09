# 1. Diseño funcional del sistema — ManglarLab

ManglarLab propone un sistema de monitoreo de la condición del agua en manglares mediante la adquisición de temperatura, pH y conductividad eléctrica. A partir de estas mediciones, se plantea procesar y almacenar información, estimar el oxígeno disuelto mediante un modelo de aprendizaje automático y presentar indicadores que apoyen la identificación de posibles condiciones de riesgo.

Esta sección describe el sistema mediante tres herramientas de diseño: la caja negra, el esquema de funciones y la matriz morfológica. En conjunto, permiten establecer sus entradas y salidas, descomponer su funcionamiento y organizar las alternativas tecnológicas para el desarrollo del prototipo.

> **Estado del diseño:** propuesta funcional y selección tecnológica inicial. Los diagramas contienen decisiones que deben unificarse antes de definir la arquitectura final. La estimación de oxígeno disuelto es una función propuesta cuya precisión deberá comprobarse experimentalmente.

## 1.1. Caja negra del sistema

La caja negra representa a ManglarLab desde su interacción con el entorno, sin detallar los componentes internos. Su función global consiste en transformar energía y señales de entrada en información útil para el seguimiento de la condición del agua.

![Caja negra de ManglarLab](https://github.com/Marco404-Dev/PI_Equipo_09/blob/main/Proyecto%20Integrador/Talleres/Caja%20negra.png?raw=true)

*Figura 1. Caja negra del sistema ManglarLab. Fuente: repositorio del Equipo 09.*

### 1.1.1. Entradas

| Tipo | Entrada representada | Descripción funcional |
|---|---|---|
| Energía | Energía eléctrica | Permite alimentar los módulos de adquisición, procesamiento y comunicación. |
| Señal | Temperatura del agua | Proporciona información sobre el estado térmico del medio monitoreado. |
| Señal | pH del agua | Proporciona información sobre su acidez o alcalinidad. |
| Señal | Conductividad eléctrica del agua | Proporciona información sobre su capacidad de conducir corriente eléctrica. |
| Control | Encendido y apagado | Permite habilitar o detener el funcionamiento del equipo. |

### 1.1.2. Salidas

La figura presenta gráficas e historial de mediciones, una medición procesada de temperatura, alertas por WhatsApp y ubicación GPS. Estas salidas describen la intención de entregar información al usuario y asociarla con el lugar de monitoreo.

Para mantener correspondencia con el resto del diseño, se propone actualizar la figura e incluir explícitamente las mediciones procesadas de **temperatura, pH y conductividad**, así como el **oxígeno disuelto estimado y su incertidumbre**. El canal de alertas y la incorporación de geolocalización deben confirmarse al unificar la arquitectura.

### 1.1.3. Límite del sistema

La representación actual considera las señales de los sensores como entradas. Si el límite del sistema incluye también los sensores, las entradas pueden expresarse como las magnitudes físicas del agua que se desea medir. Esta convención deberá mantenerse en todos los diagramas.

El alcance descrito corresponde al monitoreo y análisis del agua; los diagramas revisados no representan una función de tratamiento ni de modificación de sus condiciones.

## 1.2. Esquema de funciones

El esquema de funciones descompone la función global en operaciones relacionadas entre sí. El diagrama organiza estas operaciones en un dominio de control y un dominio electrónico, conectando la alimentación, la adquisición de señales, el procesamiento, el almacenamiento y la presentación de resultados.

![Esquema de funciones de ManglarLab](https://github.com/Marco404-Dev/PI_Equipo_09/blob/main/Proyecto%20Integrador/Talleres/Esquema%20de%20funciones.jpeg?raw=true)

*Figura 2. Esquema de funciones del sistema ManglarLab. Fuente: repositorio del Equipo 09.*

### 1.2.1. Dominio electrónico

Este dominio reúne las funciones que permiten alimentar el sistema y convertir las señales de los sensores en datos utilizables:

- **Gestionar energía:** almacenar energía, controlar la carga de la batería y acondicionar la alimentación de los módulos.
- **Indicar el estado de operación:** mostrar visualmente el encendido o apagado del equipo.
- **Adquirir señales:** leer sensores, filtrar señales, realizar la conversión analógico-digital cuando corresponda y medir el voltaje de la batería.
- **Almacenar información localmente:** guardar registros en microSD e identificar datos pendientes de transmisión.
- **Comunicar y geolocalizar:** obtener posición GNSS, fecha y hora, y transmitir información mediante una conexión celular 4G, según la propuesta del esquema.

### 1.2.2. Dominio de control

Este dominio organiza el tratamiento de los datos y su conversión en información para el usuario:

| Función | Descripción |
|---|---|
| Procesar mediciones | Adquirir lecturas y aplicar la calibración correspondiente. |
| Gestionar datos | Guardar registros y sincronizar información pendiente. |
| Comunicar con la nube | Recibir datos mediante una API, autenticar el dispositivo y almacenar información en una base de datos. El esquema menciona Flask como tecnología propuesta. |
| Estimar oxígeno disuelto | Ejecutar un modelo de aprendizaje automático y registrar la incertidumbre de sus resultados. |
| Analizar estados | Evaluar la condición fisicoquímica del agua e identificar posibles riesgos, fallas de sensores o batería baja. |
| Informar al usuario | Presentar mediciones, estimaciones, gráficas, historial y avisos conforme al canal que se defina. |

### 1.2.3. Secuencia funcional propuesta

**Alimentar el sistema → adquirir señales → procesar y calibrar lecturas → almacenar registros → transmitir y sincronizar datos → estimar oxígeno disuelto → evaluar condiciones → presentar información.**

Esta secuencia resume el flujo lógico. La distribución del procesamiento entre el dispositivo y la nube deberá precisarse durante la integración.

La matriz propone utilizar temperatura, pH y conductividad como entradas del modelo de estimación. El bloque correspondiente del esquema menciona temperatura y conductividad, por lo que se deberá unificar la lista de variables. Asimismo, la expresión «modelo ML validado» representa un requisito para su uso; el diagrama por sí solo no constituye evidencia de validación.

## 1.3. Matriz morfológica

La matriz morfológica organiza distintas alternativas tecnológicas para ejecutar las funciones de ManglarLab. Permite comparar opciones y construir configuraciones completas mediante la elección de una alternativa por función.

![Matriz morfológica de ManglarLab](https://github.com/Marco404-Dev/PI_Equipo_09/blob/main/Proyecto%20Integrador/Talleres/Matriz%20morfologica.png?raw=true)

*Figura 3. Matriz morfológica y selección inicial del sistema ManglarLab. Los indicadores verdes identifican las opciones seleccionadas inicialmente. Fuente: repositorio del Equipo 09.*

### 1.3.1. Funciones y selección inicial

La matriz comprende **14 funciones**. La siguiente tabla transcribe las opciones marcadas en verde:

| Código | Función | Alternativa seleccionada inicialmente |
|---|---|---|
| F01 | Energizar | Panel solar |
| F02 | Almacenar energía | Baterías de litio |
| F03 | Regular o adaptar voltaje | Módulo de alimentación |
| F04 | Medir temperatura | DS18B20 |
| F05 | Medir pH | Electrodo de pH de vidrio, potenciométrico |
