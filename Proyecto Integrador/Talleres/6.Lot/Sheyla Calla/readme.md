## TALLER DE INTERNET DE LAS COSAS (IoT)
### 1. Introducción y Objetivos:
Durante este taller exploramos de forma práctica y teórica los fundamentos del Internet de las Cosas (IoT), comprendiendo cómo los dispositivos recopilan información del entorno físico para transformarla en datos útiles y procesables en la nube.   
Los objetivos principales que abordamos fueron:
- Configurar y programar microcontroladores y tarjetas de desarrollo orientadas a IoT.   
- Conectar sensores físicos para capturar variables como temperatura, luz o movimiento.
- Enviar y monitorear datos en tiempo real mediante protocolos de comunicación como Wi-Fi y MQTT hacia plataformas en la nube (Arduino Cloud).
### 2. Desarrollo del Taller
### Actividad 1: Lectura del potenciómetro
En esta primera etapa nos familiarizamos con el microcontrolador ESP32, acompañado del kit de sensores. El objetivo principal fue entender cómo un dispositivo electrónico logra "leer" el mundo físico.

Para hacerlo de forma práctica, trabajamos con un potenciómetro (una perilla que varía la resistencia) siguiendo estos pasos:

1. Lectura Analógica: El ESP32 tiene un componente interno llamado conversor analógico-digital (ADC). Su función es capturar la señal física del potenciómetro y convertirla en números que la placa pueda entender.

2. Conversión a Voltaje: Como esos números por sí solos no nos dicen mucho, aplicamos una fórmula matemática en nuestro código para convertir esos valores a voltaje real (por ejemplo, de 0 a 3.3 voltios).

3. Visualización: Comprobamos que todo funcionaba al ver cómo variaba el voltaje directamente en la pantalla de nuestra computadora a través del "Monitor Serial" de Arduino, mientras girábamos la perilla.
<img width="1080" height="627" alt="image" src="https://github.com/user-attachments/assets/47240e43-5da3-4443-b811-63c1d589ceab" />
<img width="1600" height="885" alt="image" src="https://github.com/user-attachments/assets/61e799bd-9428-470c-8763-5c3d46a2c721" />

### Actividad 2: Conectividad Wi-Fi
Una vez comprendida la adquisición de datos, el siguiente paso fue dotar de conectividad al microcontrolador. Utilizamos las librerías de red del ESP32 para escanear los puntos de acceso (Wi-Fi) disponibles en el entorno. Luego, logramos conectar el dispositivo a una red local (como el hotspot de un celular), obteniendo una dirección IP que confirmó la conexión exitosa a internet.

### Actividad 3: Monitoreo en tiempo real con Arduino Cloud
Para esta tercera actividad, dimos el salto a internet utilizando específicamente la plataforma Arduino Cloud. El objetivo era sencillo: lograr que los datos físicos que estaba leyendo nuestro ESP32 (como el voltaje del potenciómetro) se enviaran a la nube para poder verlos desde cualquier lugar.

Para hacerlo fácil de entender, los pasos que seguimos fueron:

1. Vinculamos nuestro ESP32 a la plataforma de Arduino Cloud.

2. Creamos "variables" virtuales que representaban los datos de nuestro sensor físico.

3. Diseñamos un panel de control (Dashboard) en la web con indicadores visuales, como gráficos de líneas y medidores.

El resultado fue que pudimos ver cómo cambiaban los valores de nuestro sensor en tiempo real y a distancia directamente desde el navegador, demostrando de forma muy visual y práctica cómo funciona el monitoreo remoto en el Internet de las Cosas.
<img width="1600" height="818" alt="image" src="https://github.com/user-attachments/assets/2896ec65-64e0-4221-a1e1-7d8ad24f3e4a" />
<img width="1600" height="829" alt="image" src="https://github.com/user-attachments/assets/fe50f4a1-1c8d-45b4-9e73-bbbdb1bf6e6b" />
<img width="1136" height="566" alt="image" src="https://github.com/user-attachments/assets/c1ca17b5-d9b3-4305-8a74-e40fee28f49e" />

### Actividad 4: implementación del Protocolo MQTT
En esta etapa conocimos el protocolo MQTT. Lo interesante de este protocolo es que es muy rápido, ligero e ideal para enviar datos pequeños, como los de nuestros sensores.

Para entenderlo fácilmente, trabajamos con el modelo de "Publicación y Suscripción", que funciona casi como un grupo de chat o un canal de videos:

1. El Broker: Es el servidor central que funciona como un "cartero" o intermediario. Se encarga de recibir todos los mensajes y repartirlos a quien corresponda.

2. Publicar (Publish): Nuestro ESP32 enviaba los datos del sensor hacia un tema o "tópico" específico dentro del Broker.

3. Suscribir (Subscribe): A su vez, nuestro dispositivo podía "escuchar" un tópico para recibir órdenes, como por ejemplo, el comando para encender o apagar un LED remotamente.
<img width="1460" height="730" alt="image" src="https://github.com/user-attachments/assets/55eba530-2f23-4c57-8d8d-c22c9d78b1f4" />
<img width="1271" height="622" alt="image" src="https://github.com/user-attachments/assets/5b078fad-521a-4b60-a3ee-323ba3a8b5f1" />

### Actividad 5: Creación de un proyecto visual con Node-RED
Como gran cierre del taller, unimos todo lo aprendido usando Node-RED. Esta es una herramienta fantástica porque nos permite programar de manera visual: en lugar de escribir líneas de código complicadas, simplemente arrastramos y unimos "bloques" (nodos) con flechas en la pantalla.

Los pasos que realizamos fueron:

1. Conectamos Node-RED a nuestro Broker MQTT utilizando nuestras credenciales de equipo (upch/equipoX).

2. Creamos un "flujo" donde los datos que llegaban del ESP32 se dirigían hacia elementos gráficos.

3. Construimos nuestro propio Dashboard (Panel de control) interactivo. Aquí integramos botones e indicadores visuales para monitorear nuestro sensor y controlar el hardware a distancia de forma muy profesional.
<img width="470" height="415" alt="image" src="https://github.com/user-attachments/assets/d8d44923-0b01-4bbf-96d0-eb0c28a50f08" />

### 3. Conclusiones
Las cinco actividades permitieron un aprendizaje progresivo: desde el manejo básico de componentes electrónicos hasta la integración de sistemas complejos de IoT.

El ESP32 demostró ser una herramienta fundamental gracias a su capacidad de procesamiento y su módulo Wi-Fi integrado, ideal para usar protocolos como MQTT.

Herramientas visuales y en la nube, como Node-RED, facilitan enormemente la creación de interfaces de usuario para monitorear y controlar entornos físicos desde cualquier parte del mundo.
