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

## 2. Conexión mediante MQTT

Después configuramos el ESP32 para comunicarse utilizando el protocolo **MQTT**.

MQTT permite que diferentes dispositivos envíen y reciban información utilizando un servidor llamado **broker**.

En nuestro caso utilizamos:

```text
Servidor MQTT: mqtt.rcr-labs.com
Puerto: 1883
```

El ESP32 publica los datos del sensor en el tópico:
```text
equipo009/sensor/datos
```

También escucha los comandos para el LED mediante:
```text
equipo009/actuadores/led
```

Los datos enviados se agruparon en formato JSON. Por ejemplo:
```text
{
  "dispositivo": "FD_Equipo09",
  "temperatura": 24.81,
  "presion": 1000.668,
  "humedad": 54.76
}
```


<img width="1881" height="852" alt="Screenshot 2026-10-01 192714" src="https://github.com/user-attachments/assets/1b1800f2-f87a-4128-bcbc-3c875a04f26b" />

## 3. Configuración en Node-RED

Luego utilizamos **Node-RED** para recibir los datos publicados por el ESP32.

Se creó un nodo MQTT conectado al tópico:

```text
equipo009/sensor/datos
```
Después se utilizaron diferentes nodos para separar cada valor recibido.

Por ejemplo:

- Temperatura.
- Humedad.
- Presión atmosférica.
- Nombre del dispositivo.

Ademas eespués de recibir los datos, diseñamos un **Dashboard** para mostrarlos de una manera más clara.

Utilizamos indicadores tipo **gauge**, parecidos a un velocímetro.

En ellos pudimos visualizar:

```text
Temperatura: aproximadamente 24.82 °C
Humedad relativa: aproximadamente 54.5 %
Presión atmosférica: aproximadamente 1000.63 hPa

<img width="1600" height="674" alt="WhatsApp Image 2026-10-01 at 6 35 45 PM" src="https://github.com/user-attachments/assets/33fb8d7a-82fa-45d1-8bfd-169db4dc7097" />




