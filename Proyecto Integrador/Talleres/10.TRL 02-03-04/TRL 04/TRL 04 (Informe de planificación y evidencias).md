---
_PROYECTO INTEGRADOR 2026-II_
---


# Yakutoring, Informe técnico

| **Campo** | **Información** |
|:---|----|
| Institución | Universidad Peruana Cayetano Heredia (UPCH) |
| Equipo | Equipo 09 --- Proyecto Integrador |
| Área de aplicación | Monitoreo de calidad del agua en ecosistemas de manglar de Tumbes, Perú |
| Nivel objetivo | TRL 4: validación en laboratorio mediante pruebas de baja fidelidad |
| Tipo y versión | Informe de planificación y evidencias • Borrador v1 |
| Fecha de elaboración | 1 de noviembre de 2026 |


## 1. Resumen

*YakuToring* propone medir temperatura, pH, conductividad y presión atmosférica del agua y su entorno para estimar oxígeno disuelto mediante aprendizaje profundo. Las lecturas se obtienen con sensores conectados a una *Heltec WiFi LoRa V4* y se transmiten a otra placa mediante *LoRa*. El modelo se ejecutará inicialmente en una computadora.

En esta etapa se verificará el funcionamiento del conjunto en laboratorio. La instalación en el manglar y la autonomía prolongada se evaluarán posteriormente.


## 2. Fundamento y alcance de TRL 4

Según la Directiva N.º 001-2022-CONCYTEC-P, el TRL 4 exige integrar componentes básicos y comprobarlos mediante ensayos de baja fidelidad en laboratorio \[1\]. Esta definición coincide con el material de clase de la UPCH \[2\] y la escala de NASA \[3\].

| **Indicador TRL 4** | **Evidencia que generará *YakuToring*** |
|:---|----|
| Prototipo funcional con componentes básicos integrados | Montaje de sensores, *Heltec* transmisora, enlace *LoRa*, receptor y ejecución del modelo en computadora. |
| Resultados de ensayos a nivel laboratorio | Registros fechados de sensores, paquetes *LoRa*, OD de referencia, OD estimado y errores. |
| Pruebas de baja fidelidad | Ensayo en recipientes con agua de distinta salinidad y condiciones controladas, con fotografías y procedimientos. |


## 3. Objetivos

### 3.1 Objetivo general

Comprobar en laboratorio que los sensores, el enlace LoRa y el modelo de estimación de OD funcionan como un sistema integrado.

### 3.2 Objetivos específicos

- Integrar la lectura de temperatura, pH, conductividad/salinidad derivada y presión atmosférica; registrar calibraciones y unidades.
- Verificar la comunicación entre el transmisor y el receptor *LoRa* y documentar la integridad de las mediciones recibidas.
- Conectar la recepción de los datos al modelo y generar predicciones de OD sin introducir manualmente los valores de prueba.
- Comparar estimaciones con un medidor de OD de referencia de la familia *Hach HQ* (modelo por confirmar) en mediciones emparejadas.
- Calcular indicadores de error e identificar el alcance y las limitaciones de la validación experimental.


## 4. Arquitectura experimental propuesta

### **4.1 Arquitectura electrónica**

| **Etapa** | **Componente** | **Función** |
|:---|----|----|
| 1\. Adquisición | DS18B20, sonda pH, sensor de conductividad/TDS, BME280 | Capturar temperatura, pH, conductividad y presión atmosférica. La salinidad se derivará únicamente con una conversión válida para el sensor y el rango ensayado. |
| 2\. Transmisión | Heltec WiFi LoRa V4 --- sender | Consolidar una lectura y transmitirla por LoRa a 915 MHz. |
| 3\. Recepción | Heltec WiFi LoRa V4 --- receiver | Recibir, mostrar y enviar los valores a la computadora mediante puerto serie/USB. |
| 4\. Inferencia | Computadora y modelo de Deep Learning | Aplicar preprocesamiento idéntico al de entrenamiento y producir OD estimado (mg/L). |
| 5\. Contraste | Medidor de OD Hach HQ | Obtener medición de referencia en el mismo recipiente y momento aproximado. |

<img width="986" height="230" alt="image" src="https://github.com/user-attachments/assets/7594051f-ac76-4329-bf49-0d7ab47202cb" />

