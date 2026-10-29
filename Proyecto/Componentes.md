# Inventario de componentes y estado de validación

**Equipo 09 · 29/10/2026 · No sustituye una lista de compras ni un esquema eléctrico definitivo.**

| Elemento | Uso previsto | Estado documentado | Pendiente |
|---|---|---|---|
| 2 × Heltec WiFi LoRa 32 V4 | Transmisión y recepción por radio | Prueba de enlace LoRa a 915 MHz realizada; OLED probado | Alcance, pérdida de paquetes, pinout definitivo [1] |
| DS18B20 | Temperatura del agua | Lectura aislada probada durante desarrollo | Repetibilidad, comparación con patrón y montaje final [2] |
| Módulo analógico de pH | pH del agua | Pruebas de señal analógica; salida revisada con multímetro | Identificar fabricante/modelo y calibrar con soluciones tampón [3] |
| Módulo analógico TDS | Respuesta relacionada con sólidos disueltos | Seleccionado; ensayo completo sin evidencia consolidada | Identificar modelo, calibrar y validar si permite inferir conductividad [4] |
| BME280 en placa adaptadora | Presión atmosférica; temperatura/humedad auxiliares | Módulo detectado en pruebas anteriores, dirección I²C 0x76 | Identificar placa adaptadora y tensiones admitidas; integrar en Heltec V4 [5] |
| Interruptor flotador P45 | Detectar estado de contacto/nivel | Pruebas de abierto/cerrado en ESP32 previo | Ficha del modelo, encapsulado, antirrebote y GPIO V4 |
| INA219 | Medir tensión/corriente en ensayos energéticos | Considerado para pruebas | Montaje y calibración; **no equivale a porcentaje de batería** [6] |
| Power bank 5 V | Alimentación experimental | Utilizado en laboratorio | Consumo, autonomía, comportamiento con carga intermitente |
| Panel solar USB 5 W y UPS | Recarga o alimentación futura | En evaluación | Compatibilidad de entrada, regulación, protección y ensayo real |
| Circuito high-side con MOSFET | Desconectar sensores fuera de muestreo | Diseño en evaluación | Verificación con carga, corriente de fuga y compatibilidad |
| Estructura de boya y PCB | Soporte y protección física | Archivos de diseño mecánico en repositorio | Montaje, estanqueidad y corrosión en condiciones reales |

## Convención para actualizar el inventario

- **Probado:** existe resultado observacional; agregar evidencia antes de cerrar el punto.
- **En prueba:** hardware disponible o evaluado, pero todavía sin protocolo completado.
- **Previsto:** parte del diseño; no debe confundirse con una función implementada.
- **Descartado:** registrar el motivo y la fecha, si el equipo toma esa decisión.

**Nota sobre GPIO:** los valores históricos usados con ESP32 DevKit no deben copiarse como conexiones de la Heltec V4. La tabla definitiva se añadirá después de pruebas eléctricas [1].

Ver también [fichas de sensores](Modulo%20Electronico/Sensores.md), [plan de pruebas](Plan_de_pruebas.md) y [registro de evidencias](Registro_de_evidencias.md).

## Referencias (formato IEEE)

[1] Heltec Automation, “WiFi LoRa 32,” *Documentación del fabricante*. [En línea]. Disponible: https://docs.heltec.org/en/node/esp32/wifi_lora_32/index.html. [Accedido: 29-oct-2026].

[2] Analog Devices, “DS18B20: Programmable Resolution 1-Wire Digital Thermometer,” *Hoja de datos*. [En línea]. Disponible: https://www.analog.com/media/en/technical-documentation/data-sheets/ds18b20.pdf. [Accedido: 29-oct-2026].

[3] U.S. Geological Survey, “Chapter A6.4. Measurement of pH,” *Techniques and Methods*, libro 9, cap. A6.4, 2021, doi: 10.3133/tm9A6.4.

[4] U.S. Geological Survey, “Chapter A6.3. Specific Conductance,” *Techniques and Methods*, libro 9, cap. A6.3, 2019, doi: 10.3133/tm9A6.3.

[5] Bosch Sensortec, “BME280: Combined Humidity and Pressure Sensor,” *Hoja de datos*, doc. BST-BME280-DS001-23, rev. 1.23 (2022). [En línea]. Disponible: https://www.bosch-sensortec.com/media/boschsensortec/downloads/datasheets/bst-bme280-ds002.pdf. [Accedido: 29-oct-2026].

[6] Texas Instruments, “INA219: Zerø-Drift, Bidirectional Current/Power Monitor With I²C Interface,” *Hoja de datos*, rev. G. [En línea]. Disponible: https://www.ti.com/lit/ds/symlink/ina219.pdf. [Accedido: 29-oct-2026].
