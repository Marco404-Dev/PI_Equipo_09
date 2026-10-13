# Clasificación de objetos con SenseCraft AI

## 1. Objetivo

Crear y probar un modelo de **clasificación de imágenes** en [SenseCraft AI](https://sensecraft.seeed.cc/ai/model) para diferenciar dos objetos: **cables** y **celulares**, utilizando el dispositivo **XIAO ESP32S3 Sense**.

## 2. Herramientas utilizadas

- Plataforma: SenseCraft AI.
- Dispositivo: XIAO ESP32S3 Sense con cámara.
- Objetos de prueba: un cable y un celular.
- Datos de entrenamiento: **30 imágenes**, distribuidas en dos clases.

## 3. Recolección de imágenes

Se crearon dos categorías en la plataforma y se capturaron **15 imágenes por clase** desde la cámara conectada.

| Clase | Cantidad de imágenes | Objeto |
|---|---:|---|
| CABLE / Cables | 15 | Cable |
| CELULAR / Celular | 15 | Teléfono celular |
| **Total** | **30** | **2 clases** |

<img width="1802" height="650" alt="tomarfotos" src="https://github.com/user-attachments/assets/289fa204-64b3-4be7-9826-3e1bd9b55621" />


## 4. Creación del modelo

1. Ingresé a SenseCraft AI y conecté el **XIAO ESP32S3 Sense**.
2. Seleccioné la opción para crear un modelo de **clasificación de imágenes**.
3. Creé dos categorías: **CABLE** y **CELULAR**.
4. Capturé y agregué **15 imágenes** a cada una.
5. Inicié el proceso de entrenamiento para crear el modelo.
6. Una vez creado, lo probé con la cámara en tiempo real.


## 5. Pruebas del modelo

Se mostraron diferentes objetos frente a la cámara para comprobar cómo respondía el clasificador.

### Prueba 1: Cable

En esta prueba se colocó un cable frente a la cámara. El modelo clasificó la imagen como **CABLE** con una confianza de **100 %** en las capturas.

<img width="1565" height="857" alt="prueba1 2" src="https://github.com/user-attachments/assets/f8614153-c32c-450b-ac62-7212d47bdaac" />

<img width="1577" height="852" alt="prueba1" src="https://github.com/user-attachments/assets/c0ee3397-8c00-4039-a918-b9368284b63b" />


### Prueba 2: Celular

Se colocó un celular frente a la cámara. El modelo asignó a la clase **CELULAR** confianzas de **91 %** y **96 %**, según la captura.

<img width="1550" height="842" alt="prueba2 2" src="https://github.com/user-attachments/assets/ef936357-0104-4dc2-8f0b-ee7e966208ed" />

<img width="1587" height="862" alt="prueba2 1" src="https://github.com/user-attachments/assets/6df83140-80d7-42bb-8f41-cbd1bc0779d2" />


## 6. Configuración de una acción mediante GPIO

Además, en la sección **GPIO** se configuró una regla para el objeto **CELULAR**:

- **Condición:** confianza mayor que 60.
- **Salida seleccionada:** LED.
- **Estado predeterminado:** LED apagado.
- **Estado activo:** LED encendido.

Esta captura documenta la configuración de la regla; por sí sola no demuestra que el LED físico se haya encendido.

<img width="1748" height="650" alt="gpio" src="https://github.com/user-attachments/assets/77f8ceb5-018c-41e9-9e6a-1c7ac2766f83" />

## 7. Validación de la condición de activación del LED

<img width="899" height="1599" alt="validacion" src="https://github.com/user-attachments/assets/57f2b919-eeff-4c56-a3a3-075e2497fc41" />


## 8. Conclusión

Se creó un modelo de clasificación de imágenes en SenseCraft AI usando **dos clases y 30 muestras en total**. Durante las pruebas con la cámara, el modelo identificó correctamente el cable y el celular en las capturas registradas, con confianzas de **91 % a 100 %**. También se configuró una condición de salida GPIO asociada a la detección de un celular.

Como mejora futura, sería conveniente recopilar más imágenes con distintos fondos, posiciones e iluminaciones y evaluar el modelo con ejemplos que no se hayan utilizado durante el entrenamiento.
