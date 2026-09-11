<h1 align="center">🌊 YakuToring</h1>

<h3 align="center">
Sistema inteligente de monitoreo ecológico para la estimación de Oxígeno Disuelto en los manglares de Tumbes mediante IoT y Machine Learning
</h3>

<p align="center">
<b>Equipo 09 - Proyecto Integrador 2026-II</b><br>
Universidad Peruana Cayetano Heredia
</p>

---

<p align="center">
  <img src="recursos/imagenes/ods14.gif" alt="ODS relacionados al proyecto" width="1000"/>
</p>

---

# 👥 Equipo 09 - Proyecto Integrador 2026-II

### Carreras involucradas:
- Ingeniería Ambiental
- Ingeniería Informática
- Ingeniería Industrial

Somos el **Equipo 09** del curso **Proyecto Integrador 2026-II**, conformado por estudiantes de diferentes áreas de ingeniería.

Nuestro objetivo es aplicar metodologías de diseño e innovación para desarrollar soluciones con impacto **social, tecnológico y ambiental**, integrando conocimientos interdisciplinarios para abordar problemáticas reales.

---

# 🌍 Alineación con Objetivos de Desarrollo Sostenible (ODS)

Nuestro proyecto se encuentra relacionado con los siguientes **Objetivos de Desarrollo Sostenible (ODS):**

| ODS | META ESPECÍFICA |
| :---: | :---: |
| **💧ODS 6: Agua Limpia** | **Meta 6.6:** De aquí a 2030, proteger y restablecer los ecosistemas relacionados con el agua, incluidos los humedales y estuarios. |
| **⚙️ODS 9: Industria e Innovación** | **Meta 9.5:** Aumentar la investigación científica y mejorar la capacidad tecnológica de los sectores industriales y de investigación. |
| **☁️ODS 13: Acción por el Clima** | **Meta 13.1:** Fortalecer la resiliencia y la capacidad de adaptación a los riesgos relacionados con el clima y los desastres naturales. |
| **🌊ODS 14: Vida Submarina** | **Meta 14.2:** De aquí a 2020, gestionar y proteger sosteniblemente los ecosistemas marinos y costeros para evitar efectos adversos significativos. |
| **🌳ODS 15: Ecosistemas Terrestres** | **Meta 15.1:** Asegurar la conservación y el uso sostenible de los ecosistemas terrestres y los ecosistemas interiores de agua dulce. |

# 📸 Fotografía del Equipo

<p align="center">
  <img src="recursos/imagenes/equipo.png" alt="Foto grupal del equipo" width="500"/>
  <br>
  <em>Equipo 09 - Proyecto Integrador 2026-II</em>
</p>

---

# 👤 Integrantes del Equipo

| Foto | Nombre | Rol | Intereses |
|------|--------|-----|-----------|
| <img src="recursos/imagenes/result_RUTH.png" width="90"/> | **Ruth Elizabeth Atiro Cobeñas** | Líder del equipo | Innovación social, sostenibilidad |
| <img src="recursos/imagenes/result_SHEY.png" width="90"/> | **Sheila Rocío Calla Mamani** | Responsable de investigación | Gestión ambiental, desarrollo comunitario |
| <img src="recursos/imagenes/result_BENEDICT.png" width="90"/> | **Benedict Mattew Quispe Paniagua** | Integración Hardware y Software | Computación en la nube, desarrollo web, redes y desarrollo de software |
| <img src="recursos/imagenes/result_MARCO.png" width="90"/> | **Marco Antonio Ancco Quispe** | Programador y Modelador | Programación, análisis de datos y simulación |
| <img src="recursos/imagenes/result_Ivana.png" width="90"/> | **Ivana Francesca Gygax Malca** | Investigadora | Documentación y validación |

---

# 📌 Descripción del Proyecto

El **Santuario Nacional Los Manglares de Tumbes** representa uno de los ecosistemas estuarinos más importantes del Perú debido a su alta biodiversidad, capacidad de almacenamiento de carbono y función como zona de reproducción y refugio para especies de importancia ecológica y socioeconómica, como la **concha negra (*Anadara tuberculosa*)**.

