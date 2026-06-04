<div align="center">

<img src="docs/img/banner.png" alt="Predicción de Demanda Turística - Tierra del Fuego" width="100%"/>

<br/>

# 🏔️ Predicción de Demanda Turística — Tierra del Fuego

**Modelo de aprendizaje automático para predecir el total mensual de viajeros que arriban a Ushuaia, Tierra del Fuego (Argentina), utilizando series temporales históricas enriquecidas con variables climáticas y de oferta hotelera.**

<br/>

![Python](https://img.shields.io/badge/Python-3.9%2B-3776AB?style=for-the-badge&logo=python&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)
![pandas](https://img.shields.io/badge/pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white)

![Status](https://img.shields.io/badge/estado-en%20desarrollo-yellow?style=flat-square)
![License](https://img.shields.io/badge/licencia-MIT-blue?style=flat-square)
![Made with](https://img.shields.io/badge/hecho%20en-Tierra%20del%20Fuego-e98a4b?style=flat-square)

</div>

---

## 📑 Tabla de Contenidos

- [📖 Descripción del proyecto](#-descripción-del-proyecto)
- [📂 Estructura del repositorio](#-estructura-del-repositorio)
- [📊 Dataset](#-dataset)
  - [Grupos de variables](#grupos-de-variables)
  - [Features seleccionadas](#features-seleccionadas-para-el-modelo)
- [⚙️ Requisitos e instalación](#️-requisitos-e-instalación)
- [🚀 Uso](#-uso)
- [📈 Resultados](#-resultados)
- [🧪 Notas metodológicas](#-notas-metodológicas)
- [📚 Referencias](#-referencias)
- [✍️ Autoría](#️-autoría)

---

## 📖 Descripción del proyecto

El turismo es uno de los principales motores económicos de Ushuaia y la provincia de Tierra del Fuego. La marcada estacionalidad de la región —con picos en el verano austral (enero–febrero) y valles profundos en invierno (mayo–junio)— genera incertidumbre operativa tanto para el sector público como el privado.

Este proyecto construye un **modelo predictivo** capaz de anticipar la demanda turística mensual con un **horizonte de 3 a 6 meses**, apoyando decisiones en hotelería, transporte, gastronomía e infraestructura.

> 🎯 **Objetivo:** estimar `ush_viaj_total` (viajeros totales mensuales) a partir de variables históricas, climáticas y de oferta hotelera.

---

## 📂 Estructura del repositorio

```
.
├── data/
│   ├── raw/                # Datos originales sin modificar
│   ├── interim/            # Datos intermedios en procesamiento
│   └── processed/          # Datos limpios y preprocesados
├── docs/
│   └── img/                # Imágenes y gráficos del proyecto
├── models/                 # Modelos entrenados (.pkl, .h5, .joblib)
├── notebooks/              # Jupyter Notebooks de exploración y análisis (EDA)
├── src/                    # Código fuente (entrenamiento y predicción)
├── requirements.txt        # Dependencias del proyecto
└── README.md
```

---

## 📊 Dataset

| Característica | Detalle |
|---|---|
| **Período cubierto** | Enero 2004 – Noviembre 2025 |
| **Instancias** | 263 registros mensuales |
| **Variables** | 83 columnas (7 grupos temáticos) |
| **Variable objetivo** | `ush_viaj_total` (viajeros totales mensuales) |
| **Fuente principal** | [IPIEC – Instituto Provincial de Estadística y Censos, TDF](https://ipiec.tierradelfuego.gob.ar/) |
| **Fuente climática** | [Open-Meteo API (ERA5 reanalysis)](https://open-meteo.com/en/docs/historical-weather-api) |

### Grupos de variables

| Grupo | Variables | Cobertura |
|-------|-----------|-----------|
| 📅 Temporales | fecha, año, mes | 100% |
| 🧳 Viajeros y pernoctaciones | totales, residentes, no residentes | 100% |
| 🛏️ Estadía promedio | noches promedio por viajero | 100% |
| 🏨 Hotelería y alojamiento | establecimientos, plazas, tasas de ocupación | 79% |
| 🌲 Parque Nacional TDF | visitas totales y por origen | 50% |
| 🚢 Cruceros | recaladas, cruceristas por tipo | 9% |
| 🌦️ Clima | temperatura, precipitación, viento | 100% |

### Features seleccionadas para el modelo

```python
mes_num, anio, temperature_2m_mean, precipitation_sum,
wind_speed_10m_max, ush_toh_pct, ush_top_pct, ush_plazas_disponibles
```

---

## ⚙️ Requisitos e instalación

**Requisitos**

- Python `>= 3.9`
- pandas · numpy · scikit-learn
- matplotlib · seaborn · openpyxl

**Instalación**

```bash
git clone https://github.com/tuusuario/turismo-tdf-ml
cd turismo-tdf-ml
pip install -r requirements.txt
```

---

## 🚀 Uso

```bash
# Análisis exploratorio
jupyter notebook notebooks/exploracion.ipynb

# Entrenamiento del modelo
python src/modelo.py
```

---

## 📈 Resultados

### Análisis exploratorio

La serie muestra una **fuerte estacionalidad anual**, con máximos en verano y mínimos en invierno.

<div align="center">
<img src="docs/img/serie_temporal.png" alt="Serie temporal de viajeros mensuales" width="80%"/>
<br/><em>Figura 1 — Evolución mensual de viajeros (2004–2025).</em>
</div>

<br/>

<div align="center">
<img src="docs/img/correlacion.png" alt="Matriz de correlación" width="70%"/>
<br/><em>Figura 2 — Matriz de correlación entre features y la variable objetivo.</em>
</div>

### Desempeño del modelo

| Modelo | R² (test) | RMSE | MAE |
|--------|:---------:|:----:|:---:|
| Regresión Lineal | — | — | — |
| Árbol de Decisión | — | — | — |
| KNN | — | — | — |
| SVM | — | — | — |

> ℹ️ *Completar con las métricas finales obtenidas sobre el conjunto de prueba (2023–2025).*

<div align="center">
<img src="docs/img/pred_vs_real.png" alt="Predicción vs valores reales" width="80%"/>
<br/><em>Figura 3 — Predicción del modelo frente a los valores reales en el período de test.</em>
</div>

---

## 🧪 Notas metodológicas

- 🦠 El período **2020–2021** presenta valores atípicos extremos por COVID-19. Se evalúa el uso de una variable *dummy* o la exclusión del período para el entrenamiento.
- 📉 Se utilizan únicamente variables con **≥ 79% de cobertura** para el modelo principal. Las variables con alta ausencia (cruceros, desagregado por origen) quedan reservadas para análisis exploratorio.
- 🔒 **No se realizaron imputaciones** sobre las variables originales del IPIEC para preservar la integridad de los datos.
- ⏳ La división **train/test es temporal** (entrenamiento hasta 2022, prueba 2023–2025), respetando el orden cronológico propio de las series de tiempo.

---

## 📚 Referencias

- [IPIEC – Tierra del Fuego](https://ipiec.tierradelfuego.gob.ar/)
- [Open-Meteo Historical Weather API](https://open-meteo.com/en/docs/historical-weather-api)
- [ERA5 Reanalysis – ECMWF / Copernicus](https://cds.climate.copernicus.eu/)
- [datos.gob.ar – Portal Nacional de Datos Abiertos](https://datos.gob.ar/)

---

## ✍️ Autoría

Proyecto desarrollado para la materia **Aprendizaje Automático** — Politecnico Malvinas Argentinas, 2026.

<div align="center">
<br/>
<sub>🏔️ Hecho en el fin del mundo · Ushuaia, Tierra del Fuego 🇦🇷</sub>
</div>
