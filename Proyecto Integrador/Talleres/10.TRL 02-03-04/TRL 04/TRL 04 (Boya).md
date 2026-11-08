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

### **Diseño técnico definitivo de la boya.**

| **Sección** | **Componente** | **Descripción** |
|:---|----|----|
| 1\. Superior  | Panel solar, Heltec WiFi LoRa V4 (Antena) | Se encuentra el panel solar, encargado de captar energía para alimentar el sistema y contribuir a la autonomía de la boya. Además, incorpora la antena de comunicación LoRa, que permite transmitir inalámbricamente los datos recopilados hacia la estación receptora. |
| 2\. Intermedio | BME280, Heltec WiFi LoRa V4, | Contiene la unidad de procesamiento y adquisición de datos, encargada de recibir y organizar las lecturas de los sensores. El módulo BME280 permite registrar la temperatura, humedad y presión atmosférica del entorno. |
| 3\. Inferior  | DS18B20, sonda pH, sensor de conductividad/TDS | Aloja los sensores destinados al monitoreo de las condiciones fisicoquímicas del agua. Esta sección cuenta con dos subsecciones que permiten el contacto directo de los sensores con el medio y, al mismo tiempo, aíslan las secciones superiores para evitar el ingreso de agua y humedad hacia los componentes electrónicos. |

- Características y dimensiones
  
  <img width="986" height="677" alt="image" src="https://github.com/user-attachments/assets/23a25e52-c5b0-483c-92a1-44c772bbbf81" />

  <img width="986" height="683" alt="image" src="https://github.com/user-attachments/assets/b017211d-a6c8-4b4a-8211-829c8142ad59" />

  <img width="986" height="680" alt="image" src="https://github.com/user-attachments/assets/4b68e8a0-f1d0-4a61-8741-465512db5869" />

- Selección de material

  Inicialmente, se planteó utilizar polietileno de alta densidad (HDPE) para la fabricación definitiva de la boya, considerando las condiciones ambientales a las que estaría expuesta durante su funcionamiento. Sin embargo, debido a que en esta etapa se presentará un prototipo funcional elaborado mediante impresión 3D, se optó por utilizar PLA, facilitando la fabricación y reproducción de la geometría diseñada. Si bien, el HDPE se mantiene como material previsto para el producto final, el PLA se empleará exclusivamente para la elaboración del prototipo.

- Evaluación de flotabilidad y estabilidad

  La flotabilidad de la boya ManglarLab se evaluó mediante el principio de Arquímedes, el cual establece que todo cuerpo sumergido parcial o totalmente en un fluido experimenta un empuje vertical hacia arriba equivalente al peso del fluido desplazado.

|          **Parámetro**           | **Valor**     |
|:--------------------------------:|---------------|
|        Masa de estructura        | 2392.0242 g   |
| Masa de los componentes internos | 283.7 g       |
|            Masa total            | 2675.7242 g   |
|    Volumen del espacio hueco     | 0.01031871 m³ |
|       Volumen del material       | 0.00191362 m³ |
|          Volumen total           | 0.01223233 m³ |

Según el principio de Arquimides: Empuje = Peso = masa total x gravedad (9.81 m/s^2$$)

$$\rho_{\text{agua}} \cdot g \cdot V_{\text{desplazado}} = m_{\text{total}} \cdot g$$

$$V_{\text{desplazado}} = \frac{m_{\text{total}}}{\rho_{\text{agua}}}$$

$$V_{\text{desplazado}} = \frac{2.6757242\ kg}{1000\text{~kg/m}^{3}}$$

$$V_{\text{desplazado}} = 0.002676\ \text{m}^{3} = 2.676\ L$$

Al comparar el volumen total con el volumen desplazado, observamos que el volumen de la boya es superior al desplazado. Por tanto, la boya cuenta con condiciones favorables para poder flotar.

Además; considerando la geometría exterior de la boya y el volumen de agua requerido para equilibrar su peso, la profundidad de inmersión es de aproximadamente 29.63 cm. Para este cálculo se consideró el desplazamiento generado por el tubo cilíndrico inferior y una parte de la sección cónica.

Finalmente, se estima que el tubo inferior permanezca completamente sumergido, junto con aproximadamente 11.73 cm de la sección cónica, mientras que el cuerpo cilíndrico principal se mantenga sobre la superficie del agua. Esto se podrá confirmar una vez se aplique en laboratorio.

