# Predicción de la Demanda Turística en Ushuaia — Tierra del Fuego

### Informe Final · Mediante Modelos de Aprendizaje Automático

**Materia:** Aprendizaje Automático — 3.º Cuatrimestre
**Institución:** Centro Politécnico Superior Malvinas Argentinas
**Profesor:** Nicolás Caballero
**Autor:** Darío Martínez · 2026

---

## Resumen ejecutivo

El turismo es uno de los principales motores económicos de Ushuaia y la provincia de Tierra del Fuego, con una demanda marcadamente estacional que genera incertidumbre operativa en hotelería, transporte e infraestructura. Este proyecto desarrolla modelos de **Regresión Lineal Múltiple (MCO)** para predecir la demanda turística mensual sobre **tres variables objetivo**: viajeros totales, pernoctaciones totales y visitas al Parque Nacional Tierra del Fuego.

A partir de una serie temporal mensual de 2004 a 2025 (263 registros) que integra datos del IPIEC y variables climáticas de Open-Meteo (reanálisis ERA5), se entrenó un modelo independiente por cada target. El modelo de **viajeros** obtuvo el mejor desempeño (R² = 0,828 en test), seguido por **pernoctaciones** (R² = 0,807); el de **Parque Nacional** resultó más débil (R² = 0,452), condicionado por la menor cantidad de datos disponibles. Con los modelos se construyó una proyección de demanda para diciembre 2025 – noviembre 2026 que reproduce correctamente los patrones estacionales históricos.

---

## 1. Introducción y contexto

El turismo es un motor económico fundamental de Ushuaia, polo de turismo internacional y puerta de entrada a la Antártida. El impacto de la afluencia de visitantes se derrama directamente sobre la hotelería, gastronomía, transporte local, agencias de excursiones y comercio minorista.

La demanda turística regional presenta alta volatilidad y estacionalidad, influida por factores geográficos, climáticos (temporadas de nieve), conectividad aérea y turismo de cruceros. Esta predictibilidad limitada genera ineficiencias tanto en el sector público como en el privado:

- **Sector privado:** dificultad para dimensionar personal, prever compras de insumos o gestionar tarifas dinámicas.
- **Sector público:** desafíos para planificar infraestructura, gestionar saturación de áreas protegidas y coordinar contingencias.

El uso de técnicas de Aprendizaje Automático permite procesar datos históricos multifactoriales, identificar patrones y transformar los registros estadísticos en herramientas predictivas de valor estratégico para la planificación.

---

## 2. Objetivo

Desarrollar y validar modelos de Aprendizaje Automático que predigan la demanda turística mensual de Ushuaia sobre tres variables objetivo, con un horizonte de planificación de 3 a 6 meses:

1. **Viajeros totales** (`ush_viaj_total`)
2. **Pernoctaciones totales** (`ush_pernoc_total`)
3. **Visitas al Parque Nacional** (`parque_visitas_total`)

Se entrena un modelo de Regresión Lineal Múltiple independiente por cada target, cada uno con su propio conjunto de features seleccionadas.

El proyecto se define como un problema de **Aprendizaje Supervisado de Regresión**, ya que las tres variables objetivo son cuantitativas continuas.

---

## 3. Dataset y fuentes

| Característica | Valor |
|---|---|
| Período cubierto | Enero 2004 – Noviembre 2025 |
| Instancias (filas) | 263 registros mensuales |
| Características (columnas) | 83 variables |
| Granularidad | Mensual |
| Variables objetivo | 3 (viajeros, pernoctaciones, Parque Nacional) |
| Fuente principal | IPIEC – Instituto Provincial de Estadística y Censos, TDF |
| Fuente climática | Open-Meteo API (reanálisis ERA5 / ECMWF) |

### 3.1 Origen de los datos

- **IPIEC:** estadísticas mensuales del sector turístico de Ushuaia, incluyendo la Encuesta de Ocupación Hotelera (EOH) y el movimiento de pasajeros. Acceso: https://ipiec.tierradelfuego.gob.ar/
- **Open-Meteo (ERA5):** valores climáticos mensuales para las coordenadas de Ushuaia —temperatura media (°C), precipitación acumulada (mm) y velocidad máxima del viento (km/h)—. Acceso: https://open-meteo.com/en/docs/historical-weather-api

Ambas fuentes se combinaron sobre la clave temporal `fecha` (año-mes) en un único archivo `dataset_turismo_clima.xlsx`.

### 3.2 Grupos de variables

