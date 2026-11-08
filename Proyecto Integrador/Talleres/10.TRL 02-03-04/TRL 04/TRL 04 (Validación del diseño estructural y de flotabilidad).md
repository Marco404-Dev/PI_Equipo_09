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

En esta etapa se desarrolla y evalúa el diseño físico de la boya, considerando la distribución de los componentes, sus dimensiones, el material del prototipo y las condiciones de flotabilidad y estabilidad. Asimismo, se realizan simulaciones mediante SimScale para analizar el comportamiento estructural de la geometría frente a las cargas consideradas en el diseño.

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

Desarrollar y realizar una validación preliminar en laboratorio del prototipo de boya YakuToring, mediante la evaluación de su diseño físico, flotabilidad, comportamiento estructural, integración de sensores y comunicación LoRa.

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

  La flotabilidad de la boya ManglarLab se evaluó mediante el principio de Arquímedes, el cual establece que todo cuerpo sumergido parcial o totalmente en un fluido experimenta un empuje vertical hacia arriba equivalente al peso del fluido desplazado.

|          **Parámetro**           | **Valor**     |
|:--------------------------------:|---------------|
|        Masa de estructura        | 3236.91679 g |
| Masa de los componentes internos | 283.7 g |
|            Masa total            | 3520.61679 g |
|    Volumen del espacio hueco     | 0.01104772 m³ |
|       Volumen del material       | 0.00259943 m³ |
|          Volumen total           | 0.01364715 m³ |

Según el principio de Arquimides: Empuje = Peso = masa total x gravedad (9.81 m/s^2$$)

$$\rho_{\text{agua}} \cdot g \cdot V_{\text{desplazado}} = m_{\text{total}} \cdot g$$

$$V_{\text{desplazado}} = \frac{m_{\text{total}}}{\rho_{\text{agua}}}$$

$$V_{\text{desplazado}} = \frac{2.6757242\ kg}{1000\text{~kg/m}^{3}}$$

$$V_{\text{desplazado}} = 0.002676\ \text{m}^{3} = 2.676\ L$$

Al comparar el volumen total con el volumen desplazado, observamos que el volumen de la boya es superior al desplazado. Por tanto, la boya cuenta con condiciones favorables para poder flotar.

Además; considerando la geometría exterior de la boya y el volumen de agua requerido para equilibrar su peso, la profundidad de inmersión es de aproximadamente 29.63 cm. Para este cálculo se consideró el desplazamiento generado por el tubo cilíndrico inferior y una parte de la sección cónica.

Finalmente, se estima que el tubo inferior permanezca completamente sumergido, junto con aproximadamente 11.73 cm de la sección cónica, mientras que el cuerpo cilíndrico principal se mantenga sobre la superficie del agua. Esto se podrá confirmar una vez se aplique en laboratorio.

## Referencias

[1] CONCYTEC, «Directiva N.º 001-2022-CONCYTEC-P: Uso de la metodología nivel de madurez tecnológica (TRL)», Resolución de Presidencia N.º 020-2022-CONCYTEC-P, Lima, Perú, 2022. Disponible: https://vinculate.concytec.gob.pe/wp-content/files/RP-020-2022-CONCYTEC-P.pdf

[2] G. Espinoza Yauri, «TRL 2, 3 y 4: Investigación aplicada», material de clase, Oficina de Transferencia Tecnológica y Vinculación Empresarial, UPCH, diapositivas 14--16, 2026.

[3] Oficina de Ciencias y Tecnología de la Tierra de la NASA, «Niveles de preparación tecnológica (TRL)». Disponible en: https://esto.nasa.gov/trl/ (consulta: 1 nov. 2026).
