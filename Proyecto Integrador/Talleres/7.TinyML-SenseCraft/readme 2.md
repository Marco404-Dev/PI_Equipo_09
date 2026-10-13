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

![Recolección de muestras para ambas clases](imagenes/tomarfotos.png)

## 4. Creación del modelo

1. Ingresé a SenseCraft AI y conecté el **XIAO ESP32S3 Sense**.
2. Seleccioné la opción para crear un modelo de **clasificación de imágenes**.
3. Creé dos categorías: **CABLE** y **CELULAR**.
4. Capturé y agregué **15 imágenes** a cada una.
5. Inicié el proceso de entrenamiento para crear el modelo.
6. Una vez creado, lo probé con la cámara en tiempo real.

> Nota: esta práctica utiliza un modelo de **clasificación**. A diferencia de uno de detección de objetos, su salida indica a qué clase corresponde la imagen y qué confianza asigna a cada clase.

## 5. Pruebas del modelo

Se mostraron diferentes objetos frente a la cámara para comprobar cómo respondía el clasificador.

### Prueba 1: Cable

En esta prueba se colocó un cable frente a la cámara. El modelo clasificó la imagen como **CABLE** con una confianza de **100 %** en las capturas.

![Resultado de clasificación del cable, primera captura](imagenes/prueba1.2.png)

![Resultado de clasificación del cable, segunda captura](imagenes/prueba1(1).png)

### Prueba 2: Celular

Se colocó un celular frente a la cámara. El modelo asignó a la clase **CELULAR** confianzas de **91 %** y **96 %**, según la captura.

![Resultado de clasificación del celular con 91 %](imagenes/prueba2.1.png)

![Resultado de clasificación del celular con 96 %](imagenes/prueba2.2.png)

### Resumen de los resultados observados

| Objeto presentado | Clase predicha | Confianza observada |
|---|---|---|
| Cable | CABLE | 100 % |
| Celular | CELULAR | 91 % |
| Celular | CELULAR | 96 % |

> Estos porcentajes indican la **confianza de la predicción en esas capturas**, no la precisión general del modelo. Para medir su precisión harían falta más imágenes de prueba independientes.

## 6. Configuración de una acción mediante GPIO

Además, en la sección **GPIO** se configuró una regla para el objeto **CELULAR**:

- **Condición:** confianza mayor que 60.
- **Salida seleccionada:** LED.
- **Estado predeterminado:** LED apagado.
- **Estado activo:** LED encendido.

Esta captura documenta la configuración de la regla; por sí sola no demuestra que el LED físico se haya encendido.

![Regla GPIO configurada para la clase CELULAR](imagenes/gpio.png)

## 7. Conclusión

Se creó un modelo de clasificación de imágenes en SenseCraft AI usando **dos clases y 30 muestras en total**. Durante las pruebas con la cámara, el modelo identificó correctamente el cable y el celular en las capturas registradas, con confianzas de **91 % a 100 %**. También se configuró una condición de salida GPIO asociada a la detección de un celular.

Como mejora futura, sería conveniente recopilar más imágenes con distintos fondos, posiciones e iluminaciones y evaluar el modelo con ejemplos que no se hayan utilizado durante el entrenamiento.