| Grupo | Cobertura | Descripción |
|---|---|---|
| Temporales | 100% | fecha, año, mes |
| Viajeros y pernoctaciones | 100% | Totales (residentes/no residentes desagregados desde 2020) |
| Estadía promedio | 100% | Noches promedio por viajero |
| Hotelería y alojamiento | 79% | Establecimientos, habitaciones, plazas, tasas de ocupación |
| Parque Nacional TDF | 50% | Visitas totales (desde 2015) |
| Cruceros | 9% | Recaladas y cruceristas (desde 2021) |
| Clima | 100% | Temperatura, precipitación, viento |

---

## 4. Metodología

### 4.1 Preprocesamiento

1. **Imputación por mediana mensual:** los nulos de las variables hoteleras se reemplazan con la mediana histórica del mismo mes, preservando la estacionalidad.
2. **Exclusión del período COVID** (marzo 2020 – junio 2021): evento atípico que distorsionaría el aprendizaje. Quedan 247 registros.
3. **División temporal:** entrenamiento con datos hasta 2022 (212 meses) y evaluación desde 2023 (35 meses), respetando el orden cronológico propio de las series de tiempo y evitando la fuga de información.

### 4.2 Selección de variables

Sobre 9 features candidatas (`anio`, `mes.1`, `ush_toh %`, `ush_top %`, `ush_hab_disponibles`, `ush_plazas_disponibles`, `temperature_2m_mean`, `precipitation_sum`, `wind_speed_10m_max`) se aplicó una selección en dos pasos, **por cada target**:

- **Paso 1 — Correlación:** se descartan las features con correlación absoluta con el target inferior a 0,10.
- **Paso 2 — VIF iterativo:** sobre variables estandarizadas, se elimina la multicolinealidad removiendo iterativamente la feature con mayor Factor de Inflación de la Varianza hasta que todas quedan por debajo de 10.

Por ejemplo, `ush_toh %` y `ush_top %` correlacionan fuertemente con los targets pero entre sí lo hacen en 0,97; el VIF elimina una de las dos por multicolinealidad. El resultado es un subconjunto de features propio de cada modelo.

### 4.3 Modelo

- **Algoritmo:** Regresión Lineal Múltiple (mínimos cuadrados ordinarios, sin hiperparámetros). Se evaluó SVR como comparación, pero se confirmó que la relación es predominantemente lineal, por lo que se optó por MCO por su buen desempeño e interpretabilidad.
- **Un modelo por target**, cada uno con sus features seleccionadas.
- **Escalado** con `StandardScaler`, ajustado solo en train y aplicado a test, para evitar fuga de información y hacer comparables los coeficientes.
- **Validación cruzada** para estimar la estabilidad del R².

La forma general del modelo es:

```
ŷ = β₀ + β₁·año + β₂·mes + β₃·ocupación + β₄·temperatura + … + ε
```

---

## 5. Análisis exploratorio (EDA)

- Las tres series muestran **tendencia creciente** desde 2004 con estacionalidad marcada.
- **Dos temporadas altas:** verano austral (enero–febrero) por turismo internacional e invierno (julio–agosto) por turismo de nieve. El valle más profundo ocurre en mayo–junio.
- Las **visitas al Parque Nacional** siguen un patrón principalmente estival.
- El impacto del COVID (2020–2021) es visible como una caída abrupta; **tras la pandemia el turismo se recuperó y superó los niveles previos a 2020**.
- Los valores extremos detectados (método IQR) no son errores de medición sino picos legítimos de temporada alta; por tratarse de una serie temporal, se conservan para no destruir la señal estacional.

---

## 6. Resultados

Métricas sobre el conjunto de prueba (2023–2025), un modelo por variable objetivo:

| Variable objetivo | R² (test) | R² CV | RMSE | MAE |
|-------------------|:---------:|:-----:|:----:|:---:|
| Viajeros totales | **0,828** | 0,874 | 3.480 | 2.669 |
| Pernoctaciones totales | 0,807 | 0,903 | 8.114 | 5.337 |
| Visitas Parque Nacional | 0,452 | 0,241 | 12.308 | 10.239 |

**Lectura:**

- **Viajeros totales** es el mejor modelo: explica ~83% de la variación, con un error promedio de unos 2.700 viajeros/mes.
- **Pernoctaciones** muestra buen ajuste (~81%), con un R² CV alto (0,903) que confirma su estabilidad.
- **Parque Nacional** es el más débil (R² = 0,452) y su R² CV bajo (0,241) refleja la menor cantidad de datos disponibles (desde 2015).

### 6.1 Importancia de variables

