# Predicción de la Demanda Turística en Tierra del Fuego

### Mediante Modelos de Aprendizaje Automático

**Entrega 1: Descripción y Formulación del Objetivo**

Provincia de Tierra del Fuego, Antártida e Islas del Atlántico Sur · Argentina · 2026

---

## 1. Introducción y Contexto

El turismo es uno de los motores económicos fundamentales de la Provincia de Tierra del Fuego, Antártida e Islas del Atlántico Sur. Ciudades como Ushuaia son polo de turismo internacional y puerta de entrada a la Antártida.

El impacto de la afluencia de visitantes se derrama de forma directa en la hotelería, gastronomía, transporte local, agencias de excursiones y el comercio minorista.

La demanda turística en la región presenta una alta volatilidad y estacionalidad, fuertemente influenciada por factores geográficos, climáticos (temporadas de nieve), conectividad aérea y la programación del turismo de cruceros. Esta predictibilidad limitada genera ineficiencias críticas tanto en el sector público como privado.

El uso de técnicas de Aprendizaje Automático (Machine Learning) ofrece una ventaja competitiva al permitir procesar grandes volúmenes de datos históricos multifactoriales. Al identificar patrones complejos y relaciones no lineales, estos modelos transforman los registros estadísticos pasados en herramientas predictivas de alto valor estratégico para la toma de decisiones.

### 1.1 Evolución Histórica de las Pernoctaciones

La serie histórica completa de pernoctaciones en establecimientos hoteleros de Ushuaia (2004–2025) evidencia la marcada estacionalidad y el impacto del período COVID-19 (2020–2021).

> *Figura 1. Pernoctaciones totales mensuales en Ushuaia (2004–2025). Se observa el fuerte impacto de la pandemia COVID-19 y la posterior recuperación del sector.*

### 1.2 Estacionalidad: El Patrón Central del Problema

La estacionalidad es la principal característica que los modelos predictivos deben capturar. Los meses de verano austral (enero–febrero) concentran el pico de demanda, mientras que el invierno (mayo–agosto) presenta niveles mínimos —con la excepción de julio por turismo de nieve—.

> *Figura 2. Pernoctaciones promedio por mes (2004–2025). Las barras de error muestran la desviación estándar histórica. El verano austral concentra la mayor demanda.*

---

## 2. Definición del Problema

El problema central radica en la incertidumbre operativa provocada por las fluctuaciones de la demanda turística. Para resolverlo, el proyecto aborda el diseño, entrenamiento y validación de un modelo predictivo capaz de estimar el comportamiento de la demanda con una ventana de tiempo óptima para la planificación.

Esta incertidumbre genera ineficiencias en dos dimensiones:

- **Sector privado:** dificultad para dimensionar plantillas de personal, prever compras de insumos o gestionar tarifas dinámicas.
- **Sector público:** desafíos para planificar infraestructura urbana, gestionar saturación de áreas protegidas y coordinar contingencias climáticas.

### 2.1 Turismo Receptor vs. Turismo Interno

Un aspecto clave del problema es la composición de la demanda. Las pernoctaciones se desagregan entre residentes (turismo interno) y no residentes (turismo internacional receptor), dos segmentos con patrones de comportamiento diferenciados.

> *Figura 3. Composición de pernoctaciones: residentes vs. no residentes (turistas internacionales). El turismo no residente domina la demanda y presenta mayor volatilidad.*

---

## 3. Objetivos del Proyecto

### 3.1 Objetivo General

Desarrollar y validar modelos de Aprendizaje Automático que predigan la demanda turística mensual en la Provincia de Tierra del Fuego sobre **tres variables objetivo** —viajeros totales, pernoctaciones totales y visitas al Parque Nacional Tierra del Fuego—, utilizando datos históricos de ocupación hotelera y factores climáticos. Se entrena un modelo independiente por cada variable objetivo.

### 3.2 Objetivos Específicos

- **Recolección e Integración:** consolidar una base de datos unificada a partir de registros históricos de turismo, transporte aéreo, marítimo y datos meteorológicos.
- **Análisis Exploratorio (EDA):** identificar tendencias, ciclos estacionales, correlaciones y outliers en el comportamiento histórico del turismo fueguino.
- **Ingeniería de Características:** limpiar, normalizar y crear variables derivadas clave (lags temporales, dummies de temporada, etc.).
- **Entrenamiento de Modelos:** entrenar un modelo de Regresión Lineal Múltiple por cada variable objetivo, con su propio conjunto de features.
- **Evaluación y Comparación:** medir el desempeño con métricas estadísticas rigurosas (MAE, RMSE, R² y R² por validación cruzada) para evaluar cada modelo.

---

## 4. Descripción del Dataset

| Métrica | Valor | Detalle |
|---|---|---|
| Período analizado | 2004 – 2025 | 21 años |
| Registros de datos | 263 meses | Granularidad mensual |
| Variables analizadas | 12 métricas | Turismo + Parque Nacional |
| Fuente principal | IPIEC | Datos oficiales provinciales |

