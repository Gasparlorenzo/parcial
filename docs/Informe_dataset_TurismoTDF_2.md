# Predicción de la demanda turística en Ushuaia — Tierra del Fuego

### Mediante técnicas de aprendizaje automático

**Entrega 2: Descripción del Dataset y Origen** · Mayo 2026

---

## 1. Introducción y objetivo del proyecto

El turismo representa uno de los motores económicos más importantes de Ushuaia y la provincia de Tierra del Fuego. La capacidad de anticipar el volumen de visitantes con meses de anticipación permite a los actores del sector —hotelería, transporte, gastronomía, agencias y organismos públicos— planificar su oferta y recursos de manera más eficiente.

Este proyecto tiene como objetivo construir un modelo de aprendizaje automático que prediga el total mensual de viajeros que arriban a Ushuaia, utilizando series temporales históricas enriquecidas con variables climáticas y de oferta hotelera. El modelo deberá ser capaz de proyectar la demanda con un horizonte de al menos tres a seis meses.

---

## 2. Origen y fuentes del dataset

### 2.1 Fuente principal: IPIEC

Los datos de turismo provienen del **Instituto Provincial de Estadística y Censos (IPIEC)** de la Provincia de Tierra del Fuego, Antártida e Islas del Atlántico Sur. El IPIEC publica estadísticas mensuales del sector turístico de Ushuaia en su portal de datos abiertos, incluyendo información de la Encuesta de Ocupación Hotelera (EOH) y registros del movimiento de pasajeros.

- **Acceso:** https://ipiec.tierradelfuego.gob.ar/
- **Fecha de adquisición:** Mayo de 2026
- **Cobertura temporal original:** Enero 2004 – Noviembre 2025 (263 registros mensuales)

### 2.2 Fuente climática: Open-Meteo / ERA5

Las variables climáticas fueron incorporadas mediante la API histórica de **Open-Meteo**, que provee datos del reanálisis ERA5 del Centro Europeo de Previsiones Meteorológicas a Plazo Medio (ECMWF). Se extrajeron los valores mensuales correspondientes a las coordenadas geográficas de Ushuaia para el período 2004–2025.

**Variables extraídas:** temperatura media mensual (°C), precipitación acumulada mensual (mm) y velocidad máxima del viento (km/h).

### 2.3 Proceso de integración y preprocesamiento

Ambas fuentes fueron combinadas sobre la clave temporal `fecha` (año-mes), generando un único archivo `dataset_turismo_clima.xlsx`. Las transformaciones realizadas incluyen:

- Unificación de formato de fechas al primer día de cada mes.
- Joining de registros climáticos con registros de turismo por período.
- Identificación de valores faltantes sin imputación aún (documentada en la Sección 4).
- No se realizaron transformaciones sobre las variables originales del IPIEC para preservar su integridad.

---

## 3. Descripción del dataset

### 3.1 Resumen general

| Característica | Valor |
|---|---|
| Período cubierto | Enero 2004 – Noviembre 2025 |
| Total de instancias (filas) | 263 registros mensuales |
| Total de características (columnas) | 83 variables |
| Granularidad temporal | Mensual |
| Variable objetivo (target) | `ush_viaj_total` (viajeros totales) |
| Fuente principal | IPIEC – Instituto Provincial de Estadística y Censos, Tierra del Fuego |
| Fuente climática | Open-Meteo API (ERA5 reanalysis) |

### 3.2 Grupos de variables

Las 83 columnas del dataset se organizan en 7 grupos temáticos:

| Grupo | N° vars | Completitud | Descripción |
|---|---|---|---|
| Temporales | 4 | 100% | fecha, anio, mes (texto y numérico) |
| Viajeros y pernoctaciones | 46 | 100% / 13% | Totales, residentes, no residentes y desagregado por origen (solo desde 2020) |
| Estadía promedio | 3 | 100% | Noches promedio por viajero (total, residentes, no residentes) |
| Hotelería y alojamiento | 15 | 79% | Establecimientos, habitaciones, plazas, tasa de ocupación hotelera y de plazas |
| Parque Nacional Tierra del Fuego | 3 | 50% | Visitas totales, residentes y no residentes (desde 2013) |
| Cruceros | 8 | 9% | Recaladas y cruceristas por tipo: antártico, regional, internacional (desde 2021) |
| Clima | 3 | 100% | Temperatura media mensual (°C), precipitación acumulada (mm), velocidad máxima del viento (km/h) |

### 3.3 Estadísticas descriptivas de variables clave

