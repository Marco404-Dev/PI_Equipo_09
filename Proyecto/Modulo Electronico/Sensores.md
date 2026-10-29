# Fichas de sensores — YakuToring

**Equipo 09 · 29/10/2026 · Documento técnico preliminar**

**Objetivo:** dejar registrada la función, el estado real, las pruebas necesarias y la información que aún falta de cada sensor. Este documento **no** asigna pines definitivos ni reemplaza hojas de datos de los módulos concretos.

| Sensor | Variable | Interfaz prevista | Situación |
|---|---|---|---|
| DS18B20 | Temperatura del agua (°C) | Digital 1-Wire | Lectura individual reportada |
| Módulo de pH | pH del agua | Analógica mediante placa acondicionadora | Señal preliminar comprobada; calibración pendiente |
| Módulo TDS | Señal relacionada con sólidos disueltos | Analógica mediante placa acondicionadora | Identificación/calibración pendientes |
| BME280 | Presión atmosférica (hPa); datos auxiliares | I²C | Detección previa de módulo reportada |
| Flotador P45 | Estado del contacto/nivel discreto | Entrada digital | Apertura/cierre probados antes en otro ESP32 |
| INA219 | Corriente y tensión para ensayos | I²C | Considerado; no integrado |

## 1. DS18B20 — temperatura del agua

**Función.** Medir la temperatura del agua para contextualizar otras variables y alimentar, en una futura etapa, la estimación de OD. El integrado DS18B20 se comunica por 1-Wire y su hoja de datos declara exactitud de ±0,5 °C entre −10 y +85 °C, **especificación del chip que no demuestra la exactitud del conjunto sonda/montaje** [1].

**Estado.** Se ha reportado lectura individual correcta. El cableado usado en pruebas antiguas del ESP32 DevKit no se toma como distribución final de la Heltec V4.

**Por documentar y verificar:**

1. Fotografía de la sonda, origen, impermeabilización y longitud de cable.
2. Tensión de alimentación y resistencia *pull-up* según el circuito y la hoja de datos [1].
3. Cinco lecturas consecutivas y su dispersión; tiempos de respuesta al cambiar de agua.
4. Comparación con termómetro de referencia y registro de la diferencia a distintas temperaturas [2].
5. Tratamiento de lecturas inválidas o de inicio; evitar registrar valores de falla como temperaturas reales.

**Evidencia esperada:** temperatura de referencia, cinco valores DS18B20, condiciones, foto y resultado.

## 2. Módulo de pH — agua

**Función.** Leer el pH mediante electrodo y acondicionador analógico; el **voltaje de salida no es directamente el pH** sin conocer la curva de calibración del módulo [3].

**Estado.** Se ha probado una señal analógica, revisada con multímetro alrededor de 3 V como máximo en las condiciones ensayadas. Ello **no prueba precisión, rango completo ni compatibilidad eléctrica en todas las condiciones**.

**Por documentar y verificar:**

1. Marca, referencia exacta de la sonda y del circuito acondicionador; hoja de datos y foto de ambos.
2. Voltaje de alimentación y rango máximo posible de salida antes de conectarlo a un ADC Heltec V4. Verificar límites de la entrada seleccionada [7], [8].
3. Procedimiento de preparación/conservación del electrodo indicado por su fabricante.
4. Calibración con **al menos dos soluciones tampón adecuadas para el rango de trabajo**, registrando temperatura y respuesta estable; seguir las indicaciones del equipo y la guía USGS [3].
5. Verificación con una solución adicional que no sea solo una de las utilizadas para ajustar.
6. Lecturas repetidas en agua de prueba y comparación con instrumento de referencia, si se dispone.

**Evidencia esperada:** valores de tampón certificados, fecha, temperatura, voltajes, ecuación/ajuste usado, lectura y error de verificación.

## 3. Módulo TDS — sólidos disueltos / conductividad por validar

**Función.** El módulo TDS entrega una señal que puede relacionarse con la concentración de sólidos disueltos conforme a su fabricante. **TDS, conductividad eléctrica (EC) y salinidad no son sinónimos**: una conversión depende de calibración, temperatura y composición del agua [4].

**Estado.** El componente está considerado; no hay una calibración consolidada de este módulo en el repositorio.

**Por documentar y verificar:**

1. Marca, modelo y ficha de sonda/acondicionador; rango admitido y materiales compatibles con agua salobre.
2. Determinar si el modelo permite medir directamente EC o solamente estimar TDS.
3. Revisar alimentación, voltaje de salida máximo y GPIO ADC válido de la Heltec V4 [7], [8].
4. Medir en soluciones patrón del rango esperado; registrar temperatura, voltaje, lectura y constante/calibración [4].
5. Evaluar compensación por temperatura y comportamiento en agua salobre, sin extrapolar una calibración de agua dulce.
6. Validar contra un conductímetro de referencia antes de etiquetar datos como µS/cm o mS/cm.

**Evidencia esperada:** modelo, solución patrón, temperatura, lecturas originales, ajuste y error. Hasta entonces, llamar al dato **“lectura TDS sin validar”**.

## 4. BME280 — presión atmosférica

**Función.** Medir presión atmosférica y proporcionar temperatura/humedad ambientales auxiliares mediante I²C; no es un sensor de temperatura de agua ni de oxígeno disuelto. El circuito integrado BME280 utiliza tensiones bajas definidas por Bosch [5].

**Estado.** En una prueba anterior se detectó una placa BME280 en dirección I²C **0x76**. El módulo adaptador se probó alimentado a 5 V en esa ocasión, pero **eso no confirma que el chip BME280 sea tolerante a 5 V**. Determinar si el *breakout* tiene regulador y adaptación de niveles.

