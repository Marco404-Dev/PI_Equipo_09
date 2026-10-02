# **INTERNET DE LAS COSAS (IoT)**

Es una red masiva de objetos físicos que cuentan con sensores y tecnología para recopilar, enviar e intercambiar datos a través de Internet con otros dispositivos y sistemas.

Durante la práctica, se desarrollaron diversas actividades utilizando un ESP32 para recibir la información de sensores, realizar cálculos (conversión de ADC a voltaje), conectarse a la red WiFi y controlar el dispositivo desde la nube.

## **Actividad 01 \- 02: Lectura de un potenciómetro con ESP32 y Scanner WiFi con ESP32**

En esta actividad se realizó la lectura del valor analogico de un potenciómetro conectado al  ESP32 y este lo muestra cada medio segundo.

<img width="1600" height="1000" alt="image" src="https://github.com/user-attachments/assets/8b6e175d-ad40-4f0d-a695-d530d2855524" />

Después, se procedió a conectar el microcontrolador a un punto de acceso (Red WiFi), de esta manera puede funcionar como un servidor web para visualizar los datos desde otros dispositivos o enviar información a plataformas IoT mediante protocolos como MQTT, y se tomó un promedio de 10 muestras de lectura analógica para reducir las fluctuaciones causadas por el ruido eléctrico y obtener lecturas más estables. Además, la conversión del valor digital del ADC a voltaje facilita la interpretación de las señales analógicas.

<img width="1600" height="952" alt="image" src="https://github.com/user-attachments/assets/5d2c563e-8dc0-4094-a1c2-ef2589135def" />

## **Actividad 03 \- 04: Enviando datos en la nube**

El ESP32 toma el valor obtenido del sensor, lo procesa y luego lo envía a través de Internet a una plataforma IoT. En estas plataformas, los datos pueden almacenarse y mostrarse mediante gráficos, indicadores o tablas, permitiendo monitorear las mediciones desde otro dispositivo. Para realizar esta comunicación, se pueden utilizar protocolos como HTTP, que funciona mediante solicitudes, o MQTT, que permite publicar datos de manera eficiente y continua.

<img width="1600" height="829" alt="image" src="https://github.com/user-attachments/assets/5073211f-6ccd-45ac-b09f-dfe11755b69f" />

<img width="1600" height="794" alt="image" src="https://github.com/user-attachments/assets/901c177d-2070-462b-85c3-75eb85a7c20f" />

<img width="1600" height="800" alt="image" src="https://github.com/user-attachments/assets/4f6ca52e-6216-48b6-bf93-3f81a9ad5c9b" />

## **Actividad 05: Controlando desde la nube**

En esta actividad se implementó un sistema de control remoto desde la nube, donde la comunicación se realizó desde la plataforma web hacia el ESP32. Un interruptor en la interfaz permite enviar una orden para cambiar el estado del LED, encendiéndose o apagándose.

Lo que permitió demostrar la comunicación bidireccional del IoT, ya que no solo se reciben datos de sensores, sino que también se pueden enviar órdenes desde Internet para controlar dispositivos físicos.

<img width="1200" height="1600" alt="image" src="https://github.com/user-attachments/assets/c8753520-6b5a-4e2f-924c-53f12aa47748" />