Este ecosistema cumple un papel fundamental en la conservación de la biodiversidad marina y en el desarrollo sostenible de las comunidades vinculadas al aprovechamiento de recursos hidrobiológicos.

Sin embargo, los manglares se encuentran expuestos a diversas amenazas ambientales, entre ellas:

- Descargas antropogénicas.
- Alteraciones fisicoquímicas del agua.
- Variaciones climáticas extremas asociadas al **Fenómeno El Niño**.

Estas condiciones pueden modificar el equilibrio del ecosistema y afectar parámetros fundamentales para la supervivencia de organismos acuáticos.

---

# 🌱 Problemática

Uno de los parámetros más importantes para evaluar la salud del ecosistema acuático es el **Oxígeno Disuelto (OD)**.

El oxígeno disuelto representa la cantidad de oxígeno disponible en el agua para los organismos vivos y está relacionado con diversos procesos físicos, químicos y biológicos del ecosistema.

Una disminución significativa del OD puede generar condiciones de **hipoxia**, afectando:

- La supervivencia de organismos acuáticos.
- La biodiversidad del ecosistema.
- Los procesos ecológicos naturales.
- Recursos hidrobiológicos de importancia económica como la concha negra.

Actualmente, el monitoreo continuo del oxígeno disuelto presenta limitaciones debido a:

- Alto costo de sensores especializados.
- Requerimientos de mantenimiento.
- Dificultades de operación en ambientes con alta salinidad.
- Presencia de lodo y condiciones ambientales variables.

Estas limitaciones dificultan implementar sistemas accesibles de vigilancia ambiental continua.

---

# 💡 Propuesta del Proyecto

Este proyecto propone desarrollar un **sistema IoT de vigilancia ambiental temprana** capaz de monitorear variables fisicoquímicas del agua y estimar el nivel de **Oxígeno Disuelto (OD)** mediante modelos de **Machine Learning**.

La propuesta busca reducir la dependencia de sensores especializados de oxígeno mediante la construcción de un:

# 🧠 Sensor Virtual de Oxígeno Disuelto

En lugar de medir directamente el oxígeno mediante sensores especializados de alto costo, el sistema utilizará variables ambientales accesibles:

| Variable | Descripción |
|----------|-------------|
| 🌡️ Temperatura | Influye en la solubilidad del oxígeno en el agua y en procesos biológicos |
| ⚗️ pH | Proporciona información sobre condiciones químicas y procesos ambientales |
| 🌊 Conductividad eléctrica | Relacionada con la concentración iónica y cambios asociados a la salinidad |

Estas variables serán utilizadas para entrenar modelos predictivos capaces de estimar la concentración de oxígeno disuelto presente en el agua.

---

# 🔬 Flujo general del modelo

```text
Temperatura
      |
      |
pH ----|----> Modelo Machine Learning ----> Oxígeno Disuelto estimado
      |
      |
Conductividad eléctrica
```

---

# 🎯 Objetivos del Proyecto

## Objetivo General

Desarrollar un sistema IoT inteligente capaz de monitorear variables fisicoquímicas del agua y estimar el **Oxígeno Disuelto (OD)** mediante modelos de **Machine Learning** como indicador de la calidad ambiental de ecosistemas de manglar.

La propuesta busca integrar sensores ambientales accesibles, procesamiento de datos y modelos predictivos para desarrollar una herramienta tecnológica orientada al monitoreo ecológico continuo.

---

## Objetivos Específicos

### 🌡️ 1. Caracterización ambiental mediante sensores IoT

Diseñar e implementar un sistema basado en **ESP32** capaz de adquirir variables fisicoquímicas del agua relacionadas con la calidad ambiental del ecosistema.

Las variables consideradas son:

- 🌡️ **Temperatura:** Influye en la solubilidad del oxígeno y en los procesos biológicos del ecosistema.
- ⚗️ **pH:** Permite analizar las condiciones químicas del agua.
- 🌊 **Conductividad eléctrica:** Relacionada con la concentración iónica y variaciones asociadas a la salinidad.

La información obtenida permitirá construir una base de datos experimental para analizar la relación entre estas variables y el Oxígeno Disuelto.

---