| Variable | Media | Mín | Máx | Mediana | Desvío | Nulos |
|---|---|---|---|---|---|---|
| Viajeros totales (target) | 22.285 | 0 | 45.653 | 23.062 | 10.411 | 0 |
| Pernoctaciones totales | 57.746 | 0 | 106.544 | 60.864 | 25.328 | 0 |
| Estadía promedio (noches) | 2,69 | 0,00 | 10,70 | 2,58 | 0,70 | 0 |
| Tasa de ocupación hotelera (%) | 50,97 | 1,50 | 83,24 | 54,13 | 18,31 | 3 |
| Tasa de ocupación de plazas (%) | 39,86 | 1,90 | 70,80 | 41,20 | 15,05 | 4 |
| Temperatura media (°C) | 4,32 | -5,60 | 14,20 | 3,90 | 4,22 | 0 |
| Precipitación acumulada (mm) | 2,42 | 0,00 | 20,90 | 1,10 | 3,42 | 0 |
| Velocidad máx. viento (km/h) | 15,31 | 3,20 | 44,30 | 14,30 | 6,58 | 0 |

---

## 4. Análisis de datos faltantes

El dataset presenta una estructura de completitud heterogénea, que refleja la disponibilidad histórica de las distintas fuentes:

- **Variables con cobertura completa (100%):** todas las variables de turismo agregadas (viajeros, pernoctaciones, estadía), el período temporal y las tres variables climáticas. Estas 16 variables conforman el núcleo del modelo.
- **Variables de hotelería:** disponibles desde 2008, con un 79% de cobertura (faltan 55 registros correspondientes al período 2004–2007).
- **Visitas al Parque Nacional:** disponibles desde 2013, con un 50% de completitud (faltan 132 registros).
- **Datos desagregados por origen** (residentes/no residentes por provincia y país): disponibles solo desde 2020, representando el 13% del período total (35 registros de 263).
- **Datos de cruceros y temporada:** disponibles únicamente desde la temporada 2021/2022, con menos del 10% de completitud (24 registros).

Para el modelo predictivo, se utilizarán exclusivamente las variables con cobertura del 79% o superior, evitando imputaciones sobre series con menos del 50% de datos. Las variables con alta ausencia se reservan para análisis exploratorios o modelos complementarios acotados al período con datos.

---

## 5. Relevancia de las variables para el modelo

A continuación se detalla el rol previsto para cada variable en el modelo de predicción, junto con su justificación:

| Variable | Rol en modelo | Justificación |
|---|---|---|
| `ush_viaj_total` | Target | Variable a predecir: total de viajeros mensuales en Ushuaia |
| `mes.1` (mes numérico) | Feature | Captura la estacionalidad, el predictor más importante dada la marcada variación mensual |
| `anio` | Feature | Captura la tendencia histórica de crecimiento del turismo |
| `temperature_2m_mean` | Feature | Temperatura media mensual; el clima de Ushuaia es factor clave para ciertos segmentos turísticos |
| `precipitation_sum` | Feature | Precipitación mensual acumulada como proxy de condiciones climáticas adversas |
| `wind_speed_10m_max` | Feature | Velocidad máxima del viento; relevante para actividades al aire libre y navegación |
| `ush_toh %` / `ush_top %` | Feature | Tasas de ocupación hotelera y de plazas: proxy de oferta disponible y demanda previa |
| `ush_plazas_disponibles` | Feature | Capacidad total de alojamiento: limita el máximo de turistas que puede recibir la ciudad |

La variable `ush_viaj_total` presenta una marcada estacionalidad: los meses de enero, febrero y noviembre concentran los picos de demanda (temporada de verano austral y cruceros antárticos), mientras que los meses de mayo y junio registran los valores mínimos. Esta estructura estacional es el principal patrón que el modelo deberá capturar.

---

## 6. Consideraciones éticas y de uso

Los datos utilizados son de dominio público, publicados por organismos estatales argentinos con fines estadísticos. No contienen información personal ni sensible. Su uso para investigación y desarrollo de modelos predictivos es consistente con el propósito declarado por las fuentes originales.

El dataset integrado (`dataset_turismo_clima.xlsx`) se incluye en el repositorio Git del proyecto junto con este documento.

Repositorio: https://github.com/Gasparlorenzo/parcial.git

---

## 7. Referencias

- **IPIEC** – Instituto Provincial de Estadística y Censos de Tierra del Fuego: https://ipiec.tierradelfuego.gob.ar/
- **Open-Meteo** Historical Weather API: https://open-meteo.com/en/docs/historical-weather-api
- **Copernicus Climate Change Service / ECMWF** ERA5 Reanalysis: https://cds.climate.copernicus.eu/
- **datos.gob.ar** – Portal Nacional de Datos Abiertos: https://datos.gob.ar/
