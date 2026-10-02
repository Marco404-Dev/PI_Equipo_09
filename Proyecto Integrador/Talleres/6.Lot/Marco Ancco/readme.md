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
<img width="1600" height="885" alt="WhatsApp Image 2026-10-01 at 7 26 02 PM (1)" src="https://github.com/user-attachments/assets/bdbd8dc7-d7fa-4b84-8247-d234365bc89f" />


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



# 4. Envío de datos a Arduino Cloud

## ¿Qué es Arduino Cloud?

Arduino Cloud es una plataforma que permite recibir y visualizar información enviada desde dispositivos como el ESP32.

En esta actividad, el ESP32 se conecta a una red WiFi y envía los valores obtenidos por los sensores a Arduino Cloud. Los datos pueden observarse desde un Dashboard mediante indicadores o gráficas.

## Explicación sencilla

Primero el ESP32 obtiene la información del sensor. Después se conecta a Internet mediante WiFi y envía los valores a Arduino Cloud.

De esta manera podemos observar las mediciones desde una computadora o celular sin depender únicamente del Monitor Serie.

---

# Sensor de temperatura, humedad y presión atmosférica

## ¿Qué hace el sensor?

En esta actividad utilizamos un sensor ambiental conectado al ESP32.

Este sensor permite obtener información del ambiente como:

- Temperatura.
- Humedad.
- Presión atmosférica.

La **temperatura** indica qué tan caliente o frío se encuentra el ambiente y normalmente se mide en grados Celsius (°C).

La **humedad** indica la cantidad de humedad presente en el aire y normalmente se representa mediante un porcentaje (%).

La **presión atmosférica** representa la presión que ejerce el aire y puede expresarse en hectopascales (hPa).

Por ejemplo, se pueden obtener valores como:

```text
Temperatura: 25.4 °C
Humedad: 64 %
Presión: 1011 hPa
```

## Conexión con el ESP32

El sensor se comunica con el ESP32 mediante comunicación I2C.

Las conexiones principales son:

| Sensor | ESP32 |
|---|---|
| VCC | Alimentación |
| GND | GND |
| SDA | GPIO 21 |
| SCL | GPIO 22 |

## Explicación sencilla

El sensor mide las condiciones del ambiente y envía los valores al ESP32.

El ESP32 recibe esta información y puede mostrarla en el Monitor Serie o enviarla mediante WiFi hacia Arduino Cloud.

---

# 6. Visualización de datos en Arduino Cloud

Después de obtener las mediciones del sensor, utilizamos Arduino Cloud para visualizar los datos.

En el Dashboard se pueden mostrar valores como:

```text
Temperatura: 25.4 °C
Humedad: 64 %
Presión atmosférica: 1011 hPa
```

También se pueden utilizar gráficas para observar cómo cambian las mediciones durante un determinado periodo.

## Explicación sencilla

Arduino Cloud recibe los datos enviados por el ESP32 y los muestra en el Dashboard.

Esto facilita la lectura de los valores y permite revisar la información desde otro dispositivo conectado a Internet.

---

#5 Control de un LED desde una página web

## ¿Qué hacemos?

En esta actividad utilizamos el ESP32 para crear una página web sencilla que permite controlar un LED.

Desde el navegador se pueden realizar dos acciones:

- Encender el LED.
- Apagar el LED.

## Código

```cpp
#include <WiFi.h>
#include <WebServer.h>

const char* wifiNombre = "NOMBRE_DE_LA_RED";
const char* wifiClave = "CONTRASEÑA_DE_LA_RED";

const int pinLed = 23;

WebServer servidor(80);

String mostrarPagina() {

  String pagina = R"rawliteral(

  <!DOCTYPE html>
  <html>

  <head>
    <meta charset="UTF-8">
    <title>ESP32 - LED</title>

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

    <p>Elige una opcion</p>

    <a href="/on">
      <button>ENCENDER</button>
    </a>

    <a href="/off">
      <button>APAGAR</button>
    </a>

  </body>

  </html>

  )rawliteral";

  return pagina;
}

void paginaPrincipal() {
  servidor.send(200, "text/html", mostrarPagina());
}

void prenderLed() {

  digitalWrite(pinLed, HIGH);

  Serial.println("LED encendido");

  servidor.send(200, "text/html", mostrarPagina());
}

void apagarLed() {

  digitalWrite(pinLed, LOW);

  Serial.println("LED apagado");

  servidor.send(200, "text/html", mostrarPagina());
}

void setup() {

  Serial.begin(115200);

  pinMode(pinLed, OUTPUT);
  digitalWrite(pinLed, LOW);

  WiFi.begin(wifiNombre, wifiClave);

  Serial.print("Conectando");

  while (WiFi.status() != WL_CONNECTED) {
    Serial.print(".");
    delay(500);
  }

  Serial.println();
  Serial.println("WiFi conectado");

  Serial.print("Direccion IP: ");
  Serial.println(WiFi.localIP());

  servidor.on("/", paginaPrincipal);
  servidor.on("/on", prenderLed);
  servidor.on("/off", apagarLed);

  servidor.begin();

  Serial.println("Servidor iniciado");
}

void loop() {

  servidor.handleClient();
}
```

## Explicación sencilla

Primero el ESP32 se conecta a la red WiFi.

Después inicia un pequeño servidor web y muestra su dirección IP en el Monitor Serie.

Esta dirección IP se escribe en el navegador para abrir la página de control.

Cuando se presiona **ENCENDER**, el ESP32 activa el LED.

Cuando se presiona **APAGAR**, el ESP32 lo desactiva.

---

# . Conclusiones

En este taller aprendimos de manera práctica algunas funciones que puede realizar un ESP32 dentro de un sistema IoT.

Primero utilizamos un potenciómetro para realizar lecturas analógicas y convertir esos valores a voltaje.

También conectamos el ESP32 a una red WiFi, lo que permitió utilizar servicios por Internet.

Luego utilizamos un sensor ambiental para obtener datos de temperatura, humedad y presión atmosférica. Estos valores pudieron visualizarse mediante Arduino Cloud.

Finalmente, se realizó el control de un LED mediante una página web creada desde el mismo ESP32.

Estas actividades permitieron comprender cómo el ESP32 puede recibir información de sensores, procesar datos, conectarse a Internet y controlar dispositivos.