## 5. Estado del desarrollo al inicio del informe

| **Elemento** | **Estado reportado** | **Brecha para la validación** |
|:---|----|----|
| LoRa entre dos Heltec V4 | Se han realizado pruebas funcionales de transmisión/recepción. | Registrar pruebas reproducibles con el paquete completo de variables. |
| DS18B20 | Lectura de temperatura demostrada. | Integración estable con los demás sensores y trazabilidad de las lecturas. |
| Pantalla OLED | Ejemplos y visualización básica funcionales. | Mostrar estado y/o lectura integrada cuando corresponda. |
| Sonda de pH | Transmisión de lectura de voltaje demostrada. | Calibrar y convertir de voltaje a pH; registrar incertidumbre. |
| Conductividad/TDS | Elemento contemplado en el diseño. | Confirmar lectura, unidades, calibración y rango para agua salobre/salada. |
| BME280 | Módulo probado individualmente en el desarrollo. | Integrar la presión atmosférica al paquete de datos. |
| Modelo de *Deep Learning* | Entrenado previamente con datos externos; R² ≈ 0,87 reportado. | Confirmar arquitectura/versión, documentar *dataset* y validar en ensayos propios. |
| PCB y estructura 3D | Diseño/fabricación o impresión aún no disponibles para prueba integrada. | No son requisito inmediato de este prototipo de laboratorio. |
| Web, base de datos y *WhatsApp* | Diseño y planificación; integración completa no acreditada. | No confundir demostraciones de interfaz con datos medidos. |


## 6. Diseño de las pruebas de baja fidelidad

### 6.1 Materiales y entorno

- *Protoboard*/cableado provisional; 2 placas *Heltec WiFi LoRa V4*; sensores DS18B20, pH, conductividad y BME280; fuente de alimentación.

- Computadora para registrar tramas y ejecutar el modelo entrenado.

- Recipientes identificados, agua dulce y mezclas de salinidad controlada; termómetro/calibradores cuando estén disponibles.

- Medidor de OD de referencia Hach HQ y su sonda compatible; verificar modelo, calibración y procedimiento del laboratorio.

### 6.2 Escenarios propuestos

| **Escenario** | **Condición** | **Propósito** | **Registro** |
|:---|----|----|----|
| E1 | Agua dulce | Comprobar el funcionamiento inicial en baja salinidad. | OD de referencia + entradas de sensores + OD estimado. |
| E2 | Agua salobre preparada | Observar la respuesta en una mezcla de salinidades. | Mismos campos, con salinidad o conductividad comprobada. |
| E3 | Agua de mayor salinidad | Evaluar el comportamiento en el extremo salino dentro del rango válido de los sensores. | Mismos campos, con anotación de condiciones y limitaciones. |

Se propone realizar 10 mediciones emparejadas por cada tipo de agua (30 en total), con fecha, hora y condiciones registradas.

### 6.3 Procedimiento de ensayo

1.  Verificar conexiones, alimentación, identificación y rangos de los sensores.
2.  Calibrar las sondas y registrar los patrones y valores utilizados.
3.  Preparar e identificar la muestra de agua y registrar sus condiciones.
4.  Registrar las lecturas recibidas por LoRa y ejecutar el modelo con esos valores.
5.  Medir el OD con el equipo Hach en el mismo recipiente y comparar ambas lecturas.
6.  Repetir las pruebas, anotar incidencias y calcular los errores de estimación.


## 7. Indicadores y criterios de análisis

Se calculará el error absoluto \|OD estimado − OD de referencia\|, el MAE, el RMSE y el porcentaje de valores con error ≤ 0,5 mg/L.

| **Indicador** | **Cómo se reportará** | **Meta/interpretación** |
|:---|----|----|
| Integración básica | Demostración observada y grabada desde sensor hasta predicción. | Funcionamiento conjunto verificable para TRL 4. |
| LoRa | Tramas enviadas, recibidas, perdidas y lectura íntegra. | Reportar tasa de recepción; criterio específico por definir. |
| Calidad de datos | Lecturas válidas, calibraciones y fallos. | Sin ocultar mediciones rechazadas o fuera de rango. |
| Error OD | Error absoluto, MAE, RMSE, sesgo y porcentaje dentro de ±0,5 mg/L. | ±0,5 mg/L es la meta indicada para el proyecto, no una exigencia genérica de CONCYTEC. |
| Reproducibilidad | Bitácora, identificación de escenario, hora y versión del modelo. | Permitir repetir el ensayo y verificar resultados. |


