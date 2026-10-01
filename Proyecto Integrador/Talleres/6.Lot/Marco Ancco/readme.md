# Taller de IoT con ESP32

## Descripción

En este taller usamos una placa **ESP32** para realizar diferentes actividades de Internet de las Cosas o **IoT**.

El ESP32 funciona como un pequeño cerebro. Puede recibir información de sensores, hacer cálculos, conectarse a WiFi y controlar otros dispositivos.

Durante las actividades aprendimos a:

- Leer un potenciómetro.
- Convertir una lectura ADC a voltaje.
- Conectar el ESP32 a WiFi.
- Enviar información a Arduino CLoud.
- Encender y apagar un LED desde una página web.

---

# 1. Lectura del potenciómetro

## ¿Qué hace?

Un potenciómetro es una pequeña perilla que podemos girar.

Cuando la giramos, cambia el voltaje que recibe el ESP32. El ESP32 convierte este voltaje en un número.

En esta actividad usamos el **GPIO 34**.

El funcionamiento es:

Cuando giramos el potenciómetro, podemos observar cómo cambia el número mostrado en el Monitor Serie.

## Código

```cpp
const int potenciometro = 34;

void setup() {
  Serial.begin(115200);
  pinMode(potenciometro, INPUT);
}

void loop() {

  int valor = analogRead(potenciometro);

  Serial.print("Valor del potenciometro: ");
  Serial.println(valor);

  delay(500);
}
```

## Explicación sencilla

`analogRead()` sirve para preguntarle al ESP32 qué valor está llegando al pin.

El valor se guarda en la variable `valor`.

Después usamos `Serial.println()` para mostrar ese número en el Monitor Serie.

El `delay(500)` hace que el ESP32 espere medio segundo antes de volver a medir.

---

# 2. Conversión de ADC a voltaje

## ¿Qué es ADC?

El ESP32 no entiende directamente algo como:

```text
2.5 voltios
```

Primero lo representa con un número llamado **ADC**.

En este ejercicio usamos valores entre:

```text
0 → 0 V
4095 → 3.3 V
```

Por eso podemos convertir el número ADC a voltaje.

También tomamos **10 mediciones** y calculamos un promedio. Esto ayuda a obtener una lectura más estable.

## Código

```cpp
const int pinSensor = 34;
const int numeroLecturas = 10;

void setup() {
  Serial.begin(115200);
}

void loop() {

  long suma = 0;

  for (int i = 0; i < numeroLecturas; i++) {

    int lectura = analogRead(pinSensor);

    suma = suma + lectura;

    delay(10);
  }

  float promedio = suma / (float)numeroLecturas;

  float voltaje = promedio * 3.3 / 4095.0;

  Serial.print("Promedio ADC: ");
  Serial.print(promedio, 2);

  Serial.print(" | Voltaje: ");
  Serial.print(voltaje, 2);

  Serial.println(" V");

  delay(500);
}
```


# 3. Conexión del ESP32 a WiFi

## ¿Qué hacemos?

Ahora queremos conectar el ESP32 a Internet mediante una red WiFi.

Para hacerlo necesitamos:

```text
Nombre del WiFi
Contraseña
```

Cuando el ESP32 logra conectarse, el router le entrega una **dirección IP**.

Por ejemplo:

```text
172.20.10.2
```

Esta dirección sirve para identificar al ESP32 dentro de la red.

## Código

```cpp
#include <WiFi.h>

const char* wifi = "NOMBRE_DE_LA_RED";
const char* clave = "CONTRASEÑA_DE_LA_RED";

void setup() {

  Serial.begin(115200);

  Serial.println("Buscando red WiFi...");

  WiFi.begin(wifi, clave);

  while (WiFi.status() != WL_CONNECTED) {

    Serial.print(".");
    delay(500);
  }

  Serial.println();
  Serial.println("Conexion realizada");

  Serial.print("IP del ESP32: ");
  Serial.println(WiFi.localIP());
}

void loop() {

}
```

## Explicación sencilla

Esta línea:

```cpp
WiFi.begin(wifi, clave);
```

le dice al ESP32:

> Conéctate a esta red usando esta contraseña.

Después:

```cpp
WiFi.status()
```

comprueba si ya estamos conectados.

Cuando la conexión está lista:

```cpp
WiFi.localIP()
```

nos muestra la dirección IP del ESP32.

---

# 4. Envío de datos a ThingSpeak

## ¿Qué es ThingSpeak?

ThingSpeak es una plataforma que permite recibir información enviada desde dispositivos como el ESP32.

Nuestro sistema funciona así:

```text
Potenciómetro
      ↓
    ESP32
      ↓
     WiFi
      ↓
  ThingSpeak
      ↓
    Gráfica
```

El ESP32 lee el potenciómetro y envía el valor por Internet.

ThingSpeak recibe ese número y puede mostrarlo en una gráfica.