El dataset integrado cubre 263 registros mensuales (2004–2025) consolidando variables de ocupación hotelera en Ushuaia y visitas al Parque Nacional Tierra del Fuego.

> *Figura 4. Total de viajeros anuales en Ushuaia (2004–2024). Se destacan los años COVID-19 y el año récord de mayor afluencia.*

### 4.1 Parque Nacional Tierra del Fuego

El Parque Nacional es uno de los principales atractivos de la región. Sus datos de visitantes ofrecen una variable independiente de alto valor predictivo y permiten analizar la relación entre afluencia al área protegida y demanda de alojamiento.

> *Figura 5. Visitas mensuales al Parque Nacional Tierra del Fuego (2014–2025). La tendencia creciente confirma el incremento sostenido de la demanda ecoturística.*

---

## 5. Tipo de Problema

El proyecto se define estrictamente como un problema de **Aprendizaje Supervisado de Regresión**.

Las variables objetivo (targets) a predecir son cuantitativas continuas. El proyecto plantea **tres modelos independientes**, uno por cada una de las siguientes variables:

1. **Viajeros totales** (`ush_viaj_total`): cantidad total de viajeros/turistas ingresados en el período.
2. **Pernoctaciones totales** (`ush_pernoc_total`): noches que los turistas pasan en los alojamientos, indicador más preciso del impacto económico real.
3. **Visitas al Parque Nacional** (`parque_visitas_total`): afluencia mensual al Parque Nacional Tierra del Fuego, principal atractivo natural de la región.

---

## 6. Variables del Proyecto (Preliminar)

El dataset se estructura con las siguientes variables independientes (features) candidatas para alimentar los modelos predictivos:

| Categoría | Variables Candidatas |
|---|---|
| Temporales | Año (`anio`), mes (`mes.1`) |
| Capacidad y Ocupación | Tasa de ocupación hotelera (`ush_toh %`), tasa de ocupación de plazas (`ush_top %`), habitaciones y plazas disponibles |
| Clima | Temperatura media mensual, precipitación acumulada, velocidad máxima del viento |

Tras la selección estadística (Correlación + VIF) descrita en la Entrega 2, cada modelo conserva un subconjunto propio de estas 9 variables candidatas.

Las tres variables objetivo (targets) a predecir son cuantitativas continuas:

- **Viajeros totales** (`ush_viaj_total`): total de viajeros/turistas ingresados en el período.
- **Pernoctaciones totales** (`ush_pernoc_total`): noches en alojamientos, indicador más preciso del impacto económico real.
- **Visitas al Parque Nacional** (`parque_visitas_total`): afluencia mensual al área protegida.

---

## 7. Modelos Propuestos y Métricas

### 7.1 Algoritmos de Aprendizaje Automático

Tras evaluar distintos enfoques, el modelo adoptado es la **Regresión Lineal Múltiple (MCO)**. Se consideraron también modelos no lineales como SVR a modo de comparación, pero el análisis confirmó que la relación entre las features y los targets es predominantemente lineal, por lo que se optó por la Regresión Lineal Múltiple por su buen desempeño y, sobre todo, su **interpretabilidad** (coeficientes que indican el peso de cada variable):

| Modelo | Descripción | Rol |
|---|---|---|
| Regresión Lineal Múltiple (MCO) | Modelo interpretable, coeficientes por mínimos cuadrados | **Modelo final** |
| SVR (Support Vector Regression) | Modelo robusto para relaciones no lineales | Comparación (descartado: relación lineal confirmada) |

### 7.2 Métricas de Evaluación

- **MAE — Error Absoluto Medio:** error promedio en las mismas unidades que el target (ej: "el modelo le erra por X turistas en promedio").
- **RMSE — Raíz del Error Cuadrático Medio:** penaliza con mayor fuerza los errores grandes o predicciones muy desviadas.
- **R² — Coeficiente de Determinación:** porcentaje de la variabilidad de la demanda que logra explicar el modelo.

---

## 8. Fuentes de Datos

- **IPIEC** (Instituto Provincial de Estadística y Censos): fuente principal para datos de ocupación local, encuestas de turismo hotelero y estadísticas provinciales.
- **Open-Meteo** (reanálisis ERA5 del ECMWF): histórico de variables climáticas mensuales (temperatura media, precipitación acumulada y velocidad máxima del viento) para las coordenadas de Ushuaia.

---

## 9. Conclusión

La correcta previsión de la demanda turística mediante Inteligencia Artificial es un paso clave hacia la transformación digital y la gobernanza basada en datos en Tierra del Fuego. Este proyecto busca proponer una solución técnica sólida a un problema económico real, ejecutando el ciclo completo de un proyecto de Ciencia de Datos: desde la ingesta y tratamiento de datos reales, el diseño y optimización de modelos, hasta la entrega de métricas de negocio útiles para el desarrollo sostenible de la región.
