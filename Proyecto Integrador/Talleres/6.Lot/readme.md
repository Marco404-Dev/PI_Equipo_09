# Resumen de la práctica: ESP32, MQTT y Node-RED

## Descripción

En la práctica de hoy trabajamos con un **ESP32** conectado a un sensor ambiental. El objetivo principal fue leer datos de **temperatura, humedad y presión atmosférica**, enviarlos mediante **MQTT** y mostrarlos en un **Dashboard creado con Node-RED**.

También se agregó el control de un **LED**, permitiendo enviar comandos desde Node-RED hacia el ESP32.

---

## 1. Lectura del sensor ambiental

Primero configuramos el ESP32 para obtener información del sensor.

Las variables trabajadas fueron:

- Temperatura en grados Celsius (°C).
- Humedad relativa en porcentaje (%).
- Presión atmosférica en hectopascales (hPa).

En el Monitor Serie pudimos observar valores como:

<img width="1881" height="852" alt="Screenshot 2026-10-01 192714" src="https://github.com/user-attachments/assets/1b1800f2-f87a-4128-bcbc-3c875a04f26b" />