Como las variables están estandarizadas, los coeficientes son comparables entre sí:

- **`ush_top %`** (ocupación de plazas): predictor dominante en viajeros y pernoctaciones.
- **`temperature_2m_mean`**: peso alto en el Parque Nacional y relevante en viajeros — a mayor temperatura, más turistas.
- **`anio`** captura la tendencia de crecimiento y **`mes.1`** la estacionalidad.

### 6.2 Diagnóstico

- **Predicho vs Real:** en viajeros y pernoctaciones los puntos se alinean estrechamente sobre la diagonal de predicción perfecta; en el Parque la nube está más dispersa, coherente con su menor R².
- **Residuos vs Predicho:** los residuos se distribuyen alrededor de cero en los tres modelos, con una dispersión que crece levemente hacia valores altos (indicio de leve heterocedasticidad).

---

## 7. Proyección diciembre 2025 – noviembre 2026

Para construir las features futuras se utilizó la **mediana histórica de cada mes** (sin COVID) en las variables hoteleras y climáticas, actualizando únicamente `anio` y `mes.1`. Representa un **escenario base sin shocks externos**.

| Mes | Viajeros | Pernoctaciones | Parque Nacional |
|---|---:|---:|---:|
| Dic 2025 | 29.850 | 69.811 | 36.803 |
| Ene 2026 | 38.498 | 91.738 | 54.915 |
| Feb 2026 | 32.095 | 80.104 | 51.164 |
| Mar 2026 | 29.517 | 69.149 | 39.968 |
| Abr 2026 | 18.401 | 46.464 | 24.711 |
| May 2026 | 10.237 | 31.522 | 13.338 |
| Jun 2026 | 9.258 | 29.335 | 5.098 |
| Jul 2026 | 18.767 | 56.043 | 10.252 |
| Ago 2026 | 21.541 | 69.271 | 15.184 |
| Sep 2026 | 25.932 | 73.717 | 23.209 |
| Oct 2026 | 23.725 | 62.079 | 24.400 |
| Nov 2026 | 29.843 | 78.499 | 36.937 |

La proyección reproduce los patrones estacionales históricos: picos en verano (enero–febrero) e invierno (julio–agosto) y valle en mayo–junio. Estas estimaciones constituyen un escenario orientativo para apoyar la planificación, no una predicción exacta. Los valores se acotan a un mínimo de cero en los meses valle.

---

## 8. Conclusiones

- Los modelos de Regresión Lineal Múltiple resultaron herramientas efectivas para predecir la demanda turística de Ushuaia, especialmente en **viajeros (R² 0,83)** y **pernoctaciones (R² 0,81)**.
- Su principal fortaleza es la **interpretabilidad**: los coeficientes permiten identificar cómo influye cada variable sobre la demanda.
- El modelo del **Parque Nacional (R² 0,45)** es más débil por la menor cantidad de datos disponibles desde 2015.
- La metodología (selección Correlación + VIF, split temporal, exclusión COVID, escalado solo en train) garantiza la validez de la evaluación y la ausencia de fuga de información.

---

## 9. Limitaciones y líneas futuras

- **Transformación logarítmica del target** para atenuar la leve heterocedasticidad observada en los residuos.
- **Incorporar lags temporales** (demanda del mes anterior o del mismo mes del año previo) como nuevas features de la regresión.
- **Ampliar la base de datos del Parque Nacional** para mejorar su modelo.
- **Incorporar variables de shocks externos** (tipo de cambio, eventos) que impacten sobre la actividad turística.

Organismos como el IPIEC o la Secretaría de Turismo podrían utilizar este tipo de modelos para apoyar procesos de planificación y monitoreo basados en evidencia.

---

## 10. Reproducibilidad

- **Notebook principal:** `01_prediccion_demanda_turistica_v2.ipynb`
- **Descarga de clima:** `00_descarga_clima_openmeteo.ipynb`
- **Dataset integrado:** `data/processed/dataset_turismo_clima.xlsx`
- **Repositorio:** https://github.com/Gasparlorenzo/parcial.git

---

## Referencias

- IPIEC – Instituto Provincial de Estadística y Censos de Tierra del Fuego: https://ipiec.tierradelfuego.gob.ar/
- Open-Meteo Historical Weather API: https://open-meteo.com/en/docs/historical-weather-api
- Copernicus Climate Change Service / ECMWF — ERA5 Reanalysis: https://cds.climate.copernicus.eu/
- datos.gob.ar — Portal Nacional de Datos Abiertos: https://datos.gob.ar/
