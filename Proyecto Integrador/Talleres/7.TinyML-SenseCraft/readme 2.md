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
| CABLE | 15 | Cable |
| CELULAR | 15 | Teléfono celular |
| **Total** | **30** | **2 clases** |

![Recolección de imágenes para el entrenamiento](https://github.com/user-attachments/assets/289fa204-64b3-4be7-9826-3e1bd9b55621)

## 4. Creación del modelo

1. Ingresé a SenseCraft AI y conecté el **XIAO ESP32S3 Sense**.
2. Seleccioné la opción para crear un modelo de **clasificación de imágenes**.
3. Creé dos categorías: **CABLE** y **CELULAR**.
4. Capturé y agregué **15 imágenes** a cada una.
5. Inicié el entrenamiento para crear el modelo.
6. Una vez creado, lo probé con la cámara en tiempo real.

## 5. Pruebas del modelo

Se colocaron distintos objetos frente a la cámara para comprobar cómo respondía el clasificador.

### Prueba 1: Cable

Al colocar un cable frente a la cámara, el modelo lo clasificó como **CABLE**, con una confianza del **100 %** en ambas capturas.

![Prueba de clasificación del cable 1](https://github.com/user-attachments/assets/f8614153-c32c-450b-ac62-7212d47bdaac)

![Prueba de clasificación del cable 2](https://github.com/user-attachments/assets/c0ee3397-8c00-4039-a918-b9368284b63b)

### Prueba 2: Celular

Al colocar un celular frente a la cámara, el modelo lo clasificó como **CELULAR**, con confianzas del **91 %** y **96 %** según la captura.

![Prueba de clasificación del celular 1](https://github.com/user-attachments/assets/ef936357-0104-4dc2-8f0b-ee7e966208ed)

![Prueba de clasificación del celular 2](https://github.com/user-attachments/assets/6df83140-80d7-42bb-8f41-cbd1bc0779d2)

## 6. Configuración de una acción mediante GPIO

En la sección **GPIO** configuré una regla para la clase **CELULAR**:

- **Condición:** confianza mayor que 60 %.
- **Salida seleccionada:** LED.
- **Estado predeterminado:** LED apagado.
- **Estado activo:** LED encendido.

La siguiente captura muestra la configuración de la regla. Por sí sola, no demuestra la activación del LED físico.

![Configuración de la condición GPIO](https://github.com/user-attachments/assets/77f8ceb5-018c-41e9-9e6a-1c7ac2766f83)

## 7. Validación de la condición de activación del LED

Se realizó una prueba de la condición configurada para observar la respuesta del LED cuando el modelo reconoce un celular con una confianza superior al umbral establecido.

![Validación de la condición del LED](https://github.com/user-attachments/assets/57f2b919-eeff-4c56-a3a3-075e2497fc41)

## 8. Conclusión

Se creó un modelo de clasificación de imágenes en SenseCraft AI con **dos clases y 30 imágenes de entrenamiento**. En las pruebas registradas, el modelo identificó correctamente el cable y el celular, con niveles de confianza entre **91 % y 100 %**. Además, se configuró una condición GPIO para activar un LED al detectar un celular.

Como mejora futura, se pueden recopilar más imágenes con diferentes fondos, posiciones e iluminaciones, y evaluar el modelo con imágenes nuevas que no hayan sido utilizadas durante el entrenamiento.