## Código

```cpp
#include <WiFi.h>
#include <ThingSpeak.h>

const char* nombreWifi = "NOMBRE_DE_LA_RED";
const char* claveWifi = "CONTRASEÑA_DE_LA_RED";

unsigned long canal = TU_CHANNEL_ID;
const char* apiKey = "TU_WRITE_API_KEY";

WiFiClient cliente;

const int pinPotenciometro = 34;

void setup() {

  Serial.begin(115200);

  WiFi.begin(nombreWifi, claveWifi);

  Serial.print("Conectando");

  while (WiFi.status() != WL_CONNECTED) {

    Serial.print(".");
    delay(500);
  }

  Serial.println();
  Serial.println("WiFi listo");

  Serial.print("Direccion IP: ");
  Serial.println(WiFi.localIP());

  ThingSpeak.begin(cliente);
}

void loop() {

  int valorSensor = analogRead(pinPotenciometro);

  Serial.print("Lectura: ");
  Serial.println(valorSensor);

  ThingSpeak.setField(1, valorSensor);

  int respuesta = ThingSpeak.writeFields(canal, apiKey);

  if (respuesta == 200) {

    Serial.println("Dato enviado correctamente");

  } else {

    Serial.print("No se pudo enviar. Codigo: ");
    Serial.println(respuesta);
  }

  delay(20000);
}
```

## Explicación sencilla

Primero el ESP32 lee el potenciómetro:

```cpp
analogRead(pinPotenciometro);
```

Después coloca ese número en el **Field 1**:

```cpp
ThingSpeak.setField(1, valorSensor);
```

Finalmente lo envía a nuestro canal de ThingSpeak.

Si aparece:

```text
Dato enviado correctamente
```

significa que la información llegó correctamente.

---

# 5. Medición de distancia con HC-SR04

## ¿Cómo funciona?

El **HC-SR04** es un sensor que permite medir distancias utilizando ultrasonido.

Podemos imaginarlo como un pequeño eco.

El sensor hace esto:

```text
Envía sonido
     ↓
El sonido golpea un objeto
     ↓
El sonido regresa
     ↓
ESP32 mide el tiempo
     ↓
Calcula la distancia
```

El sensor utiliza dos señales importantes:

```text
TRIG → envía el ultrasonido
ECHO → recibe el rebote
```

## Código

```cpp
#include <WiFi.h>
#include <ThingSpeak.h>

const char* red = "NOMBRE_DE_LA_RED";
const char* password = "CONTRASEÑA_DE_LA_RED";

unsigned long canalID = TU_CHANNEL_ID;
const char* apiKey = "TU_WRITE_API_KEY";

WiFiClient cliente;

const int trig = 25;
const int echo = 26;

float medirDistancia() {

  digitalWrite(trig, LOW);
  delayMicroseconds(2);

  digitalWrite(trig, HIGH);
  delayMicroseconds(10);

  digitalWrite(trig, LOW);

  long tiempo = pulseIn(echo, HIGH, 30000);

  if (tiempo == 0) {
    return 0;
  }

  float distancia = tiempo * 0.0343 / 2;

  return distancia;
}

void setup() {

  Serial.begin(115200);

  pinMode(trig, OUTPUT);
  pinMode(echo, INPUT);

  WiFi.begin(red, password);

  Serial.print("Conectando");

  while (WiFi.status() != WL_CONNECTED) {

    Serial.print(".");
    delay(500);
  }

  Serial.println();
  Serial.println("WiFi conectado");

  ThingSpeak.begin(cliente);
}

void loop() {

  float distanciaActual = medirDistancia();

  Serial.print("Distancia medida: ");
  Serial.print(distanciaActual, 2);
  Serial.println(" cm");

  ThingSpeak.setField(1, distanciaActual);

  int respuesta = ThingSpeak.writeFields(canalID, apiKey);

  if (respuesta == 200) {

    Serial.println("Distancia enviada");

  } else {

    Serial.println("Error al enviar");
  }

  delay(20000);
}
```

## Explicación sencilla

El ESP32 manda una señal muy pequeña usando `TRIG`.

Después espera que la señal regrese por `ECHO`.

Esta línea:

```cpp
pulseIn(echo, HIGH, 30000);
```

mide cuánto tiempo demoró en regresar.

Luego calculamos:

```cpp
float distancia = tiempo * 0.0343 / 2;
```

Dividimos entre 2 porque el sonido realiza dos viajes:

```text
Sensor → objeto
Objeto → sensor
```

El resultado se muestra en **centímetros** y también se envía a ThingSpeak.

---

# 6. Control de un LED desde una página web

## ¿Qué hacemos?

En esta actividad el ESP32 crea una pequeña página web.

Desde el navegador podemos presionar botones para controlar un LED.

El funcionamiento es:

```text
Celular o computadora
        ↓
     Navegador
        ↓
       WiFi
        ↓
      ESP32
        ↓
       LED
```

