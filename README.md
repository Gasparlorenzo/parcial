Parcial Aprendizaje2026

##Predicción de la Demanda Turística en Tierra del Fuego Mediante Aprendizaje Automático##

Este estudio presenta un modelo de aprendizaje automático para predecir la demanda turística en Tierra del Fuego, Argentina. El objetivo del proyecto es analizar datos históricos de turismo e identificar patrones relacionados con la actividad turística estacional y el comportamiento de los visitantes. La demanda turística en la región está fuertemente influenciada por las condiciones climáticas, la conectividad aeroportuaria, el turismo de cruceros y las variaciones estacionales, las cuales generan incertidumbre operativa tanto en el sector público como en el privado. Los datos fueron recolectados de fuentes estadísticas oficiales, incluyendo registros de ocupación hotelera, indicadores turísticos, actividad aeroportuaria, arribos de cruceros y variables climáticas. Se evaluaron varios modelos de aprendizaje automático, como Regresión Lineal, Árboles de Decisión y Regresión por Vectores de Soporte, para predecir la demanda turística mensual y analizar relaciones complejas entre variables. Los resultados mostraron que los patrones históricos de turismo, las condiciones climáticas y los indicadores de transporte pueden mejorar la precisión de las predicciones y apoyar procesos de toma de decisiones basados en datos. Además, el modelo propuesto puede ayudar a las organizaciones turísticas a optimizar estrategias de planificación, gestión de recursos y organización de infraestructura en entornos altamente estacionales. Asimismo, este proyecto demuestra cómo la Inteligencia Artificial puede aplicarse para resolver problemas económicos y operativos reales mediante análisis predictivo y análisis de datos históricos.


## Organización del Proyecto

```
├── LICENSE            <- Open-source license if one is chosen
├── Makefile           <- Makefile with convenience commands like `make data` or `make train`
├── README.md          <- The top-level README for developers using this project.
├── data
│   ├── external       <- Data from third party sources.
│   ├── interim        <- Intermediate data that has been transformed.
│   ├── processed      <- The final, canonical data sets for modeling.
│   └── raw            <- The original, immutable data dump.
│
├── docs               <- A default mkdocs project; see www.mkdocs.org for details
│
├── models             <- Trained and serialized models, model predictions, or model summaries
│
├── notebooks          <- Jupyter notebooks. Naming convention is a number (for ordering),
│                         the creator's initials, and a short `-` delimited description, e.g.
│                         `1.0-jqp-initial-data-exploration`.
│
├── pyproject.toml     <- Project configuration file with package metadata for 
│                         parcial_aprendizaje2026 and configuration for tools like black
│
├── references         <- Data dictionaries, manuals, and all other explanatory materials.
│
├── reports            <- Generated analysis as HTML, PDF, LaTeX, etc.
│   └── figures        <- Generated graphics and figures to be used in reporting
│
├── requirements.txt   <- The requirements file for reproducing the analysis environment, e.g.
│                         generated with `pip freeze > requirements.txt`
│
├── setup.cfg          <- Configuration file for flake8
│
└── parcial_aprendizaje2026   <- Source code for use in this project.
    │
    ├── __init__.py             <- Makes parcial_aprendizaje2026 a Python module
    │
    ├── config.py               <- Store useful variables and configuration
    │
    ├── dataset.py              <- Scripts to download or generate data
    │
    ├── features.py             <- Code to create features for modeling
    │
    ├── modeling                
    │   ├── __init__.py 
    │   ├── predict.py          <- Code to run model inference with trained models          
    │   └── train.py            <- Code to train models
    │
    └── plots.py                <- Code to create visualizations
```

--------

