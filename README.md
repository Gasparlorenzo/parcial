#  Predicción de Demanda Turística — Tierra del Fuego



Modelo de aprendizaje automático para predecir el total mensual de viajeros que arriban a Ushuaia, Tierra del Fuego (Argentina), utilizando series temporales históricas enriquecidas con variables climáticas y de oferta hotelera.



---



##  Descripción del proyecto



El turismo es uno de los principales motores económicos de Ushuaia y la provincia de Tierra del Fuego. La marcada estacionalidad de la región —con picos en el verano austral (enero–febrero) y valles profundos en invierno (mayo–junio)— genera incertidumbre operativa tanto para el sector público como el privado.



Este proyecto construye un modelo predictivo capaz de anticipar la demanda turística mensual con un horizonte de 3 a 6 meses, apoyando decisiones en hotelería, transporte, gastronomía e infraestructura.



---



## 📂 Estructura del repositorio



```

.

├── data/

│   ├── raw/                # Datos originales sin modificar

│   ├── interim/            # Datos intermedios en procesamiento

│   └── processed/          # Datos limpios y preprocesados

├── models/                 # Modelos entrenados (.pkl, .h5, .joblib)

├── notebooks/              # Jupyter Notebooks de exploración y análisis (EDA)

├── src/                    # Código fuente (entrenamiento y predicción)

├── requirements.txt        # Dependencias del proyecto

└── README.md

```



\---



##  Dataset



| Característica | Detalle |

|---|---|

| \*\*Período cubierto\*\* | Enero 2004 – Noviembre 2025 |

| \*\*Instancias\*\* | 263 registros mensuales |

| \*\*Variables\*\* | 83 columnas (7 grupos temáticos) |

| \*\*Variable objetivo\*\* | `ush\_viaj\_total` (viajeros totales mensuales) |

| \*\*Fuente principal\*\* | \[IPIEC – Instituto Provincial de Estadística y Censos, TDF](https://ipiec.tierradelfuego.gob.ar/) |

| \*\*Fuente climática\*\* | \[Open-Meteo API (ERA5 reanalysis)](https://open-meteo.com/en/docs/historical-weather-api) |



### Grupos de variables



| Grupo | Variables | Cobertura |

|-------|-----------|-----------|

| Temporales | fecha, año, mes | 100% |

| Viajeros y pernoctaciones | totales, residentes, no residentes | 100% |

| Estadía promedio | noches promedio por viajero | 100% |

| Hotelería y alojamiento | establecimientos, plazas, tasas de ocupación | 79% |

| Parque Nacional TDF | visitas totales y por origen | 50% |

| Cruceros | recaladas, cruceristas por tipo | 9% |

| Clima | temperatura, precipitación, viento | 100% |



\### Features seleccionadas para el modelo



```

mes\_num, anio, temperature\_2m\_mean, precipitation\_sum,

wind\_speed\_10m\_max, ush\_toh\_pct, ush\_top\_pct, ush\_plazas\_disponibles

```



---



##  Requisitos



```

Python >= 3.9

pandas

numpy

scikit-learn

matplotlib

seaborn

openpyxl

```



### Instalación



```bash

git clone https://github.com/tuusuario/turismo-tdf-ml

cd turismo-tdf-ml

pip install -r requirements.txt

```



---



\##  Uso



```bash

# Análisis exploratorio

jupyter notebook notebooks/exploracion.ipynb



# Entrenamiento del modelo

python src/modelo.py

```



\---



##  Resultados preliminares



\*(Se actualizará con métricas finales: RMSE, MAE, R²)\*



---



##  Notas metodológicas



\- El período \*\*2020–2021\*\* presenta valores atípicos extremos por COVID-19. Se evalúa el uso de una variable dummy o exclusión del período para el entrenamiento.

\- Se utilizan únicamente variables con \*\*≥ 79% de cobertura\*\* para el modelo principal. Las variables con alta ausencia (cruceros, desagregado por origen) quedan reservadas para análisis exploratorio.

\- No se realizaron imputaciones sobre las variables originales del IPIEC para preservar la integridad de los datos.



---



##  Referencias



\- \[IPIEC – Tierra del Fuego](https://ipiec.tierradelfuego.gob.ar/)

\- \[Open-Meteo Historical Weather API](https://open-meteo.com/en/docs/historical-weather-api)

\- \[ERA5 Reanalysis – ECMWF / Copernicus](https://cds.climate.copernicus.eu/)

\- \[datos.gob.ar – Portal Nacional de Datos Abiertos](https://datos.gob.ar/)



---



##  Autoría



Proyecto desarrollado para la materia \*\*Aprendizaje Automático\*\* — Universidad Nacional de Tierra del Fuego, 2026.

