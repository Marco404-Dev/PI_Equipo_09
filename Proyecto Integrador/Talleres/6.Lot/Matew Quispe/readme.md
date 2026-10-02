# Practica con ESP32 y plataformas IoT

En esta practica se utilizo un **ESP32 DevKit V1** para realizar lecturas de sensores, conectarse a una red WiFi y enviar informacion hacia plataformas IoT. Tambien se realizo el control de un LED, permitiendo comprobar tanto el monitoreo de datos como el control de un dispositivo fisico

---

## Lectura del potenciometro

Se conecto un potenciometro al **GPIO 34** del ESP32 para obtener valores mediante el conversor analogico-digital (ADC)

Para mejorar la estabilidad de las lecturas se tomaron **10 muestras consecutivas** y se calculo su promedio. Despues, el valor obtenido se convirtio a voltaje considerando el rango aproximado del ADC del ESP32 de **0 a 4095** y una referencia de **3.3 V**

La conversion utilizada fue:

```text
Voltaje = ADC × 3.3 / 4095
```

### Resultado en el monitor serial

<img width="1600" height="952" alt="image" src="https://github.com/user-attachments/assets/b0726f0c-fb09-4af5-b318-e0672ea2ba6d" />

En la imagen se observa el codigo ejecutandose en Arduino IDE y los resultados obtenidos en el monitor serial

Por ejemplo:

```text
Promedio ADC: 313.20 | Voltaje: 0.25 V
Promedio ADC: 314.40 | Voltaje: 0.25 V
Promedio ADC: 316.00 | Voltaje: 0.25 V
```

Aunque existen pequeñas variaciones en el ADC, el voltaje se mantiene estable. Esto demuestra que utilizar varias muestras y calcular un promedio ayuda a reducir las pequeñas variaciones presentes en una lectura analogica

---

## Conexion del ESP32 a WiFi

Para enviar informacion hacia Internet se conecto el ESP32 a una red WiFi creada mediante el **Hotspot de un telefono movil**

Para realizar la conexion se utilizo la libreria:

```cpp
#include <WiFi.h>
```

y se configuraron el nombre y la contraseña de la red

Cuando el ESP32 se conecta correctamente recibe una **direccion IP**, que permite identificarlo dentro de la red

Un resultado esperado en el monitor serial es:

```text
WiFi conectado
Direccion IP: 192.168.x.x
```

Esta conexion fue necesaria para posteriormente comunicar el ESP32 con las diferentes plataformas IoT

---

## Monitoreo del potenciometro en Arduino Cloud

Despues de comprobar la lectura del potenciometro, los datos fueron enviados hacia **Arduino Cloud**

Se crearon dos variables:

```text
ADC
voltaje
```

La variable `ADC` almacena la lectura promediada del potenciometro, mientras que `voltaje` representa el mismo valor convertido a voltios

### Variables registradas

<img width="1600" height="818" alt="image" src="https://github.com/user-attachments/assets/15437101-864d-4fdb-bc0a-5f801478a1aa" />

En la imagen se observa que Arduino Cloud esta recibiendo informacion desde el ESP32

Durante la captura se registraron aproximadamente:

```text
ADC: 1688.7
Voltaje: 1.361 V
```

La presencia de estos valores y su fecha de actualizacion confirma que existe comunicacion entre el ESP32 y la plataforma

### Dashboard del potenciometro

<img width="1600" height="794" alt="image" src="https://github.com/user-attachments/assets/4a30b766-f37e-41e8-bc67-ddbe37295741" />

Para visualizar mejor la informacion se utilizaron graficas para el **ADC** y el **voltaje**

Tambien se agrego un indicador tipo **Gauge** configurado entre:

```text
0 V - 3.3 V
```

En el momento de la captura se obtuvo aproximadamente:

```text
1.365 V
```

Las dos graficas presentan un comportamiento parecido porque el voltaje se calcula directamente a partir del ADC. Cuando cambia la posicion del potenciometro, ambos valores cambian al mismo tiempo

Esta prueba permitio comprobar como una señal obtenida fisicamente puede ser enviada por Internet y visualizada practicamente en tiempo real

---

## Monitoreo de variables ambientales

Posteriormente se trabajo con un sensor ambiental para obtener informacion directamente del entorno

Se utilizaron tres variables:

```text
temperatura
humedad
presion
```

El ESP32 realizo las mediciones y posteriormente las envio hacia Arduino Cloud

### Variables recibidas

<img width="1600" height="815" alt="image" src="https://github.com/user-attachments/assets/ef109ee8-4a8f-42e7-a586-28daaac4dfd8" />

Durante la prueba se registraron aproximadamente los siguientes valores:

```text
Temperatura: 25.6 °C
Humedad: 63.2 %
Presion: 1008.5 hPa
```

Esto demuestra que el ESP32 puede trabajar con varias variables al mismo tiempo y enviarlas hacia una plataforma IoT utilizando una sola conexion WiFi

### Dashboard ambiental

<img width="1600" height="800" alt="image" src="https://github.com/user-attachments/assets/fc54f000-509b-481b-a8d1-6f23c481fcde" />

La temperatura y la humedad fueron representadas mediante graficas, permitiendo observar sus pequeñas variaciones a traves del tiempo

Para la presion se utilizo un Gauge, donde se registro aproximadamente:

```text
1008.5 hPa
```

El uso de estos elementos facilita la interpretacion de los datos y permite observar tanto el valor actual como su comportamiento durante un periodo determinado

A diferencia del potenciometro, estas variables son obtenidas directamente de las condiciones del ambiente, por lo que representan un ejemplo mas cercano a una aplicacion real de monitoreo IoT

---

## Control de un LED con ThingSpeak

Finalmente se conecto un **LED** a una salida digital del ESP32

En este caso se trabajo con un actuador, ya que el LED no obtiene informacion del ambiente, sino que realiza una accion dependiendo de la orden recibida

Se utilizaron dos estados:

```text
1 = LED encendido
0 = LED apagado
```

### Codigo utilizado

<img width="1200" height="1600" alt="image" src="https://github.com/user-attachments/assets/1eb9620f-5d92-4a18-821d-59d998fe7d34" />

En la imagen se observa parte del codigo utilizado para establecer la comunicacion con **ThingSpeak**

Para ello se utilizaron las librerias:

```cpp
#include <WiFi.h>
#include <ThingSpeak.h>
```

Ademas, se configuraron los datos correspondientes al canal de ThingSpeak y el pin digital conectado al LED

---

## Estados registrados en ThingSpeak

<img width="1200" height="1600" alt="image" src="https://github.com/user-attachments/assets/575c3dc0-e60e-4414-83fd-f444521a7fc6" />

En la grafica se observan cambios entre los valores **0 y 1**

Estos valores representan los dos estados utilizados para controlar el LED:

```text
0 → apagado
1 → encendido
```

La grafica permite verificar cuando se realizaron los diferentes cambios de estado

---

## LED encendido

<img width="1600" height="1200" alt="image" src="https://github.com/user-attachments/assets/c204f25e-02c0-4cef-a964-eb15d44c305b" />

En la fotografia se observa el circuito fisico con el LED encendido

Esta evidencia permite comprobar que los cambios realizados en el sistema no solamente se muestran dentro de una plataforma web, sino que tambien producen una accion sobre un componente fisico

---

## LED apagado

<img width="1600" height="1200" alt="image" src="https://github.com/user-attachments/assets/3f7d90a5-a046-44ca-8dc5-8a91a63b967d" />

En esta segunda fotografia se observa el mismo circuito con el LED apagado

La comparacion de ambas imagenes permite comprobar claramente el funcionamiento de los dos estados utilizados durante la prueba

---

## Que aprendimos

Durante esta practica se aprendio a utilizar diferentes funciones del ESP32 dentro de una aplicacion IoT

Primero se realizaron lecturas analogicas utilizando un potenciometro y se mejoro la estabilidad de los datos mediante el promedio de varias muestras. Tambien se convirtio el valor obtenido por el ADC a voltaje

Posteriormente se conecto el ESP32 a una red WiFi y se enviaron datos hacia **Arduino Cloud**, donde se utilizaron graficas y gauges para visualizar las mediciones

Tambien se trabajo con variables ambientales como temperatura, humedad y presion, comprobando que un solo ESP32 puede obtener y transmitir varios datos simultaneamente

Finalmente, mediante ThingSpeak y un LED se comprobo la diferencia entre **monitorear informacion** y **controlar un actuador**

---

## Reflexion final

La practica permitio comprender de forma mas clara como funciona un sistema IoT basico

El ESP32 puede recibir informacion desde sensores, procesarla y enviarla mediante WiFi hacia una plataforma en Internet. Estas plataformas permiten almacenar y visualizar los datos de una forma mas sencilla mediante graficas e indicadores

Tambien se comprobo que la comunicacion puede utilizarse para controlar dispositivos fisicos, como ocurrio con el LED

En conjunto, las pruebas permitieron relacionar cuatro elementos importantes:

```text
Sensores → ESP32 → Internet → Visualizacion o control
```

Esto permitio entender de manera practica como un microcontrolador puede conectar elementos del mundo fisico con servicios disponibles en Internet