## 8. Plantillas de resultados (por completar)

### 8.1 Registro de mediciones emparejadas

| **ID / fecha-hora** | **Escenario** | **T (°C)** | **pH** | **Cond. / sal.** | **P atm.** | **OD Hach (mg/L)** | **OD IA (mg/L)** | **\|Error\|** |
|:---|----|----|----|----|----|----|----|----|
| M-001 / pendiente | E1 | --- | --- | --- | --- | --- | --- | --- |
| M-002 / pendiente | E1 | --- | --- | --- | --- | --- | --- | --- |
| M-003 / pendiente | E2 | --- | --- | --- | --- | --- | --- | --- |
| M-004 / pendiente | E3 | --- | --- | --- | --- | --- | --- | --- |

### 8.2 Resumen de desempeño

| **Métrica** | **Resultado** | **Observaciones** |
|:---|----|----|
| N.º de mediciones evaluadas | Pendiente | Contabilizar pares válidos y excluidos. |
| MAE (mg/L) | Pendiente | Error absoluto medio. |
| RMSE (mg/L) | Pendiente | Penaliza errores grandes. |
| Sesgo medio (mg/L) | Pendiente | Signo de subestimación o sobreestimación. |
| Porcentaje con \|error\| ≤ 0,5 mg/L | Pendiente | Comparar con la meta establecida. |
| Recepción LoRa (%) | Pendiente | Recibidos / enviados × 100. |


## 9. Matriz de evidencias para la presentación

| **Código** | **Evidencia requerida** | **Estado** |
|:---|----|----|
| EV-01 | Fotografía general del prototipo montado con sensores identificados. | Por adjuntar |
| EV-02 | Captura de lecturas simultáneas con sus unidades y calibración. | Por adjuntar |
| EV-03 | Captura emisor/receptor LoRa con trama idéntica y hora. | Por adjuntar |
| EV-04 | Captura de inferencia a partir de valores recibidos y versión del modelo. | Por adjuntar |
| EV-05 | Fotografía de la lectura del instrumento Hach durante un ensayo. | Por adjuntar |
| EV-06 | Tabla de pares de OD, errores y gráfico de contraste. | Por elaborar |
| EV-07 | Video breve que muestre el flujo de extremo a extremo sin cortes engañosos. | Por grabar |
| EV-08 | Bitácora de pruebas, calibraciones y anomalías. | Por elaborar |


## 10. Riesgos y limitaciones declaradas

- El R² obtenido con un conjunto de datos externo no demuestra la precisión del modelo en el manglar de Tumbes.
- La sonda de conductividad debe verificarse para el rango salino utilizado.
- El BME280 mide presión atmosférica y no presión del agua.
- La evaluación del modelo debe utilizar datos separados de los empleados para ajustarlo.


## 11. Conclusión provisional y próximos pasos

YakuToring podrá justificar TRL 4 cuando exista una demostración del sistema integrado y resultados de laboratorio documentados. Queda pendiente completar las lecturas conjuntas, transmitirlas por LoRa, ejecutar la inferencia y contrastar las predicciones de OD con el equipo Hach. Después se anexarán los registros y fotografías correspondientes.


# Referencias

\[1\] CONCYTEC, «Directiva N.º 001-2022-CONCYTEC-P: Uso de la metodología nivel de madurez tecnológica (TRL)», Resolución de Presidencia N.º 020-2022-CONCYTEC-P, Lima, Perú, 2022. Disponible: https://vinculate.concytec.gob.pe/wp-content/files/RP-020-2022-CONCYTEC-P.pdf

\[2\] G. Espinoza Yauri, «TRL 2, 3 y 4: Investigación aplicada», material de clase, Oficina de Transferencia Tecnológica y Vinculación Empresarial, UPCH, diapositivas 14--16, 2026.

\[3\] NASA Earth Science and Technology Office, «Technology Readiness Levels (TRLs)». Disponible: https://esto.nasa.gov/trl/ (consulta: 1 nov. 2026).
