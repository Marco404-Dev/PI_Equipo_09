🌊 Manglar (NAME-MODIFICAR) EQUIPO- 09
Sistema inteligente de monitoreo ecológico para la estimación de oxígeno disuelto en los manglares de Tumbes mediante IoT y Machine Learning

# Equipo 09 - Proyecto Integrador 2026-II  
### Carrera de Ingeniería Ambiental / Informática / Industrial
**Universidad Peruana Cayetano Heredia**

---
<p align="center">
  <img src="recursos/imagenes/ods14.gif" alt="ODS 12 - Producción y consumo responsables" width="1000"/>
</p>

---

## 🌍 Descripción del Equipo  
Somos el **Equipo 09** del curso **Proyecto Integrador 2026-II**, conformado por estudiantes de la carrera de Ingeniería Ambiental e Informática.  
Nuestro objetivo es aplicar la metodología de diseño para generar soluciones innovadoras con impacto social, tecnológico y ambiental.  

Nos interesa trabajar en los siguientes **Objetivos de Desarrollo Sostenible (ODS):**  
- **ODS 14: Vida submarina**
- ODS 6: Agua limpia y saneamiento
- ODS 13: Acción por el clima
- ODS 15: Vida de ecosistemas terrestres 

---

## 📸 Fotografía del Equipo  
<p align="center">
  <img src="/recursos/imagenes/equipo.png" alt="Foto grupal del equipo" width="500"/><br>
  <em>Figura 1. Fotografía del equipo 06</em>
</p>

---

## 👥 Integrantes del Equipo  

| Foto | Nombre | Rol | Intereses |
|------|--------|-----|-----------|
| <img src="/recursos/imagenes/result_RUTH.png" width="90"/> | **Ruth Elizabeth Atiro Cobeñas** | Líder del equipo | Innovación social, sostenibilidad |
| <img src="/recursos/imagenes/result_SHEY.png" width="90"/> | **Sheila Rocío Calla Mamani** | Responsable de investigación | Gestión ambiental, desarrollo comunitario |
| <img src="/recursos/imagenes/result_BENEDICT.png" width="90"/> | **Benedict Mattew Quispe Paniagua** | Integración de Hardware y Software | Computación en la nube, desarrollo web, redes, desarrollo de software |
| <img src="/recursos/imagenes/result_MARCO.png" width="90"/> | **Marco Antonio Ancco Quispe** | Programador/a - Modelador/a | Programación, análisis de datos, simulación |
| <img src="/recursos/imagenes/result_Ivana.png" width="90"/> | **Ivana Francesca Gygax Malca** | Investigadora | Documentación y validación |







---

# 📌 Descripción del Proyecto

El **Santuario Nacional Los Manglares de Tumbes** representa uno de los ecosistemas estuarinos más importantes del Perú debido a su alta biodiversidad, capacidad de almacenamiento de carbono y función como zona de reproducción y refugio para especies de importancia ecológica y socioeconómica, como la **concha negra (*Anadara tuberculosa*)**.

Sin embargo, este ecosistema se encuentra expuesto a diversas amenazas ambientales, entre ellas descargas antropogénicas y variaciones climáticas extremas asociadas al **Fenómeno El Niño**, las cuales pueden alterar las condiciones fisicoquímicas del agua.

Uno de los parámetros más importantes para evaluar la salud del ecosistema es el **Oxígeno Disuelto (OD)**, debido a que niveles bajos pueden generar condiciones de **hipoxia**, afectando la supervivencia de organismos acuáticos y alterando el equilibrio ecológico.

Actualmente, el monitoreo continuo del oxígeno disuelto presenta limitaciones debido al elevado costo de sensores especializados, requerimientos de mantenimiento y dificultades de operación en ambientes con alta salinidad, presencia de lodo y condiciones ambientales variables.

---

# 💡 Propuesta del Proyecto

Este proyecto propone desarrollar un **sistema IoT de vigilancia ambiental temprana** capaz de monitorear variables fisicoquímicas del agua y estimar el nivel de **Oxígeno Disuelto (OD)** mediante modelos de **Machine Learning**.

La propuesta busca reducir la dependencia de sensores especializados de oxígeno mediante la construcción de un:

## 🧠 Sensor Virtual de Oxígeno Disuelto

En lugar de medir directamente el oxígeno mediante sensores costosos, el sistema utiliza variables ambientales accesibles:

| Variable | Descripción |
|----------|-------------|
| 🌡️ Temperatura | Influye en la solubilidad del oxígeno en el agua |
| ⚗️ pH | Proporciona información sobre condiciones químicas y procesos biológicos |
| 🌊 Conductividad eléctrica | Relacionada con la concentración iónica y salinidad |

Estas variables serán utilizadas para entrenar modelos predictivos capaces de estimar la concentración de oxígeno disuelto presente en el agua.

### Flujo general del modelo

```text
Temperatura
      |
      |
pH ----|----> Modelo Machine Learning ----> Oxígeno Disuelto estimado
      |
# 🎯 Objetivos del Proyecto

## Objetivo General

Desarrollar un sistema IoT inteligente capaz de monitorear variables fisicoquímicas del agua y estimar el **Oxígeno Disuelto (OD)** mediante modelos de **Machine Learning**, con la finalidad de evaluar la calidad ambiental de ecosistemas de manglar.

---

## Objetivos Específicos

### 🌡️ 1. Adquisición de datos ambientales

Diseñar e implementar un sistema basado en **ESP32** capaz de obtener información fisicoquímica del agua mediante sensores accesibles de:

- Temperatura.
- pH.
- Conductividad eléctrica.

Estos datos permitirán caracterizar las condiciones ambientales del ecosistema monitoreado.

---

### 🤖 2. Modelamiento predictivo del Oxígeno Disuelto

Establecer la relación entre las variables fisicoquímicas del agua y la concentración de **Oxígeno Disuelto (OD)** mediante modelos de **Machine Learning**.

El modelo buscará estimar el OD utilizando como variables de entrada:

```text
Temperatura + pH + Conductividad eléctrica
      |
Conductividad