Tendremos dos botones:

```text
ENCENDER
APAGAR
```

## Código

```cpp
#include <WiFi.h>
#include <WebServer.h>

const char* redWifi = "NOMBRE_DE_LA_RED";
const char* claveWifi = "CONTRASEÑA_DE_LA_RED";

const int led = 23;

WebServer servidor(80);

String paginaWeb() {

  String pagina = R"rawliteral(

  <!DOCTYPE html>

  <html>

  <head>

    <meta charset="UTF-8">

    <title>Control LED ESP32</title>

    <style>

      body {
        font-family: Arial;
        text-align: center;
        margin-top: 50px;
      }

      button {
        padding: 15px;
        margin: 10px;
        font-size: 18px;
      }

    </style>

  </head>

  <body>

    <h1>Control del LED</h1>

    <p>Selecciona una opcion:</p>

    <a href="/encender">
      <button>ENCENDER</button>
    </a>

    <a href="/apagar">
      <button>APAGAR</button>
    </a>

  </body>

  </html>

  )rawliteral";

  return pagina;
}

void inicio() {

  servidor.send(200, "text/html", paginaWeb());
}

void encenderLed() {

  digitalWrite(led, HIGH);

  Serial.println("LED encendido");

  servidor.send(200, "text/html", paginaWeb());
}

void apagarLed() {

  digitalWrite(led, LOW);

  Serial.println("LED apagado");

  servidor.send(200, "text/html", paginaWeb());
}

void setup() {

  Serial.begin(115200);

  pinMode(led, OUTPUT);

  digitalWrite(led, LOW);

  WiFi.begin(redWifi, claveWifi);

  Serial.print("Conectando al WiFi");

  while (WiFi.status() != WL_CONNECTED) {

    Serial.print(".");
    delay(500);
  }

  Serial.println();

  Serial.print("IP para entrar a la pagina: ");
  Serial.println(WiFi.localIP());

  servidor.on("/", inicio);
  servidor.on("/encender", encenderLed);
  servidor.on("/apagar", apagarLed);

  servidor.begin();

  Serial.println("Pagina web lista");
}

void loop() {

  servidor.handleClient();
}
```

## Explicación sencilla

Primero el ESP32 se conecta al WiFi.

Después crea una página web.

En el Monitor Serie aparecerá una IP parecida a:

```text
192.168.1.10
```

Escribimos esa dirección en el navegador.

Cuando presionamos:

```text
ENCENDER
```

el navegador pide:

```text
/encender
```

y el ESP32 ejecuta:

```cpp
digitalWrite(led, HIGH);
```

Cuando presionamos:

```text
APAGAR
```

el ESP32 ejecuta:

```cpp
digitalWrite(led, LOW);
```

Así podemos controlar un dispositivo físico desde una página web.

---

# 7. Arquitectura general

Todas las actividades pueden juntarse de esta manera:

```text
                    WiFi
                      |
                      v
                 +---------+
                 |  ESP32  |
                 +----+----+
                      |
          +-----------+-----------+
          |                       |
          v                       v
   Potenciómetro               HC-SR04
          |                       |
          +-----------+-----------+
                      |
                      v
                 ThingSpeak
                      |
                      v
                   Gráficas


Navegador
    |
    v
  WiFi
    |
    v
 ESP32
    |
    v
  LED
```

El **ESP32 es el cerebro principal**.

Puede recibir información de sensores, procesarla, conectarse mediante WiFi, enviar datos a Internet y controlar dispositivos.

---

# 8. Resultados

| Actividad | ¿Qué conseguimos? |
|---|---|
| Potenciómetro | Leer un valor analógico |
| ADC | Convertir una lectura a voltaje |
| WiFi | Conectar el ESP32 a una red |
| ThingSpeak | Enviar datos a Internet |
| HC-SR04 | Medir una distancia |
| Página web | Encender y apagar un LED |

---

# 9. Conclusiones

En este taller aprendimos que el **ESP32 puede funcionar como el cerebro de un sistema IoT**.

Primero aprendimos a recibir información usando un potenciómetro. Después convertimos los valores obtenidos a voltaje.

También conectamos el ESP32 a una red WiFi. Gracias a esta conexión pudimos enviar información a **ThingSpeak** y observar los datos mediante gráficas.

Luego utilizamos el sensor **HC-SR04** para medir la distancia de un objeto. El ESP32 recibió la información del sensor, calculó la distancia y pudo enviarla a ThingSpeak.

Finalmente creamos una pequeña página web para controlar un LED. De esta manera comprobamos que el ESP32 no solamente puede recibir información, sino también realizar acciones.

En resumen, un sistema IoT sencillo puede funcionar así:

```text
Sensor → ESP32 → WiFi → Internet → Información
```

y también:

```text
Usuario → Internet/WiFi → ESP32 → Dispositivo
```
