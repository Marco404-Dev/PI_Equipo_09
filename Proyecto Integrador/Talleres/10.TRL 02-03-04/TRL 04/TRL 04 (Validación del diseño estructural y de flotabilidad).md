---
_PROYECTO INTEGRADOR 2026-II_
---

# Yakutoring, Informe técnico

| **Campo** | **Información** |
|:---|----|
| Institución | Universidad Peruana Cayetano Heredia (UPCH) |
| Equipo | Equipo 09 --- Proyecto Integrador |
| Área de aplicación | Monitoreo de calidad del agua en ecosistemas de manglar de Tumbes, Perú |
| Nivel objetivo | TRL 4: validación en laboratorio mediante pruebas de baja fidelidad |
| Tipo y versión | Validación del diseño estructural y de flotabilidad • Borrador v1 |
| Fecha de elaboración | 7 de noviembre de 2026 |

### **1. Resumen**

En esta etapa se desarrolló y evaluó el diseño físico de la boya, considerando la distribución de los componentes, sus dimensiones, el material del prototipo y las condiciones de flotabilidad y estabilidad. Asimismo, se realizaron simulaciones mediante SimScale para analizar el comportamiento estructural de la geometría frente a las cargas consideradas en el diseño.

La validación experimental se realizará inicialmente en laboratorio mediante pruebas de flotabilidad, estabilidad, funcionamiento de los sensores y comunicación LoRa. Las pruebas en el laboratorio y/o en el campo de estudio (Pantanos de Villa), como la exposición prolongada a las condiciones ambientales y la evaluación de autonomía serán abordadas en etapas posteriores.

### **2. Objetivos**

### **2.1 Objetivo general**

Desarrollar y realizar una validación preliminar en laboratorio del prototipo de la boya YakuToring, mediante la evaluación de su diseño físico, flotabilidad, comportamiento estructural, integración de sensores y comunicación LoRa.

### **2.2 Objetivos específicos**

- Diseñar la geometría y distribución interna de la boya, considerando la ubicación de los sensores, componentes electrónicos, sistema de alimentación y elementos de comunicación.
- Determinar las condiciones teóricas de flotabilidad de la boya mediante el principio de Arquímedes, considerando la masa total del prototipo y el volumen desplazado.
- Evaluar mediante SimScale el comportamiento estructural de la boya frente a las cargas consideradas en el diseño, analizando parámetros como esfuerzos de Von Mises y desplazamientos, según los resultados disponibles.
- Comprobar experimentalmente la flotabilidad y estabilidad del prototipo mediante pruebas controladas en laboratorio.
- Integrar y verificar el funcionamiento de los sensores de temperatura, pH y conductividad, así como del sensor ambiental, registrando las mediciones obtenidas.
- Verificar la comunicación entre la unidad transmisora y receptora mediante LoRa, evaluando la recepción e integridad de los datos transmitidos.
- Comparar los resultados obtenidos mediante cálculos teóricos, simulaciones y pruebas físicas para identificar el desempeño, alcance y principales limitaciones del prototipo.

### **3. Diseño técnico definitivo de la boya.**

| **Sección** | **Componente** | **Descripción** |
|:----|----|----|
| Superior | Panel solar, Heltec WiFi LoRa V4 (Antena) | Se encuentra el panel solar, encargado de captar energía para alimentar el sistema y contribuir a la autonomía de la boya. Además, incorpora la antena de comunicación LoRa, que permite transmitir inalámbricamente los datos recopilados hacia la estación receptora. |
| Intermedio | BME280, Heltec WiFi LoRa V4, | Contiene la unidad de procesamiento y adquisición de datos, encargada de recibir y organizar las lecturas de los sensores. El módulo BME280 permite registrar la temperatura, humedad y presión atmosférica del entorno. |
| Inferior | DS18B20, sonda pH, sensor de conductividad/TDS | Aloja los sensores destinados al monitoreo de las condiciones fisicoquímicas del agua. Esta sección cuenta con dos subsecciones que permiten el contacto directo de los sensores con el medio y, al mismo tiempo, aíslan las secciones superiores para evitar el ingreso de agua y humedad hacia los componentes electrónicos. |

