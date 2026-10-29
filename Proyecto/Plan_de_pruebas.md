# Plan básico de pruebas del prototipo

**Equipo 09 · 29/10/2026 · Versión de trabajo**

Las pruebas deben realizarse **por partes antes del montaje conjunto**. No se fijan umbrales de aceptación sin una fuente o criterio acordado.

| ID | Prueba | Procedimiento mínimo | Qué guardar como evidencia |
|---|---|---|---|
| P01 | Identificación del hardware | Fotografiar ambos Heltec V4 y cada placa sensora; registrar versión, modelo y alimentación admitida | Foto legible y enlace a ficha técnica |
| P02 | Temperatura DS18B20 | Hacer cinco lecturas en medio estable; repetir en otro punto de temperatura y contrastar con termómetro de referencia [1] | Lecturas, referencia, diferencia y tiempo de estabilización |
| P03 | pH | Identificar el módulo; medir voltaje de salida; calibrar con soluciones tampón según su manual y verificar con una muestra independiente [2] | Buffers, temperatura, voltaje, pH de referencia, lectura |
| P04 | TDS/conductividad | Identificar sonda y módulo; usar soluciones patrón compatibles; anotar temperatura y comprobar escala o conversión antes de llamarla conductividad [3] | Valor patrón, voltaje, lectura, conversión aplicada |
| P05 | Presión BME280 | Detectar dispositivo I²C; comprobar alimentación real de la placa adaptadora y comparar presión con referencia local confiable [4] | Dirección I²C, alimentación, lecturas y comparación |
| P06 | Flotador P45 | Registrar abierto/cerrado, repetibilidad y cambios falsos por vibración o salpicaduras | Tabla de transiciones y fotos del montaje |
| P07 | Integración de sensores | Encender conjuntamente; repetir P02–P06 sin interferencias eléctricas apreciables | Datos simultáneos, errores, temperatura y tensión |
| P08 | Paquetes LoRa | Enviar una secuencia numerada; contar enviados, recibidos y duplicados en puntos de ensayo | Distancia, obstáculos, antena, SF, potencia configurada, resultados |
| P09 | OLED | Mostrar lecturas identificables y un estado claro si falta un sensor | Foto/video con una lectura correcta y una falla controlada |
| P10 | Ciclo de ahorro | Activar sensores, esperar estabilización, hacer cinco lecturas y apagarlos; repetir ciclos | Tiempos, cinco valores y corriente encendido/apagado |
| P11 | Energía | Medir corriente y tensión durante encendido, transmisión y espera; después evaluar autonomía con power bank | Tabla mA/V, tiempo y condiciones de la batería |
| P12 | Panel/UPS (si se monta) | Revisar voltajes en vacío/con carga y comportamiento en cambios de luz antes de conectar al prototipo | Modelo, mediciones y estado de protección |
| P13 | Protección ambiental | Inspeccionar conexiones, paso de cables y carcasa; ensayar estanqueidad sin electrónica energizada antes de uso en campo | Fotos, ubicación de filtraciones y mejoras |

## Registro recomendado por ensayo

- **Fecha, lugar, responsable y versión** de la placa/código.
- **Material y condiciones:** agua dulce/salobre, temperatura aproximada, alimentación, estado de antena, montaje.
- **Datos sin modificar:** al menos cinco lecturas por ensayo, unidades y fallos.
- **Patrón o referencia:** nombre, precisión disponible y fecha de calibración, si existe.
- **Resultado:** completado, incompleto o fallido; nota técnica y siguiente acción.
- **Enlace de evidencia:** foto, video, CSV, captura de consola u hoja de observación.

**Criterio:** una prueba previa con ESP32 DevKit no valida automáticamente el conexionado de la Heltec V4 [5]. Para la radio, no afirmar un alcance máximo a partir de una sola ruta.

Archivo complementario: [Registro de evidencias](Registro_de_evidencias.md) y [Sensores](Modulo%20Electronico/Sensores.md).

## Referencias (formato IEEE)

[1] U.S. Geological Survey, “Temperature,” *Techniques and Methods*, libro 9, cap. A6.1, 2024, doi: 10.3133/tm9A6.1.

[2] U.S. Geological Survey, “Chapter A6.4. Measurement of pH,” *Techniques and Methods*, libro 9, cap. A6.4, 2021, doi: 10.3133/tm9A6.4.

[3] U.S. Geological Survey, “Chapter A6.3. Specific Conductance,” *Techniques and Methods*, libro 9, cap. A6.3, 2019, doi: 10.3133/tm9A6.3.

[4] Bosch Sensortec, “BME280,” *Hoja de datos*, BST-BME280-DS001-23, rev. 1.23 (2022). [En línea]. Disponible: https://www.bosch-sensortec.com/media/boschsensortec/downloads/datasheets/bst-bme280-ds002.pdf. [Accedido: 29-oct-2026].

[5] Heltec Automation, “WiFi LoRa 32,” *Documentación del fabricante*. [En línea]. Disponible: https://docs.heltec.org/en/node/esp32/wifi_lora_32/index.html. [Accedido: 29-oct-2026].