### 🤖 2. Desarrollo de un modelo predictivo de Oxígeno Disuelto

Establecer la relación matemática y predictiva entre las variables fisicoquímicas del agua y la concentración de **Oxígeno Disuelto (OD)** mediante algoritmos de **Machine Learning**.

El modelo utilizará como variables de entrada:

```text
Temperatura
pH
Conductividad eléctrica
```

para estimar:

```text
Oxígeno Disuelto (OD)
```

El sistema será evaluado mediante métricas de desempeño y análisis de incertidumbre con el objetivo de determinar la confiabilidad de las predicciones.

---

### 🧪 3. Validación experimental del modelo

Evaluar progresivamente el funcionamiento del sistema mediante pruebas controladas en diferentes condiciones del agua.

Inicialmente se considerarán:

- Agua dulce.
- Agua salada.
- Condiciones similares a ambientes estuarinos.

Estas pruebas permitirán:

- Validar el funcionamiento de los sensores.
- Analizar la relación entre variables ambientales y OD.
- Evaluar los límites del modelo predictivo.
- Identificar factores externos que puedan afectar la estimación.

---

### 🌱 4. Monitoreo y conservación ambiental

Desarrollar una herramienta tecnológica accesible que permita analizar la evolución de las condiciones del agua e identificar posibles escenarios de estrés ambiental dentro del ecosistema de manglar.

El sistema busca generar información útil para:

- Investigación ambiental.
- Monitoreo ecológico.
- Evaluación de cambios en la calidad del agua.
- Futuras estrategias de conservación.

---

# 🏗️ Arquitectura General del Sistema

El sistema está compuesto por diferentes módulos integrados:

```text
              Ecosistema Manglar

                     ↓

        ┌────────────┬────────────┐
        │            │            │

  Temperatura       pH      Conductividad

        │            │            │

        └────────────┴────────────┘

                     ↓

                   ESP32

                     ↓

          Procesamiento de datos

                     ↓

          Modelo Machine Learning

                     ↓

        Oxígeno Disuelto estimado

                     ↓

             AWS / Dashboard
```

---

# 🔧 Componentes del Sistema

| Componente | Función |
|------------|---------|
| ESP32 DevKit | Procesamiento y comunicación del sistema |
| Sensor DS18B20 | Medición de temperatura del agua |
| Sensor pH | Medición de condiciones químicas |
| Sensor de conductividad | Estimación de cambios relacionados con salinidad |
| Módulo de comunicación | Transmisión futura de datos |
| Boya experimental | Soporte físico del sistema |

---

# 🤖 Machine Learning

## Planteamiento del problema

El proyecto plantea un problema de **regresión supervisada**, donde el modelo aprende la relación entre variables ambientales medidas y la concentración de Oxígeno Disuelto.

### Variables de entrada:

```text
X = [Temperatura, pH, Conductividad eléctrica]
```

### Variable objetivo:

```text
Y = Oxígeno Disuelto (OD)
```

---

## Flujo de entrenamiento

```mermaid
flowchart TD
    subgraph S1["① ADQUISICIÓN DE DATOS"]
        A["Sensores ambientales"] --> C["Registro de datos experimentales<br/>con fecha y hora"]
        B["Medidor de OD de referencia"] --> C
    end

    subgraph S2["② PREPARACIÓN Y ENTRENAMIENTO"]
        C --> D["Revisar calidad de datos<br/>y preparar variables"]
        D --> E["Separar experimentos para<br/>entrenamiento, validación y prueba"]
        E --> F["Entrenar y ajustar el modelo<br/>con entrenamiento y validación"]
        F --> G{"¿Cumple los criterios<br/>en validación?"}
        G -- "No" --> H["Revisar datos, variables<br/>y configuración del modelo"]
        H --> F
    end

    subgraph S3["③ EVALUACIÓN Y USO"]
        G -- "Sí" --> I["Evaluar una vez con<br/>los experimentos de prueba reservados"]
        I --> J["Documentar error, limitaciones<br/>y condiciones de uso"]
        J --> K["Si el desempeño es adecuado:<br/>usar el modelo con nuevas mediciones"]
        K --> L(["Oxígeno disuelto estimado · mg/L"])
    end

    classDef sensor fill:#E0F2FE,stroke:#0284C7,stroke-width:2px,color:#0C4A6E;
    classDef proceso fill:#EFF6FF,stroke:#3B82F6,stroke-width:2px,color:#1E3A8A;
    classDef decision fill:#CCFBF1,stroke:#0D9488,stroke-width:2px,color:#134E4A;
    classDef revision fill:#FFF7ED,stroke:#EA580C,stroke-width:2px,color:#7C2D12;
    classDef resultado fill:#065F46,stroke:#34D399,stroke-width:3px,color:#FFFFFF;

    class A,B sensor;
    class C,D,E,F,I,J,K proceso;
    class G decision;
    class H revision;
    class L resultado;

    style S1 fill:#F8FAFC,stroke:#CBD5E1,color:#334155
    style S2 fill:#F0FDFA,stroke:#99F6E4,color:#134E4A
    style S3 fill:#F0FDF4,stroke:#BBF7D0,color:#14532D

    linkStyle default stroke:#64748B,stroke-width:2px;
```