### **4. Características y dimensiones**

  <img width="3508" height="2480" alt="Parte 01 y 02" src="https://github.com/user-attachments/assets/5c1090f4-e7d0-411e-8fc7-d73005f0b8b2" />
  
  <img width="3508" height="2480" alt="Cinturón, tuerca y tornillo" src="https://github.com/user-attachments/assets/66570f9a-4ee1-4866-a7fe-79d1020e0ad1" />
  
  <img width="3508" height="2480" alt="Tapa de la boya" src="https://github.com/user-attachments/assets/6233363c-899e-4b0b-9914-0397cc29d4e6" />
  
  <img width="3508" height="2480" alt="Cuerpo de boya" src="https://github.com/user-attachments/assets/15249a89-82c0-4bc8-b2ab-adc58d6397b2" />


### **5. Selección de material**

Inicialmente, se planteó utilizar polietileno de alta densidad (HDPE) para la fabricación definitiva de la boya, considerando las condiciones ambientales a las que estaría expuesta durante su funcionamiento. Sin embargo, debido a que en esta etapa se presentará un prototipo funcional elaborado mediante impresión 3D, se optó por utilizar PLA, facilitando la fabricación y reproducción de la geometría diseñada. Si bien, el HDPE se mantiene como material previsto para el producto final, el PLA se empleará exclusivamente para la elaboración del prototipo.

### **6. Evaluación de flotabilidad y estabilidad**

La flotabilidad de la boya ManglarLab se evaluó mediante el principio de Arquímedes, el cual establece que todo cuerpo sumergido parcial o totalmente en un fluido experimenta un empuje vertical hacia arriba equivalente al peso del fluido desplazado [4].

|          **Parámetro**           | **Valor**     |
|:--------------------------------:|---------------|
|        Masa de estructura        | 3236.91679 g  |
| Masa de los componentes internos |    283.7 g    |
|            Masa total            | 3520.61679 g  |
|    Volumen del espacio hueco     | 0.01104772 m³ |
|       Volumen del material       | 0.00259943 m³ |
|          Volumen total           | 0.01364715 m³ |

Según el principio de Arquimides: Empuje = Peso = masa total x gravedad (9.81 m/s^2$$)

$$\rho_{\text{agua}} \cdot g \cdot V_{\text{desplazado}} = m_{\text{total}} \cdot g$$

$$V_{\text{desplazado}} = \frac{m_{\text{total}}}{\rho_{\text{agua}}}$$

$$V_{\text{desplazado}} = \frac{3520.61679\ kg}{1000\text{~kg/m}^{3}}$$

$$V_{\text{desplazado}} = 0.00352062\ \text{m}^{3} = 3.52062\ L$$

Al comparar el volumen total con el volumen desplazado, observamos que el volumen de la boya es superior al desplazado. Por tanto, la boya cuenta con condiciones favorables para poder flotar.

### 6.1. Cinturón de sujeción y unión al sistema de anclaje

El diseño de la boya incorpora un cinturón de sujeción en forma de aro, dispuesto alrededor de una sección de la estructura, cuya función principal es establecer la unión entre la boya y el sistema de anclaje. Este elemento permite mantener la boya aproximadamente en una posición determinada, proporcionando libertad de giro relativa entre la boya y el cinturón ante la acción de fuerzas ambientales, como el viento, las corrientes de agua y el oleaje.

Para la evaluación de flotabilidad, el cinturón se considera parte de la masa total del sistema. El cinturón presenta una masa de 0.82017 kg y un volumen de 0.00108464 m³, mientras que el volumen de agua requerido para compensar su peso es de aproximadamente 0.00082017 m³, equivalente al 75.62 % de su volumen. Por tanto, presenta flotabilidad positiva.

Finalmente, se plantea verificar experimentalmente que el cinturón mantenga la conexión con la boya y el sistema de anclaje, además, de permitir el giro de la boya y que no genere interferencias significativas con la flotación o estabilidad del sistema.

<img width="877" height="722" alt="image" src="https://github.com/user-attachments/assets/d6550b80-9553-440f-9699-2f352b12ce37" />

