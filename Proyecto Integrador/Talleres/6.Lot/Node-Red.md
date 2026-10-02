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
<img width="738" height="1600" alt="WhatsApp Image 2026-10-01 at 7 04 34 PM" src="https://github.com/user-attachments/assets/ff2e3ea4-43db-4181-aad1-e099a402ad58" />


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
```

<img width="1600" height="674" alt="WhatsApp Image 2026-10-01 at 6 35 45 PM" src="https://github.com/user-attachments/assets/33fb8d7a-82fa-45d1-8bfd-169db4dc7097" />


## 4. Gráfica de temperatura

Además del valor actual, agregamos una **gráfica** para observar cómo cambia la temperatura con el tiempo.

La gráfica permite guardar visualmente las mediciones recibidas y observar si la temperatura **aumenta, disminuye o permanece estable**.

Durante la prueba se observaron valores cercanos a los **25 °C**.

Esto es diferente al gauge:

- El **gauge** muestra principalmente el valor actual.
- La **gráfica** permite observar el comportamiento de los valores durante un periodo.

<img width="1901" height="872" alt="Screenshot 2026-10-01 192123" src="https://github.com/user-attachments/assets/99ff52b3-6a4d-4393-9f8d-0a6953e8f33d" />



## 5. Control del LED

También agregamos un **switch** en el Dashboard de Node-RED.

Este switch permite enviar una orden hacia el ESP32 para:

```text
ENCENDER LED
o
APAGAR LED
```
<img width="996" height="686" alt="Screenshot 2026-10-01 192636" src="https://github.com/user-attachments/assets/751bbced-2dde-4f41-a39d-e513c1182cc8" />


## 6. ¿Qué aprendimos?

Durante esta práctica aprendimos a integrar varias herramientas utilizadas en **IoT**.

Primero comprobamos cómo obtener información de un sensor utilizando el **ESP32**. Luego aprendimos a enviar esos datos mediante el protocolo **MQTT**.

También entendimos mejor el uso de los **tópicos MQTT**, ya que permiten indicar dónde se publican y reciben los mensajes.

Aprendimos a utilizar **JSON** para agrupar varios datos, como temperatura, humedad y presión, dentro de un mismo mensaje.

Con **Node-RED** aprendimos a recibir estos datos, separarlos y mostrarlos mediante **gauges** y **gráficas**.

Finalmente, comprobamos que **MQTT** no solamente sirve para enviar información desde los sensores, sino también para controlar dispositivos, como en el caso del **LED**.