---

## Modelos considerados

Como primera aproximación se evaluarán modelos de regresión:

- Regresión lineal.
- Random Forest.
- XGBoost.

La selección final dependerá del desempeño obtenido con los datos experimentales.

---

## Evaluación del modelo

El desempeño será evaluado mediante:

- **MAE:** Error absoluto medio.
- **RMSE:** Error cuadrático medio.
- **R²:** Capacidad explicativa del modelo.

Además, se analizará la incertidumbre asociada a las predicciones para determinar la confiabilidad del sensor virtual.

---

# ☁️ Arquitectura Cloud (Propuesta futura)

Como evolución del sistema se plantea una arquitectura basada en servicios cloud para almacenamiento y visualización remota.

```text
Boya IoT

   ↓

ESP32

   ↓

Comunicación inalámbrica

   ↓

AWS

   ↓

Base de datos

   ↓

Dashboard ambiental
```

Esta arquitectura permitirá:

- Almacenar históricos de medición.
- Consultar datos remotamente.
- Analizar tendencias ambientales.
- Escalar el sistema hacia futuras implementaciones en campo.

---

# 📊 Estado del Proyecto

## ✅ Completado

- Investigación del problema ambiental.
- Definición de la propuesta tecnológica.
- Identificación de variables ambientales.
- Matriz morfológica.
- Diseño conceptual del sistema.
- Diseño preliminar electrónico.
- Diseño mecánico de la boya.
- Simulación estructural.

---

## 🔄 En desarrollo

- Integración de sensores.
- Construcción del prototipo.
- Pruebas experimentales.
- Generación del dataset.
- Desarrollo del modelo Machine Learning.

---

## 🔜 Trabajo futuro

- Validación en condiciones reales del manglar.
- Optimización del modelo predictivo.
- Integración completa con AWS.
- Implementación de dashboard de monitoreo.
- Evaluación con datos ambientales reales.

---

# 📚 Referencias Científicas

- [1] Instituto del Mar del Perú (IMARPE), Informes de evaluación poblacional de concha negra y calidad del medio acuático en la Región Tumbes, Callao, Perú: IMARPE, 2020.
- [2] R. B. Baird, A. D. Eaton, and E. W. Rice, Eds., Standard Methods for the Examination of Water and Wastewater, 23rd ed. Washington, DC, USA: American Public Health Association (APHA), 2017.
- [3] Ministerio del Ambiente (MINAM), Estándares de Calidad Ambiental (ECA) para Agua, Decreto Supremo N° 004-2017-MINAM, Lima, Perú, 2017.
- [4] K. Takahashi and A. Martínez, "El Niño, cambio climático, y el ecosistema de manglares de Tumbes," Instituto Geofísico del Perú (IGP), Lima, Perú, Tech. Rep., 2015.
- [5] Y. Zhi et al., "Prediction of dissolved oxygen in water based on machine learning," Scientific Reports.
- [6] SERNANP, Plan Maestro del Santuario Nacional Los Manglares de Tumbes (2016-2020), Servicio Nacional de Áreas Naturales Protegidas por el Estado, Lima, Perú, 2016.
