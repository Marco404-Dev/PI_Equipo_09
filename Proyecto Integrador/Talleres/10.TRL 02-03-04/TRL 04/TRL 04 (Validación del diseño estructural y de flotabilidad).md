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

La validación experimental se realizará inicialmente en laboratorio mediante pruebas de flotabilidad, estabilidad, funcionamiento de los sensores y comunicación LoRa. La instalación en el campo de estudio (Pantanos de Villa), la exposición prolongada a las condiciones ambientales y la evaluación de autonomía serán abordadas en etapas posteriores.

### **2. Fundamento y alcance de TRL 4**

Según la Directiva N.º 001-2022-CONCYTEC-P, el TRL 4 exige integrar componentes básicos y comprobarlos mediante ensayos de baja fidelidad en laboratorio [1]. Esta definición coincide con el material de clase de la UPCH [2] y la escala de NASA [3].

| **Indicador TRL 4** | **Evidencia que generará *YakuToring*** |
|---|---|
| Diseño integrado del prototipo | Diseño CAD de la boya, distribución de sensores, componentes electrónicos, batería y panel solar. |
|Integración de componentes básicos	| Integración de sensores, Heltec WiFi LoRa V4, sistema de alimentación y comunicación LoRa. |
| Evaluación del comportamiento físico | Cálculos teóricos de flotabilidad mediante el principio de Arquímedes y análisis de la geometría de la boya. |
| Análisis mediante simulación | Simulaciones en *SimScale* para evaluar esfuerzos, desplazamientos y comportamiento de la estructura frente a las cargas consideradas. |
| Pruebas de baja fidelidad | Pruebas de flotabilidad, estabilidad, funcionamiento de sensores y comunicación en condiciones controladas de laboratorio. |
| Resultados experimentales | Registros de las pruebas, fotografías, mediciones obtenidas y comparación con los resultados teóricos y de simulación. |

### **3. Objetivos**

### **3.1 Objetivo general**

Desarrollar y realizar una validación preliminar en laboratorio del prototipo de la boya YakuToring, mediante la evaluación de su diseño físico, flotabilidad, comportamiento estructural, integración de sensores y comunicación LoRa.

### **3.2 Objetivos específicos**

- Diseñar la geometría y distribución interna de la boya, considerando la ubicación de los sensores, componentes electrónicos, sistema de alimentación y elementos de comunicación.
- Determinar las condiciones teóricas de flotabilidad de la boya mediante el principio de Arquímedes, considerando la masa total del prototipo y el volumen desplazado.
- Evaluar mediante SimScale el comportamiento estructural de la boya frente a las cargas consideradas en el diseño, analizando parámetros como esfuerzos de Von Mises, desplazamientos y factor de seguridad, según los resultados disponibles.
- Comprobar experimentalmente la flotabilidad y estabilidad del prototipo mediante pruebas controladas en laboratorio.
- Integrar y verificar el funcionamiento de los sensores de temperatura, pH y conductividad, así como del sensor ambiental, registrando las mediciones obtenidas.
- Verificar la comunicación entre la unidad transmisora y receptora mediante LoRa, evaluando la recepción e integridad de los datos transmitidos.
- Comparar los resultados obtenidos mediante cálculos teóricos, simulaciones y pruebas físicas para identificar el desempeño, alcance y principales limitaciones del prototipo.

### **4. Diseño técnico definitivo de la boya.**

| **Sección** | **Componente** | **Descripción** |
|:----|----|----|
| Superior | Panel solar, Heltec WiFi LoRa V4 (Antena) | Se encuentra el panel solar, encargado de captar energía para alimentar el sistema y contribuir a la autonomía de la boya. Además, incorpora la antena de comunicación LoRa, que permite transmitir inalámbricamente los datos recopilados hacia la estación receptora. |
| Intermedio | BME280, Heltec WiFi LoRa V4, | Contiene la unidad de procesamiento y adquisición de datos, encargada de recibir y organizar las lecturas de los sensores. El módulo BME280 permite registrar la temperatura, humedad y presión atmosférica del entorno. |
| Inferior | DS18B20, sonda pH, sensor de conductividad/TDS | Aloja los sensores destinados al monitoreo de las condiciones fisicoquímicas del agua. Esta sección cuenta con dos subsecciones que permiten el contacto directo de los sensores con el medio y, al mismo tiempo, aíslan las secciones superiores para evitar el ingreso de agua y humedad hacia los componentes electrónicos. |

### **5. Características y dimensiones**
  
  <img width="986" height="677" alt="image" src="https://github.com/user-attachments/assets/23a25e52-c5b0-483c-92a1-44c772bbbf81" />

  <img width="3508" height="2480" alt="Cuerpo de boya" src="https://github.com/user-attachments/assets/71e2ce09-2ce6-4d0a-a488-f8afb7655858" />

  <img width="986" height="680" alt="image" src="https://github.com/user-attachments/assets/4b68e8a0-f1d0-4a61-8741-465512db5869" />

  <img width="3508" height="2480" alt="Cinturón, tuerca y tornillo" src="https://github.com/user-attachments/assets/2ff8c21a-91d7-4dac-a3d7-b364dd965c5d" />

