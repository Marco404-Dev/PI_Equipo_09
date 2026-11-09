## **Resultados: SimScale**

Con el propósito de evaluar el comportamiento estructural de la boya frente a las condiciones de presión y fuerzas a las que estará sometida durante su funcionamiento, se realizaron simulaciones en SimScale.

Para determinar la fuerza de arrastre, se tomó como referencia el artículo de investigación [1], empleando la ecuación correspondiente al cálculo de esta fuerza ($$F_D = \frac{1}{2} C_d \, \rho \, A \, v^2$$). Se adoptó un coeficiente de arrastre **$C_d$** de 1,01 y velocidades de corriente (**$V$**) entre 0,15 y 0,5 m/s. A partir de estos valores, se obtuvieron fuerzas de arrastre de 0,62 N y 6,93 N, correspondientes a las condiciones de menor y mayor velocidad, respectivamente.

Inicialmente, se aplicó una presión hidrostática de 1,815 kPa. A partir de esta condición, se analizaron los desplazamientos y los esfuerzos de Von Mises, con el fin de identificar las zonas de mayor deformación y concentración de esfuerzos y verificar el comportamiento estructural de la boya.

Posteriormente, se sometió la boya a fuerzas de arrastre de 0,62 N y 6,93 N, correspondientes a condiciones de corriente baja y alta, respectivamente. Con ello, se evaluó la respuesta estructural de la boya ante las fuerzas horizontales generadas por el flujo de agua.

### **Presión hidrostática**

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/347f3a8b-5e32-4f7a-8d17-77e55b405f44" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/2daf2272-33bb-4a72-a53d-59bf4158088a" />

 - Esfuerzos de Von Mises: Se muestra que, bajo una presión hidrostática de 1.815 kPa, los esfuerzos se mantienen bajos en la mayor parte de la estructura, mientras que las mayores concentraciones de esfuerzo se localizan principalmente en las zonas de cambio de geometría y unión. Estos esfuerzos elevados elevados se concentran en la parte superior, indicando mayor deformidad.

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/4a450cdc-c670-43ce-9342-271b84a95c4a" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/e439354c-5a38-4f46-85cb-7a32f7a516fa" />
  
 - Magnitud de desplazamiento: La boya presenta pequeños desplazamientos en la mayor parte de su geometría y las mayores magnitudes se concentran en la parte superior de la boya (tapa). Esto indica que la geometría mantiene una adecuada rigidez frente a la condición de presión analizada en la mayor parte de su sistema, pero la tapa constituye la región con mayor desplazamiento.

### **Fuerza de arrastre**

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/f897320e-2172-48bb-96c3-4119f9fcc472" />

 - Esfuerzos de Von Mises: Se observa que ante la fuerza de arrastre, ya sea de 0.62 N o 6.93 N, las deformaciones en la boya son practicamente nulas. No se evidencian valores que indiquen una condición crítica para la integridad estructural del modelo bajo las cargas analizadas, sin embargo, estos resultados corresponden a una simulación y deberán ser confirmadas posteriormente mediante pruebas experimentales en laboratorio.

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/56a1df74-d632-42c3-b23a-12199685198d" />
  
 - Esfuerzos de desplazamiento: En la imagen se puede apreciar, como el cinturón de anclaje no presenta desplazamientos, ya que corresponde a la zona de restricción de la estructura. En comparación, todo el cuerpo de la boya presenta dezplazamientos que aumentan gradualmente desde la sujeción hasta la base. Esto evidencia una deformación global por las fuerzas de arrastre dentro del rango previsto para las cargas evaluadas.

### Referencia:

[1] M. Yoshikai et al., «Field Measurement and Prediction of Drag in a Planted Rhizophora Mangrove Forest», Journal of Geophysical Research: Oceans, vol. 127, n.o 11, p. e2021JC018320, 2022, doi: 10.1029/2021JC018320.
