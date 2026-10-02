# Práctica con ESP32 y plataformas IoT

En esta práctica se utilizó un **ESP32 DevKit V1** para realizar lecturas de sensores, conectarse a una red WiFi y enviar información hacia plataformas IoT. También se realizó el control de un LED, permitiendo comprobar tanto el monitoreo de datos como el control de un dispositivo físico.

---

## Lectura del potenciómetro

Se conectó un potenciómetro al **GPIO 34** del ESP32 para obtener valores mediante el conversor analógico-digital (ADC).

Para mejorar la estabilidad de las lecturas se tomaron **10 muestras consecutivas** y se calculó su promedio. Después, el valor obtenido se convirtió a voltaje considerando el rango aproximado del ADC del ESP32 de **0 a 4095** y una referencia de **3.3 V**.

La conversión utilizada fue:

```text
Voltaje = ADC × 3.3 / 4095
```

### Resultado en el monitor serial

![Lectura del potenciómetro](imagenes/01_potenciometro_promedio.png)

En la imagen se observa el código ejecutándose en Arduino IDE y los resultados obtenidos en el monitor serial.

Por ejemplo:

```text
Promedio ADC: 313.20 | Voltaje: 0.25 V
Promedio ADC: 314.40 | Voltaje: 0.25 V
Promedio ADC: 316.00 | Voltaje: 0.25 V
```

Aunque existen pequeñas variaciones en el ADC, el voltaje se mantiene estable. Esto demuestra que utilizar varias muestras y calcular un promedio ayuda a reducir las pequeñas variaciones presentes en una lectura analógica.

---

## Conexión del ESP32 a WiFi

Para enviar información hacia Internet se conectó el ESP32 a una red WiFi creada mediante el **Hotspot de un teléfono móvil**.

Para realizar la conexión se utilizó la librería:

```cpp
#include <WiFi.h>
```

y se configuraron el nombre y la contraseña de la red.

Cuando el ESP32 se conecta correctamente recibe una **dirección IP**, que permite identificarlo dentro de la red.

Un resultado esperado en el monitor serial es:

```text
WiFi conectado
Direccion IP: 192.168.x.x
```

Esta conexión fue necesaria para posteriormente comunicar el ESP32 con las diferentes plataformas IoT.

---

## Monitoreo del potenciómetro en Arduino Cloud

Después de comprobar la lectura del potenciómetro, los datos fueron enviados hacia **Arduino Cloud**.

Se crearon dos variables:

```text
ADC
voltaje
```

La variable `ADC` almacena la lectura promediada del potenciómetro, mientras que `voltaje` representa el mismo valor convertido a voltios.

### Variables registradas

![Variables ADC y voltaje](imagenes/02_variables_adc_voltaje.png)

En la imagen se observa que Arduino Cloud está recibiendo información desde el ESP32.

Durante la captura se registraron aproximadamente:

```text
ADC: 1688.7
Voltaje: 1.361 V
```

La presencia de estos valores y su fecha de actualización confirma que existe comunicación entre el ESP32 y la plataforma.

### Dashboard del potenciómetro

![Dashboard del potenciómetro](imagenes/03_dashboard_potenciometro.png)

Para visualizar mejor la información se utilizaron gráficas para el **ADC** y el **voltaje**.

También se agregó un indicador tipo **Gauge** configurado entre:

```text
0 V - 3.3 V
```

En el momento de la captura se obtuvo aproximadamente:

```text
1.365 V
```

Las dos gráficas presentan un comportamiento parecido porque el voltaje se calcula directamente a partir del ADC. Cuando cambia la posición del potenciómetro, ambos valores cambian al mismo tiempo.

Esta prueba permitió comprobar cómo una señal obtenida físicamente puede ser enviada por Internet y visualizada prácticamente en tiempo real.

---

## Monitoreo de variables ambientales

Posteriormente se trabajó con un sensor ambiental para obtener información directamente del entorno.

Se utilizaron tres variables:

```text
temperatura
humedad
presion
```

El ESP32 realizó las mediciones y posteriormente las envió hacia Arduino Cloud.

### Variables recibidas

![Variables ambientales](imagenes/04_variables_ambientales.png)

Durante la prueba se registraron aproximadamente los siguientes valores:

```text
Temperatura: 25.6 °C
Humedad: 63.2 %
Presión: 1008.5 hPa
```

Esto demuestra que el ESP32 puede trabajar con varias variables al mismo tiempo y enviarlas hacia una plataforma IoT utilizando una sola conexión WiFi.

### Dashboard ambiental

![Dashboard ambiental](imagenes/05_dashboard_ambiental.png)

La temperatura y la humedad fueron representadas mediante gráficas, permitiendo observar sus pequeñas variaciones a través del tiempo.

Para la presión se utilizó un Gauge, donde se registró aproximadamente:

```text
1008.5 hPa
```

El uso de estos elementos facilita la interpretación de los datos y permite observar tanto el valor actual como su comportamiento durante un periodo determinado.

A diferencia del potenciómetro, estas variables son obtenidas directamente de las condiciones del ambiente, por lo que representan un ejemplo más cercano a una aplicación real de monitoreo IoT.

---

## Control de un LED con ThingSpeak

Finalmente se conectó un **LED** a una salida digital del ESP32.

En este caso se trabajó con un actuador, ya que el LED no obtiene información del ambiente, sino que realiza una acción dependiendo de la orden recibida.

Se utilizaron dos estados:

```text
1 = LED encendido
0 = LED apagado
```

### Código utilizado

![Código del LED](imagenes/06_codigo_led.png)

En la imagen se observa parte del código utilizado para establecer la comunicación con **ThingSpeak**.

Para ello se utilizaron las librerías:

```cpp
#include <WiFi.h>
#include <ThingSpeak.h>
```

Además, se configuraron los datos correspondientes al canal de ThingSpeak y el pin digital conectado al LED.

---

## Estados registrados en ThingSpeak

![ThingSpeak LED](imagenes/07_thingspeak_led.png)

En la gráfica se observan cambios entre los valores **0 y 1**.

Estos valores representan los dos estados utilizados para controlar el LED:

```text
0 → apagado
1 → encendido
```

La gráfica permite verificar cuándo se realizaron los diferentes cambios de estado.

---

## LED encendido

![LED encendido](imagenes/08_led_encendido.png)

En la fotografía se observa el circuito físico con el LED encendido.

Esta evidencia permite comprobar que los cambios realizados en el sistema no solamente se muestran dentro de una plataforma web, sino que también producen una acción sobre un componente físico.

---

## LED apagado

![LED apagado](imagenes/09_led_apagado.png)

En esta segunda fotografía se observa el mismo circuito con el LED apagado.

La comparación de ambas imágenes permite comprobar claramente el funcionamiento de los dos estados utilizados durante la prueba.

---

## ¿Qué aprendimos?

Durante esta práctica se aprendió a utilizar diferentes funciones del ESP32 dentro de una aplicación IoT.

Primero se realizaron lecturas analógicas utilizando un potenciómetro y se mejoró la estabilidad de los datos mediante el promedio de varias muestras. También se convirtió el valor obtenido por el ADC a voltaje.

Posteriormente se conectó el ESP32 a una red WiFi y se enviaron datos hacia **Arduino Cloud**, donde se utilizaron gráficas y gauges para visualizar las mediciones.

También se trabajó con variables ambientales como temperatura, humedad y presión, comprobando que un solo ESP32 puede obtener y transmitir varios datos simultáneamente.

Finalmente, mediante ThingSpeak y un LED se comprobó la diferencia entre **monitorear información** y **controlar un actuador**.

---

## Reflexión final

La práctica permitió comprender de forma más clara cómo funciona un sistema IoT básico.

El ESP32 puede recibir información desde sensores, procesarla y enviarla mediante WiFi hacia una plataforma en Internet. Estas plataformas permiten almacenar y visualizar los datos de una forma más sencilla mediante gráficas e indicadores.

También se comprobó que la comunicación puede utilizarse para controlar dispositivos físicos, como ocurrió con el LED.

En conjunto, las pruebas permitieron relacionar cuatro elementos importantes:

```text
Sensores → ESP32 → Internet → Visualización o control
```

Esto permitió entender de manera práctica cómo un microcontrolador puede conectar elementos del mundo físico con servicios disponibles en Internet.
