# 1. Diseño funcional del sistema 

ManglarLab propone un sistema de monitoreo de la condición del agua en manglares mediante la adquisición de temperatura, pH y conductividad eléctrica. A partir de estas mediciones, se plantea procesar y almacenar información, estimar el oxígeno disuelto mediante un modelo de aprendizaje automático y presentar indicadores que apoyen la identificación de posibles condiciones de riesgo.

Esta sección describe el sistema mediante tres herramientas de diseño: la caja negra, el esquema de funciones y la matriz morfológica. En conjunto, permiten establecer sus entradas y salidas, descomponer su funcionamiento y organizar las alternativas tecnológicas para el desarrollo del prototipo.

> **Estado del diseño:** propuesta funcional y selección tecnológica inicial. Los diagramas contienen decisiones que deben unificarse antes de definir la arquitectura final. La estimación de oxígeno disuelto es una función propuesta cuya precisión deberá comprobarse experimentalmente.

## 1.1. Caja negra del sistema

La caja negra representa a ManglarLab desde su interacción con el entorno, sin detallar los componentes internos. Su función global consiste en transformar energía y señales de entrada en información útil para el seguimiento de la condición del agua.

![Caja negra de ManglarLab](https://github.com/Marco404-Dev/PI_Equipo_09/blob/main/Proyecto%20Integrador/Talleres/caja%20negra.png?raw=true)

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




### 1.3.4. Configuración de los caminos de solución

Para desarrollar la comparación ponderada se toma la selección verde de la matriz como **Camino A** y se proponen dos configuraciones adicionales: **Camino B**, orientado a una prueba local, y **Camino C**, orientado a comunicación de campo mediante red celular.

> **Evaluación preliminar propuesta:** los caminos B y C, los pesos y las calificaciones siguientes se plantean para discusión del equipo. No corresponden a resultados experimentales, cotizaciones ni a tres caminos ya aprobados en la matriz. Las puntuaciones permiten mostrar el procedimiento de selección y deberán actualizarse con evidencia del prototipo.

| Función | Camino A: selección inicial | Camino B: prueba local propuesta | Camino C: comunicación de campo propuesta |
|---|---|---|---|
| Energizar | Panel solar | Batería recargable con recarga externa | Panel solar |
| Almacenar energía | Baterías de litio | Batería de litio recargable, compartida con la función anterior | Baterías de litio |
| Regular voltaje | Módulo de alimentación | Módulo de alimentación | Módulo de alimentación |
| Medir temperatura | DS18B20 | DS18B20 | DS18B20 |
| Medir pH | Electrodo de vidrio | Electrodo de vidrio | Electrodo de vidrio |
| Medir conductividad | Sensor de conductividad eléctrica | Sensor de conductividad eléctrica | Sensor de conductividad eléctrica |
| Procesar datos | ESP32 | ESP32 | ESP32 |
| Estimar oxígeno disuelto | ML con temperatura, pH y conductividad | Mismo enfoque de ML | Mismo enfoque de ML |
| Cuantificar confiabilidad | Intervalo de predicción | Intervalo de predicción | Intervalo de predicción |
| Evaluar condición del agua | Rangos y variación temporal | Rangos y variación temporal | Rangos y variación temporal |
| Comunicar datos | Wi-Fi | Wi-Fi en una red local | GSM/4G mediante módulo adicional |
| Almacenar datos | AWS / nube | PostgreSQL en un equipo local | AWS / nube |
| Visualizar información | Aplicación Android | Streamlit local | Aplicación Android |
| Notificar riesgos | Indicador en dashboard | Indicador en dashboard | Notificación web/app |

*Tabla 4. Configuraciones utilizadas en la evaluación preliminar. Las alternativas se combinan por función; no se equiparan automáticamente con las columnas CS1, CS2 y CS3.*

En B se requiere un equipo local para ejecutar PostgreSQL y Streamlit. En C se requiere un módulo celular y un servicio de datos. Estos recursos deben incluirse en el presupuesto. Los tres caminos mantienen la misma cadena de medición y el mismo enfoque predictivo para comparar principalmente alimentación, comunicación e implementación.

### 1.3.5. Criterios, pesos y valoración de los caminos

Los pesos representan la importancia relativa de cada criterio para el proyecto y suman **100 %**. Cada camino recibe una calificación de 1 a 5; una calificación mayor siempre representa una condición más favorable. Por ello, menor costo y menor dificultad de integración reciben puntuaciones mayores.

| Puntaje | Interpretación |
|---|---|
| 1 | Muy desfavorable |
| 2 | Desfavorable |
| 3 | Aceptable |
| 4 | Bueno |
| 5 | Muy bueno |

| Criterio | Peso propuesto | Justificación de su importancia |
|---|---:|---|
| Calidad de medición y validación de la estimación | 25 % | Las decisiones dependen de lecturas calibradas y de una estimación contrastada con mediciones de referencia. |
| Autonomía energética | 20 % | Se busca sostener el monitoreo y reducir intervenciones para recarga. |
| Conectividad en el lugar de uso | 15 % | Determina la posibilidad de consultar datos y recibir información a distancia. |
| Costo total del prototipo | 15 % | Considera sensores, alimentación, comunicaciones, equipo auxiliar y servicios durante un mismo período de comparación. |
| Facilidad de integración | 10 % | Considera el esfuerzo de montaje, programación, configuración y puesta en funcionamiento. |
| Acceso e historial de datos | 10 % | Considera la disponibilidad del historial y la consulta fuera del equipo local. |
| Visualización y avisos | 5 % | Considera la facilidad de consulta y la forma de presentar cambios al usuario. |
| **Total** | **100 %** | |

*Tabla 5. Criterios y ponderaciones propuestos para ManglarLab.*

#### Valoración preliminar

| Criterio | Camino A | Camino B | Camino C |
|---|---:|---:|---:|
| Calidad de medición y validación de la estimación | 3 | 3 | 3 |
| Autonomía energética | 4 | 2 | 3 |
| Conectividad en el lugar de uso | 2 | 2 | 4 |
| Costo total del prototipo | 3 | 4 | 2 |
| Facilidad de integración | 3 | 4 | 2 |
| Acceso e historial de datos | 4 | 3 | 4 |
| Visualización y avisos | 4 | 3 | 4 |

*Tabla 6. Calificaciones de trabajo, sujetas a confirmación. El valor 3 en medición es una asignación neutral para la comparación, no una declaración de precisión aceptable demostrada.*

Las calificaciones se basan en los siguientes supuestos explícitos:

- **Medición:** se asigna el mismo valor a los tres caminos porque comparten sensores y enfoque de estimación. No existe evidencia aquí para atribuir mayor precisión a alguno.
- **Autonomía:** se supone que A dispone de un sistema solar correctamente dimensionado. B depende de recargas externas. Para C se supone una mayor demanda por transmisión celular sin aumentar inicialmente el almacenamiento energético. Estos supuestos deben comprobarse con un balance de energía.
- **Conectividad:** se supone que el sitio no dispone de Wi-Fi permanente, pero sí de cobertura celular utilizable. Si no se confirma esta condición, la ventaja asignada a C deja de estar sustentada.
- **Costo:** se supone que B reutiliza un equipo local disponible y evita el sistema solar y los servicios remotos; C incorpora módulo celular y servicio de datos. Sin esta disponibilidad o sin cotizaciones, la comparación puede cambiar.
- **Integración:** se supone que el equipo puede desarrollar una prueba local con menor esfuerzo que integrar nube y aplicación móvil; C añade la integración celular.
- **Historial:** se valora favorablemente la consulta remota prevista en A y C. No se presume que almacenar en la nube garantice por sí solo respaldo o ausencia de pérdidas.
- **Visualización:** se asigna una valoración favorable a la consulta móvil de A y C. No se atribuye una ventaja adicional a las notificaciones de C hasta definir y probar su funcionamiento.

### 1.3.6. Evaluación ponderada y selección preliminar

La evaluación ponderada combina el peso de cada criterio con la calificación asignada a cada camino. Para cada fila se calcula:

**Puntaje ponderado = (peso porcentual / 100) × calificación del camino.**

La suma de los resultados proporciona un puntaje global de hasta **5 puntos**. Por ejemplo, el aporte de autonomía energética para A es **0,20 × 4 = 0,80 puntos**.

| Criterio | Peso | A | B | C | Peso × A | Peso × B | Peso × C |
|---|---:|---:|---:|---:|---:|---:|---:|
| Calidad de medición y validación de la estimación | 25 % | 3 | 3 | 3 | 0,75 | 0,75 | 0,75 |
| Autonomía energética | 20 % | 4 | 2 | 3 | 0,80 | 0,40 | 0,60 |
| Conectividad en el lugar de uso | 15 % | 2 | 2 | 4 | 0,30 | 0,30 | 0,60 |
| Costo total del prototipo | 15 % | 3 | 4 | 2 | 0,45 | 0,60 | 0,30 |
| Facilidad de integración | 10 % | 3 | 4 | 2 | 0,30 | 0,40 | 0,20 |
| Acceso e historial de datos | 10 % | 4 | 3 | 4 | 0,40 | 0,30 | 0,40 |
| Visualización y avisos | 5 % | 4 | 3 | 4 | 0,20 | 0,15 | 0,20 |
| **Total ponderado** | **100 %** | | | | **3,20** | **2,90** | **3,05** |

*Tabla 7. Evaluación ponderada preliminar de los caminos de solución.*

| Camino | Puntaje final | Posición |
|---|---:|---:|
| **A — Selección inicial** | **3,20 / 5** | **1** |
| C — Comunicación de campo | 3,05 / 5 | 2 |
| B — Prueba local | 2,90 / 5 | 3 |

Bajo los pesos y supuestos propuestos, el **Camino A obtiene el mayor puntaje y se conserva como candidato inicial para desarrollar el prototipo**. Su ventaja resulta de la valoración asignada a autonomía, costo e integración, frente a la conectividad prevista en C.

La diferencia entre A y C es de **0,15 puntos**, por lo que la selección no es concluyente. Si el peso de conectividad aumenta de 15 % a 20 % y el de costo disminuye de 15 % a 10 %, ambos caminos obtienen **3,15 puntos**. Esto muestra que la prioridad de comunicación en campo puede modificar la decisión.

Además, un requisito obligatorio no debe compensarse con una buena puntuación en otros criterios: si la transmisión remota es indispensable y no existe Wi-Fi ni un enlace adicional viable, A no cumple ese requisito aunque alcance el mayor total. La selección final deberá realizarse después de confirmar cobertura, presupuesto energético, costos y desempeño de medición.

## 1.4. Decisiones pendientes de unificación

No se asignan puntajes en este documento porque las figuras revisadas no contienen evidencia suficiente para sustentarlos.
Los apartados 2.3.4 a 2.3.6 presentan una propuesta de caminos y una evaluación preliminar con supuestos explícitos. Antes de aprobar la selección final, el equipo deberá confirmar las configuraciones y reemplazar las calificaciones de trabajo por valoraciones sustentadas en pruebas, cotizaciones y requisitos del lugar de uso.