**Por documentar y verificar:**

1. Foto de ambas caras y modelo del *breakout*; esquemático del módulo.
2. Distinguir la tensión del **chip** de la tensión de alimentación **admitida por el módulo**; revisar también niveles de SDA/SCL [5].
3. Confirmar la dirección I²C y el bus en la Heltec V4 sin asumir los GPIO21/22 de pruebas pasadas.
4. Registrar cinco medidas de presión (hPa), temperatura y humedad, con fecha, ubicación y condiciones.
5. Comparar presión con una referencia local y considerar que una estación puede reportar presión reducida al nivel del mar.

**Evidencia esperada:** escaneo I²C, tensión real, cinco lecturas y comparación.

## 5. Interruptor flotador P45 — estado de nivel

**Función.** Entregar una señal **binaria** de posición del flotador; no mide de forma continua una altura en centímetros sin calibración mecánica o más sensores.

**Estado.** En un ESP32 anterior se observó **LOW = contacto cerrado** y **HIGH = contacto abierto** con polarización de entrada en ese montaje. **La polaridad final debe verificarse nuevamente** según la orientación física y el circuito utilizado.

**Por documentar y verificar:**

1. Identificar fabricante y ficha exacta “P45”; material, temperatura, protección, corriente de contacto y orientación de montaje.
2. Dibujar su conexión real a un GPIO viable de Heltec V4: alimentación/polarización, resistencia de protección y filtro si procede.
3. Medir diez ciclos de apertura y cierre; registrar rebotes, falsas transiciones y la posición mecánica.
4. Comprobar comportamiento tras salpicaduras, vibración y cambios de orientación, sin exponer contactos no protegidos.

**Evidencia esperada:** foto, diagrama real verificado y tabla de transiciones. No se incorpora un datasheet P45 hasta confirmar el fabricante.

## 6. INA219 — instrumento auxiliar de energía (no sensor de calidad del agua)

**Función.** El INA219 mide corriente/tensión del bus y permite estimar potencia eléctrica mediante una resistencia de derivación (*shunt*) [6].

**Estado.** Propuesto como apoyo a pruebas de consumo; **no existe un sensor de porcentaje de batería implementado**. La corriente/voltaje instantáneos por sí solos no determinan la carga remanente de un power bank.

**Por documentar y verificar:**

1. Confirmar módulo, valor del *shunt* y rango/posición de conexión segura.
2. Registrar V, mA y mW en espera, activación de sensores, lectura y transmisión LoRa.
3. Comprobar el sentido de corriente y comparar con un multímetro adecuado.
4. Usar resultados para estimar consumo por sesión y ensayar autonomía; evitar publicar un “% de batería” no medido.

## 7. Puntos comunes antes del firmware final

- Confirmar **GPIO disponibles en Heltec WiFi LoRa 32 V4**, entradas ADC, niveles eléctricos y conflictos con LoRa/OLED [7], [8].
- Guardar el **valor crudo y su unidad**, el resultado calibrado cuando proceda, el estado de validez, y la identificación de sensor/sesión.
- Revisar masas comunes, alimentación de cada módulo, corrosión, sellado y tiempo de estabilización.
- El plan es **una sesión por hora con cinco lecturas**; no se afirma que este ciclo funcione ya de extremo a extremo.
- El oxígeno disuelto será una **estimación futura** del modelo; ninguno de estos sensores mide directamente OD.

Para ejecutar estos pendientes: [Plan de pruebas](../Plan_de_pruebas.md) y [Registro de evidencias](../Registro_de_evidencias.md).

## Referencias (formato IEEE)

[1] Analog Devices, “DS18B20: Programmable Resolution 1-Wire Digital Thermometer,” *Hoja de datos*. [En línea]. Disponible: https://www.analog.com/media/en/technical-documentation/data-sheets/ds18b20.pdf. [Accedido: 29-oct-2026].

[2] U.S. Geological Survey, “Temperature,” *Techniques and Methods*, libro 9, cap. A6.1, 2024, doi: 10.3133/tm9A6.1.

[3] U.S. Geological Survey, “Chapter A6.4. Measurement of pH,” *Techniques and Methods*, libro 9, cap. A6.4, 2021, doi: 10.3133/tm9A6.4.

[4] U.S. Geological Survey, “Chapter A6.3. Specific Conductance,” *Techniques and Methods*, libro 9, cap. A6.3, 2019, doi: 10.3133/tm9A6.3.

[5] Bosch Sensortec, “BME280: Combined Humidity and Pressure Sensor,” *Hoja de datos*, BST-BME280-DS001-23, rev. 1.23 (2022). [En línea]. Disponible: https://www.bosch-sensortec.com/media/boschsensortec/downloads/datasheets/bst-bme280-ds002.pdf. [Accedido: 29-oct-2026].

[6] Texas Instruments, “INA219: Zerø-Drift, Bidirectional Current/Power Monitor With I²C Interface,” *Hoja de datos*, rev. G. [En línea]. Disponible: https://www.ti.com/lit/ds/symlink/ina219.pdf. [Accedido: 29-oct-2026].

[7] Heltec Automation, “WiFi LoRa 32,” *Documentación técnica del fabricante*. [En línea]. Disponible: https://docs.heltec.org/en/node/esp32/wifi_lora_32/index.html. [Accedido: 29-oct-2026].

[8] Espressif Systems, “Analog to Digital Converter (ADC) — ESP32-S3,” *ESP-IDF Programming Guide*. [En línea]. Disponible: https://docs.espressif.com/projects/esp-idf/en/stable/esp32s3/api-reference/peripherals/adc/index.html. [Accedido: 29-oct-2026].