### **7. Análisis estructural mediante SimScale**

### **7.1. Cargas consideradas en el análisis**

| **Tipo de carga** |	**Cantidad** |	**Objetivo** |
|:------------------|------------------------|---------------|
| Fuerza de arrastre |	0.62 N - 0.6.93 N	| Se evaluará los esfuerzos por resistencia al flujo de la superficie expuesta al agua, considerando diferentes velocidades de corriente. |
| Presión hidrostática | 1.815 kPa | Se evaluará los esfuerzos producidos por la presión del agua sobre la superficie sumergida de la boya. |

Para el cálculo de la fuerza de arrastre se tomó como referencia el artículo de investigación [5], del cual se consideró la siguiente fórmula:
$$F_D = \frac{1}{2} C_d \, \rho \, A \, v^2$$
Asimismo, se adoptó un coeficiente de arrastre **$C_d$** de **1,01** para el análisis y una velocidad de arrastre **$V$** de entre **0.15-0.5 m/s**. A partir de estos valores, se consideraron las fuerzas de arrastre de 0.62 N y 6.93 N, correspondientes a las condiciones de menor y mayor velocidad, respectivamente.

### **7.2. Resultados: SimScale**

- Presión hidrostática

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/347f3a8b-5e32-4f7a-8d17-77e55b405f44" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/2daf2272-33bb-4a72-a53d-59bf4158088a" />

 - Esfuerzos de Von Mises: Se muestra que, bajo una presión hidrostática de 1.815 kPa, los esfuerzos se mantienen bajos en la mayor parte de la estructura, mientras que las mayores concentraciones de esfuerzo se localizan principalmente en las zonas de cambio de geometría y unión. Estos esfuerzos elevados elevados se concentran en la parte superior, indicando mayor deformidad.

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/4a450cdc-c670-43ce-9342-271b84a95c4a" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/e439354c-5a38-4f46-85cb-7a32f7a516fa" />
  
 - Esfuerzos de desplazamiento: La boya presenta pequeños desplazamientos en la mayor parte de su geometría y las mayores magnitudes se concentran en la parte superior de la boya (tapa). Esto indica que la geometría mantiene una adecuada rigidez frente a la condición de presión analizada en la mayor parte de su sistema, pero la tapa constituye la región con mayor desplazamiento.
   
- Fuerza de arrastre




### **8. Evaluación de estabilidad y comportamiento esperado**



Aquí relacionas los resultados de flotabilidad + SimScale y explicas qué indican sobre el comportamiento esperado de la boya.

### **9. Validación experimental prevista**

Finalmente señalas que los resultados teóricos y computacionales serán contrastados con pruebas físicas del prototipo impreso en PLA.

## Referencias

[1] CONCYTEC, «Directiva N.º 001-2022-CONCYTEC-P: Uso de la metodología nivel de madurez tecnológica (TRL)», Resolución de Presidencia N.º 020-2022-CONCYTEC-P, Lima, Perú, 2022. Disponible: https://vinculate.concytec.gob.pe/wp-content/files/RP-020-2022-CONCYTEC-P.pdf

[2] G. Espinoza Yauri, «TRL 2, 3 y 4: Investigación aplicada», material de clase, Oficina de Transferencia Tecnológica y Vinculación Empresarial, UPCH, diapositivas 14--16, 2026.

[3] Oficina de Ciencias y Tecnología de la Tierra de la NASA, «Niveles de preparación tecnológica (TRL)». Disponible en: https://esto.nasa.gov/trl/ (consulta: 1 nov. 2026).

[4] C. V. Peñaranda Osorio, Mecánica de fluidos. Bogotá: Ecoe Ediciones, 2018. pp. 54-56 [En Línea] Disponible en: https://elibro.net/es/lc/cayetano/titulos/122458

[5] M. Yoshikai et al., «Field Measurement and Prediction of Drag in a Planted Rhizophora Mangrove Forest», Journal of Geophysical Research: Oceans, vol. 127, n.o 11, p. e2021JC018320, 2022, doi: 10.1029/2021JC018320.