### **6. Selección de material**

Inicialmente, se planteó utilizar polietileno de alta densidad (HDPE) para la fabricación definitiva de la boya, considerando las condiciones ambientales a las que estaría expuesta durante su funcionamiento. Sin embargo, debido a que en esta etapa se presentará un prototipo funcional elaborado mediante impresión 3D, se optó por utilizar PLA, facilitando la fabricación y reproducción de la geometría diseñada. Si bien, el HDPE se mantiene como material previsto para el producto final, el PLA se empleará exclusivamente para la elaboración del prototipo.

### **7. Evaluación de flotabilidad y estabilidad**

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

### 7.1. Cinturón de sujeción y unión al sistema de anclaje

El diseño de la boya incorpora un cinturón de sujeción en forma de aro, dispuesto alrededor de una sección de la estructura, cuya función principal es establecer la unión entre la boya y el sistema de anclaje. Este elemento permite mantener la boya aproximadamente en una posición determinada, proporcionando libertad de giro relativa entre la boya y el cinturón ante la acción de fuerzas ambientales, como el viento, las corrientes de agua y el oleaje.

Para la evaluación de flotabilidad, el cinturón se considera parte de la masa total del sistema. El cinturón presenta una masa de 0.82017 kg y un volumen de 0.00108464 m³, mientra que el volumen de agua requerido para compensar su peso es de aproximadamente 0.00082017 m³, equivalente al 75.62 % de su volumen. Por tanto, presenta flotabilidad positiva.

Finalmente, se plantea verificar experimentalmente que el cinturón mantenga la conexión con la boya y el sistema de anclaje, además, de permitir el giro de la boya y que no genere interferencias significativas con la flotación o estabilidad del sistema.

### **8. Análisis estructural mediante SimScale**

### **8.1. Cargas consideradas en el análisis**

| **Tipo de carga** |	**Zona de aplicación** |	**Objetivo** |
|:------------------|------------------------|---------------|
| Fuerza de arrastre |		| Se evaluará los esfuerzos por resistencia al flujo de la superficie expuesta al aire. |
| Fuerza del oleaje | 	| Se evaluará la respuesta estructural ante las acciones de las olas de la superficie en contacto con el agua. |
| Presión hidrostática |	Superficie sumergida | Se evaluará los esfuerzos debido a la presión del agua del volumen sumergido. |
| Tensión del ancla | 	| Se evaluará los esfuerzos transmitidos por el sistema de anclaje en el cinturón y en la unión con la boya. |

Para el cálculo de la fuerza de arrastre se tomó como referencia el artículo de investigación [5], del cual se consideró la siguiente expresión: $$F_D = \frac{1}{2} C_d \, \rho \, A \, v^2$$
Asimismo, se adoptó un coeficiente de arrastre **$C_d$** de **1,01** para el análisis.


### **9. Evaluación de estabilidad y comportamiento esperado**



Aquí relacionas los resultados de flotabilidad + SimScale y explicas qué indican sobre el comportamiento esperado de la boya.

### **10. Validación experimental prevista**

Finalmente señalas que los resultados teóricos y computacionales serán contrastados con pruebas físicas del prototipo impreso en PLA.

## Referencias

[1] CONCYTEC, «Directiva N.º 001-2022-CONCYTEC-P: Uso de la metodología nivel de madurez tecnológica (TRL)», Resolución de Presidencia N.º 020-2022-CONCYTEC-P, Lima, Perú, 2022. Disponible: https://vinculate.concytec.gob.pe/wp-content/files/RP-020-2022-CONCYTEC-P.pdf

[2] G. Espinoza Yauri, «TRL 2, 3 y 4: Investigación aplicada», material de clase, Oficina de Transferencia Tecnológica y Vinculación Empresarial, UPCH, diapositivas 14--16, 2026.

[3] Oficina de Ciencias y Tecnología de la Tierra de la NASA, «Niveles de preparación tecnológica (TRL)». Disponible en: https://esto.nasa.gov/trl/ (consulta: 1 nov. 2026).

[4] C. V. Peñaranda Osorio, Mecánica de fluidos. Bogotá: Ecoe Ediciones, 2018. pp. 54-56 [En Línea] Disponible en: https://elibro.net/es/lc/cayetano/titulos/122458

[5] M. Yoshikai et al., «Field Measurement and Prediction of Drag in a Planted Rhizophora Mangrove Forest», Journal of Geophysical Research: Oceans, vol. 127, n.o 11, p. e2021JC018320, 2022, doi: 10.1029/2021JC018320.

