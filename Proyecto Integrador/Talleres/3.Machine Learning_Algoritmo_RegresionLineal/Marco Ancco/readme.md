# Reporte Técnico: Taller de Inteligencia Artificial
**Módulo de Modelado de Regresión y Diagnóstico de Variables**

---

### Contexto del Experimento
Este informe aborda la evaluación de un modelo predictivo centrado en estimar la demanda de **consumo energético**. El análisis contempla el impacto directo de factores operativos y ambientales clave: **temperatura**, **horas de operación**, **nivel de carga** y **porcentaje de humedad**.

El proceso metodológico estructuró las siguientes fases clave:
1. **Exploración de Variables:** Análisis exploratorio de datos (EDA) para identificar niveles de correlación e interdependencia.
2. **Modelado Estimativo:** Ajuste de algoritmos de **Regresión Lineal** y **Árboles de Decisión**.
3. **Validación de Supuestos:** Evaluación diagnóstica mediante el análisis de residuos y precisión frente a datos reales.


# Análisis e Interpretación de Gráficos

## 1. Matriz de Correlación
Gráfico de calor (*heatmap*) que representa los coeficientes de correlación de Pearson entre las distintas variables del conjunto de datos.

* **Relación Fuerte:** La variable **`Horas_Operacion`** presenta una correlación lineal muy alta con **`Consumo_Energia`** ($r = 0.84$), posicionándose como el principal predictor del consumo.
* **Relación Moderada:** **`Carga`** muestra una asociación positiva moderada con el consumo de energía ($r = 0.34$).
* **Variables Independientes:** **`Temperatura`** ($0.098$) y **`Humedad`** ($0.063$) no muestran una correlación significativa con el consumo energético ni con las demás variables explicativas.
<img width="761" height="588" alt="1 matriz_de_correlacion" src="https://github.com/user-attachments/assets/8905ff75-8be4-4a3f-afb9-a08d67b68618" />

---

## 2. Consumo de Energía Real vs. Predicción
Diagrama de dispersión (*scatter plot*) diseñado para evaluar la precisión global de un modelo de regresión.

* **Ajuste Lineal:** Los puntos se concentran a lo largo de la diagonal principal, lo que refleja que las predicciones coinciden cercanamente con los valores reales.
* **Homocedasticidad:** La dispersión de los errores se mantiene constante en todo el rango de evaluación (de $15$ a $40$ unidades de consumo).
<img width="851" height="647" alt="2 grafico_real_vs_predicho" src="https://github.com/user-attachments/assets/a43d4f2a-dceb-4398-a9bf-8026d5478191" />

---

## 3. Histograma de Residuos (Verificación de Normalidad)
Distribución de frecuencias y estimación de densidad de Kernel (KDE) sobre los errores de predicción ($e = y_{real} - y_{predicho}$).

* **Distribución Bell-Shaped:** Los residuos adoptan la forma de una campana de Gauss centrada en cero ($0.0$).
* **Ausencia de Sesgo:** La simetría indica que el modelo no sobreestima ni subestima sistemáticamente los datos, cumpliendo el supuesto de normalidad en los residuos.
<img width="939" height="647" alt="3 histograma_de_residuos" src="https://github.com/user-attachments/assets/5143db50-b315-4c2e-a396-3ff7f6fdd766" />

---

## 4. Gráfico Real vs. Árbol de Decisión
Gráfico de dispersión que contrasta los valores observados frente a las estimaciones obtenidas mediante un árbol de decisión.

* **Estructura Escalonada:** Muestra una mayor dispersión con agrupamientos discretos, comportamiento típico de las particiones rectangulares de los modelos basados en árboles.
* **Amplitud de Rango:** Presenta valores en un rango más extenso y negativo (de $-300$ a $+200$), sugiriendo una mayor varianza en la respuesta estimada.
<img width="563" height="413" alt="4 grafico_real_vs_arbol" src="https://github.com/user-attachments/assets/e4e05753-0da2-4fe3-b4e1-7759bd50d0cd" />

---

## 5. Importancia Relativa de Características (Árbol)
Gráfico de barras horizontales que detalla la importancia normalizada de cada variable predictora en la construcción del árbol.

| Variable | Importancia Normalizada | Impacto en el Modelo |
| :--- | :--- | :--- |
| **X2** | **~0.54 (54%)** | Variable determinante en la reducción de impureza/varianza. |
| **X1** | **~0.27 (27%)** | Segundo factor de mayor relevancia en las divisiones. |
| **X3** | **~0.11 (11%)** | Contribución moderada. |
| **X6** | **~0.03 (3%)** | Bajo impacto predictivo. |
| **X4** | **~0.03 (3%)** | Bajo impacto predictivo. |
| **X5** | **< 0.01 (< 1%)** | Variable prescindible. |

<img width="907" height="609" alt="5 Importancia_de_arbol" src="https://github.com/user-attachments/assets/fdfbf466-f9a4-4d6d-9a27-9d7c4adbdb70" />
