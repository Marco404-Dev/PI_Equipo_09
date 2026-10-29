# Módulo electrónico

## Estado del prototipo

- Se están utilizando **dos placas Heltec WiFi LoRa 32 V4** con radio LoRa, configuradas a **915 MHz** para las pruebas.
- Se ha comprobado una comunicación LoRa preliminar entre las placas. Las pruebas de OLED y sensores se realizan por etapas.
- Sensores considerados: **DS18B20** (temperatura), **módulo pH**, **módulo TDS** (lectura relacionada con sólidos disueltos) y **BME280** (presión atmosférica).
- La alimentación actual de las pruebas utiliza **5 V desde una batería externa (power bank)**. Se está evaluando un panel solar USB de **5 W**, todavía no integrado ni validado.

## Pendiente de verificar

- Distribución definitiva de pines y compatibilidad eléctrica de sensores con la **Heltec V4 (ESP32-S3)**; no copiar directamente la numeración de un ESP32 DevKit anterior.
- Calibración de pH/TDS y conversión de la lectura TDS a conductividad, si se necesitara.
- Integración simultánea de sensores, circuito de apagado de alimentación y pruebas de consumo/autonomía.
- Protección del circuito frente a humedad y salinidad antes del montaje en campo.

**No se declara un esquema de conexiones ni firmware definitivo en esta etapa.**
