# Clasificación de piedra, papel y tijera con SenseCraft AI

## 1. Objetivo

Crear y probar un modelo de **clasificación de imágenes** en [SenseCraft AI](https://sensecraft.seeed.cc/ai/model) para reconocer tres gestos de la mano: **piedra, papel y tijera**, utilizando la cámara del **XIAO ESP32S3 Sense**.

## 2. Herramientas utilizadas

- Plataforma: SenseCraft AI.
- Dispositivo: XIAO ESP32S3 Sense con cámara.
- Clases del modelo: **PIEDRA**, **PAPEL** y **TIJERA**.
- Imágenes de entrenamiento: fotografías de cada gesto capturadas con la cámara.

## 3. Recolección de imágenes

Se crearon tres categorías para entrenar el modelo, cada una correspondiente a un gesto diferente.

| Clase | Gesto |
|---|---|
| PIEDRA | Puño cerrado |
| PAPEL | Mano abierta |
| TIJERA | Dos dedos extendidos en forma de V |

**Captura de las tres clases y sus imágenes de entrenamiento:**

<!-- Reemplaza la línea siguiente por la imagen subida a GitHub -->
![Recolección de imágenes de piedra, papel y tijera](URL_DE_IMAGEN_RECOLECCION)

## 4. Creación del modelo

1. Ingresé a [SenseCraft AI](https://sensecraft.seeed.cc/ai/model).
2. Conecté el **XIAO ESP32S3 Sense** a la plataforma.
3. Seleccioné la opción para crear un modelo de **clasificación de imágenes**.
4. Creé tres clases: **PIEDRA**, **PAPEL** y **TIJERA**.
5. Capturé imágenes de los tres gestos para utilizarlas como datos de entrenamiento.
6. Inicié el entrenamiento para generar el modelo.
7. Probé el modelo mostrando los gestos frente a la cámara.

**Captura del modelo creado:**

![Modelo de tres clases](URL_DE_IMAGEN_MODELO)

## 5. Pruebas del modelo

Se mostraron los tres gestos frente a la cámara para observar la clasificación realizada por el modelo.

### Prueba 1: Piedra

Se mostró un **puño cerrado** frente a la cámara para comprobar si el modelo lo reconocía como **PIEDRA**.

<img width="1600" height="900" alt="WhatsApp Image 2026-10-13 at 6 12 15 PM" src="https://github.com/user-attachments/assets/97e498c4-aad0-4f38-920b-bc28bb718961" />

<img width="1600" height="900" alt="WhatsApp Image 2026-10-13 at 6 12 16 PM (5)" src="https://github.com/user-attachments/assets/a9c9c475-e6ca-445f-9b07-83d99e0e1442" />




### Prueba 2: Papel

Se mostró una **mano abierta** frente a la cámara para comprobar si el modelo la reconocía como **PAPEL**.

<img width="1600" height="900" alt="WhatsApp Image 2026-10-13 at 6 12 16 PM" src="https://github.com/user-attachments/assets/716c902e-297b-44df-9aaf-3228b8d03a52" />

<img width="1600" height="900" alt="WhatsApp Image 2026-10-13 at 6 15 59 PM (1)" src="https://github.com/user-attachments/assets/cfefb204-4edc-40c3-a953-e1889f7f5cb7" />




### Prueba 3: Tijera

Se mostraron **dos dedos extendidos en forma de V** frente a la cámara para comprobar si el modelo los reconocía como **TIJERA**.

<img width="1600" height="900" alt="WhatsApp Image 2026-10-13 at 6 12 16 PM (1)" src="https://github.com/user-attachments/assets/28344aba-5c92-40cc-b073-57840ca93848" />

<img width="1600" height="900" alt="WhatsApp Image 2026-10-13 at 6 12 16 PM (4)" src="https://github.com/user-attachments/assets/771d79e5-de54-4f46-9d71-e01207e47902" />


## 6. Resultados

Registrar las confianzas que aparezcan durante las pruebas:

| Gesto mostrado | Clase predicha | Confianza |
|---|---|---|
| Piedra | Pendiente de registrar | — |
| Papel | Pendiente de registrar | — |
| Tijera | Pendiente de registrar | — |

## 7. Conclusión

Se desarrolló una práctica de **clasificación de imágenes** con tres categorías: piedra, papel y tijera, utilizando **SenseCraft AI** y el **XIAO ESP32S3 Sense**. Este ejercicio permite comprender cómo se recopilan imágenes, se entrena un modelo y se realizan predicciones mediante una cámara.

Como mejora, se pueden agregar imágenes de distintas personas, fondos, distancias e iluminaciones para evaluar si el modelo reconoce correctamente los gestos en situaciones diferentes.

> **Nota:** Reemplazar `URL_DE_IMAGEN_...` por los enlaces de las capturas subidas a GitHub y completar la tabla de resultados con los valores observados.
