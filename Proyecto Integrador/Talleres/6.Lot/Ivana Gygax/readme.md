#Taller de Internet de las Cosas (IoT) Descripción 

El taller aborda los fundamentos teóricos y prácticos del Internet de las Cosas (IoT) mediante el uso de microcontroladores, sensores, redes inalámbricas y plataformas en la nube. Se trabaja principalmente con el ESP32, realizando adquisición, procesamiento y transmisión de datos.

##Objetivos 
Comprender los fundamentos del Internet de las Cosas
Configurar y programar dispositivos ESP32 y Arduino. 
Adquirir datos mediante sensores de temperatura, humedad, luz y movimiento. 
Establecer comunicación mediante Wi-Fi y MQTT. 
Enviar y visualizar datos en plataformas IoT como Arduino Cloud, ThingSpeak y Ubidots. 
Implementar sistemas básicos de monitoreo y control remoto. 
Hardware y componentes 

##Componentes

ESP32 Dev Kit 1 
Arduino Explore IoT Kit 
Kit de sensores Keystudio 48 en 1 
Protoboard 
Multímetro 

##Funcionalidad
El ESP32 permite adquirir señales provenientes de sensores y procesarlas mediante sus entradas digitales y analógicas.

Adquisición de datos 

La adquisición de datos consiste en capturar información del entorno mediante sensores y convertirla en señales que puedan ser procesadas por un microcontrolador.

##Flujo general

Sensor → ESP32 → Procesamiento → Comunicación → Plataforma IoT 

##Sensores utilizados

DHT22: temperatura y humedad. LDR: intensidad luminosa. PIR: detección de movimiento. MQ-2: detección de gases. 

Como primera aplicación se realizó la lectura de un potenciómetro mediante el ADC del ESP32, utilizando analogRead() y mostrando los valores mediante el monitor serial. Posteriormente, se planteó mejorar la lectura mediante promediado y conversión de los valores ADC a voltaje.

##Código y salidas



##Comunicación Wi-Fi 

La biblioteca WiFi.h permite establecer conectividad inalámbrica con el ESP32, posibilitando la conexión a redes, el intercambio de datos y la comunicación con servidores.

Una de las actividades consistió en utilizar un teléfono móvil como Hotspot Wi-Fi, conectar el ESP32 a la red y visualizar la dirección IP asignada en el monitor serial.

##Plataformas IoT 

El taller presenta diferentes plataformas para almacenar, visualizar y gestionar datos provenientes de dispositivos IoT, entre ellas:

Arduino Cloud ThingSpeak Ubidots AWS IoT Microsoft Azure IoT ThingsBoard 

Se plantea enviar datos del potenciómetro y de sensores del kit Keystudio a Arduino Cloud, ThingSpeak y Ubidots, permitiendo observar las variaciones de las variables en tiempo real.

##Protocolo MQTT 

MQTT (Message Queuing Telemetry Transport) es un protocolo ligero de comunicación basado en el modelo publicación/suscripción, especialmente utilizado en aplicaciones IoT donde se requiere bajo consumo de recursos y ancho de banda.

Sus conceptos principales son:

Topic: dirección utilizada para identificar los mensajes. Publish: envío de mensajes. Subscribe: recepción de mensajes asociados a un topic. Broker: servidor encargado de recibir, filtrar y distribuir los mensajes entre clientes. 

Los puertos MQTT indicados en el taller son:

Puerto Uso 1883 MQTT estándar sin cifrado 8883 MQTT mediante TLS/SSL 8080 MQTT sobre WebSockets 8081 MQTT sobre WebSockets con TLS/SSL 9001 MQTT WebSockets Node-RED 

Node-RED es una herramienta de programación basada en flujos que permite integrar dispositivos, APIs y servicios mediante una interfaz gráfica basada en navegador.

En conjunto con MQTT, puede actuar como intermediario entre los dispositivos IoT y las aplicaciones, permitiendo recibir datos, procesarlos y enviar comandos en tiempo real.

Su aplicación en entornos industriales permite desarrollar sistemas de monitoreo, control y automatización, especialmente dentro de aplicaciones relacionadas con Industria 4.0 e IoT.

Actividades principales 

Durante el taller se plantean las siguientes actividades:

Lectura y promediado de datos de un potenciómetro. Conversión de valores ADC a voltaje. Conexión del ESP32 a una red Wi-Fi. Envío de datos a plataformas IoT. Lectura de sensores del kit Keystudio. Visualización de datos en tiempo real. Control remoto de un LED desde una plataforma IoT. Comunicación mediante MQTT. Implementación de flujos utilizando Node-RED. Conclusiones 

El taller permite integrar los principales elementos de un sistema IoT: sensores, microcontroladores, adquisición de datos, conectividad, protocolos de comunicación, plataformas en la nube y herramientas de visualización y control. El ESP32 constituye el elemento central para adquirir y transmitir información, mientras que MQTT y Node-RED permiten establecer una arquitectura de comunicación y procesamiento de datos adecuada para aplicaciones de monitoreo y automatización.

Tecnologías utilizadas ESP32 Arduino C/C++ Wi-Fi MQTT Node-RED Arduino Cloud ThingSpeak Ubidots IoT Industria 4.0 
