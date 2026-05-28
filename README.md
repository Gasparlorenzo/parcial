# Parcial ML2026

## Predicción de la Demanda Turística en Tierra del Fuego Mediante Aprendizaje Automático

Este estudio presenta un modelo de aprendizaje automático para predecir la demanda turística en Tierra del Fuego, Argentina. El objetivo del proyecto es analizar datos históricos de turismo e identificar patrones relacionados con la actividad turística estacional y el comportamiento de los visitantes. La demanda turística en la región está fuertemente influenciada por las condiciones climáticas, la conectividad aeroportuaria, el turismo de cruceros y las variaciones estacionales, las cuales generan incertidumbre operativa tanto en el sector público como en el privado. Los datos fueron recolectados de fuentes estadísticas oficiales, incluyendo registros de ocupación hotelera, indicadores turísticos, actividad aeroportuaria, arribos de cruceros y variables climáticas. Se evaluaron varios modelos de aprendizaje automático, como Regresión Lineal, Árboles de Decisión y Regresión por Vectores de Soporte, para predecir la demanda turística mensual y analizar relaciones complejas entre variables. Los resultados mostraron que los patrones históricos de turismo, las condiciones climáticas y los indicadores de transporte pueden mejorar la precisión de las predicciones y apoyar procesos de toma de decisiones basados en datos. Además, el modelo propuesto puede ayudar a las organizaciones turísticas a optimizar estrategias de planificación, gestión de recursos y organización de infraestructura en entornos altamente estacionales. Asimismo, este proyecto demuestra cómo la Inteligencia Artificial puede aplicarse para resolver problemas económicos y operativos reales mediante análisis predictivo y análisis de datos históricos.


## Organización del Proyecto

```
├── LICENSE            <- Licencia del proyecto.
├── Makefile           <- Archivo de automatización de comandos.
├── README.md          <- Documento principal del proyecto para desarrolladores que utilizan este proyecto.
├── data
│   ├── interim        <- Datos intermedios que fueron transformados.
│   ├── processed      <- Conjuntos de datos finales listos para el modelado.
│   └── raw            <- Datos originales sin modificar.
├── docs               <- Proyecto predeterminado de MkDocs; ver www.mkdocs.org para más detalles.
│
├── models             <- Modelos entrenados y serializados, predicciones del modelo o resúmenes del modelo.
│
├── notebooks          <- Jupyter notebooks. La convención de nombres usa un número (para ordenarlos),
│			 				las iniciales del creador y una breve descripción separada por guiones.
│                         
│
├── pyproject.toml     <- Archivo de configuración del proyecto con metadatos del paquete y 
│							configuración para herramientas como Black.
│
├── references         <- references → Diccionarios de datos, manuales y otros materiales explicativos.
│
├── reports            <- Análisis generados en formato HTML, PDF, LaTeX, etc.
│   └── figures        <- Gráficos e imágenes generadas para ser utilizadas en informes.
│
├── requirements.txt   <- Archivo de requisitos para reproducir el entorno de análisis, 
│							por ejemplo generado con: pip freeze > requirements.txt
│
├── setup.cfg          <- Archivo de configuración para herramientas como flake8

