<div align="center">

<img src="./banner.png" alt="Predicción de Demanda Turística - Tierra del Fuego" width="100%"/>

# Informe de Proyección de Demanda Turística · Ushuaia 2026

**Predicción mensual de viajeros, pernoctaciones y visitas al Parque Nacional**
mediante modelos de aprendizaje automático sobre datos históricos 2004–2025

`Ref. DT-USH-2026-01` · `Versión 1.0` · `Julio 2026`

**Preparado para:** Organismo de Gestión Turística · Tierra del Fuego
**Elaborado por:** Darío Martínez

</div>

---

## Nota de presentación

El presente informe responde al encargo de **anticipar la demanda turística mensual de Ushuaia**, con el fin de apoyar la planificación operativa del sector durante la temporada 2026.

Para ello se construyó un modelo a partir de **21 años de registros oficiales** de turismo y datos climáticos. El documento presenta, en lenguaje claro y orientado a la decisión, qué demanda esperar mes a mes, con qué grado de confianza, y qué acciones habilita esa anticipación. El detalle metodológico se incluye en el **Anexo Técnico** al final.

---

## El titular: la temporada de invierno 2026

<div align="center">

| 18.767 | 56.043 | ~83% |
|:------:|:------:|:----:|
| **Viajeros** estimados · Julio 2026 | **Pernoctaciones** estimadas · Julio 2026 | de la variación **explicada** (modelo de viajeros) |

</div>

Para **julio de 2026**, en plena temporada de nieve, se esperan cerca de **18.767 viajeros** y **56.043 pernoctaciones** en Ushuaia. Es el repunte invernal: por encima del valle de mayo–junio, aunque por debajo del pico de verano (enero, que ronda los 38.500 viajeros). De cara al verano, la demanda vuelve a crecer de forma sostenida desde septiembre.

---

## 1 · El patrón: la demanda se mueve en dos olas al año

El turismo de Ushuaia no es parejo: sube y baja con fuerza según la época. Conocer ese ritmo es la base para anticiparse.

<div align="center">
  <img src="./evolucion_historica_demanda_2004_2025.png" alt="Evolución histórica 2004-2025" width="92%"/>
  <br/>
  <em>Evolución mensual de viajeros, pernoctaciones y visitas al Parque Nacional (2004–2025). El bajón de 2020–2021 corresponde a la pandemia, tras la cual la demanda se recuperó y superó los niveles previos.</em>
</div>

<br/>

| Temporada | Meses | Qué significa para la operación |
|---|---|---|
| 🔺 **Alta — Verano** | Enero–Febrero | Pico del año, turismo internacional y cruceros antárticos |
| 🔺 **Alta — Invierno** | Julio–Agosto | Repunte por turismo de nieve. Ushuaia tiene dos temporadas, no una |
| 🔻 **Baja — Otoño** | Mayo–Junio | El valle más profundo. Momento natural para mantenimiento |
| ◾ **Transición** | Sep–Noviembre | Recuperación sostenida hacia el verano |

---

## 2 · Lo que viene: proyección mes a mes para 2026

El núcleo del encargo: cuánta demanda esperar en cada mes del año entrante, en un escenario normal sin sobresaltos.

<div align="center">
  <img src="./predicciones.png" alt="Proyección diciembre 2025 - noviembre 2026" width="95%"/>
  <br/>
  <em>Proyección Dic 2025 – Nov 2026 (en color) a continuación de los datos reales (en negro). Picos en verano e invierno, valle en mayo–junio.</em>
</div>

<br/>

> **Cómo leerlo — es un escenario base, no una bola de cristal.**
> La proyección asume condiciones típicas para cada mes. Un evento extraordinario —un cambio brusco del tipo de cambio, un shock externo— puede moverla. Sirve para planificar con confianza, revisándola cuando el contexto cambie.

---

## 3 · Qué hacer con esto

El valor de conocer la demanda con meses de adelanto está en las decisiones que se toman **antes** de que llegue.

1. **Dimensionar el personal** — contratar y capacitar para los picos de enero y julio con tiempo, en vez de buscar gente sobre la hora.
2. **Planificar compras e insumos** — ajustar stock y abastecimiento al volumen esperado de cada mes, reduciendo faltantes y sobrantes.
3. **Gestionar tarifas** — aprovechar los picos previstos con precios dinámicos y estimular la demanda en los valles.
4. **Coordinar infraestructura y áreas naturales** — anticipar la presión sobre el Parque Nacional y los servicios urbanos en los meses de mayor afluencia.

---

## 4 · Qué tan confiable es

No todas las predicciones tienen la misma solidez. Esta es la precisión de cada modelo, medida sobre datos reales de los últimos años (2023–2025) que el modelo no usó para entrenar.

<div align="center">
  <img src="./real_vs_predicho.png" alt="Real vs predicho 2023-2025" width="95%"/>
  <br/>
  <em>Predicción del modelo (línea de color) frente a lo que realmente ocurrió (línea negra). Cuanto más se pegan las líneas, mejor.</em>
</div>

<br/>

| Indicador | Precisión (R²) | Lectura |
|---|:---:|---|
| **Viajeros** | 83% | Predicción sólida, lista para usar |
| **Pernoctaciones** | 81% | Predicción sólida, lista para usar |
| **Parque Nacional** | 45% | Más incierta: datos disponibles solo desde 2015 |

**Viajeros y pernoctaciones** son predicciones confiables. **Parque Nacional** es más incierta y mejorará a medida que se acumule más historia de datos.

---

## 5 · Alcance y supuestos

<table>
<tr>
<th width="50%">✓ Qué cubre</th>
<th width="50%">— Qué no cubre</th>
</tr>
<tr>
<td valign="top">

- Proyección mensual de los tres indicadores
- Horizonte de 12 meses (Dic 2025 – Nov 2026)
- Escenario base en condiciones normales
- Nivel de confianza por indicador

</td>
<td valign="top">

- Eventos extraordinarios o shocks externos
- Desagregación por establecimiento o barrio
- Predicción diaria o por evento puntual
- Variables fuera de las fuentes oficiales usadas

</td>
</tr>
</table>

---

## 6 · Próximos pasos

Una proyección es más útil cuando se actualiza. Vías sugeridas de continuidad:

1. **Actualización periódica** — reentrenar con los nuevos datos del IPIEC a medida que se publican, idealmente cada trimestre.
2. **Mejorar el modelo del Parque Nacional** — incorporar más historia de visitas para elevar su confianza.
3. **Incorporar variables de contexto** — sumar señales como tipo de cambio o conectividad aérea para anticipar escenarios alternativos.

---
---

# Anexo Técnico

> *Esta sección documenta el detalle metodológico para los equipos que deseen auditar o reproducir el trabajo. No es necesaria para interpretar las conclusiones del informe.*

## A.1 · Datos

Serie mensual 2004–2025 (**263 registros**) que integra estadísticas turísticas del **IPIEC** (Encuesta de Ocupación Hotelera) con variables climáticas de **Open-Meteo** (reanálisis ERA5): temperatura media, precipitación acumulada y velocidad máxima del viento.

| Característica | Valor |
|---|---|
| Período | Enero 2004 – Noviembre 2025 |
| Registros | 263 meses |
| Variables objetivo | 3 (viajeros, pernoctaciones, Parque Nacional) |
| Features candidatas | 9 (temporales, hoteleras, climáticas) |

## A.2 · Preprocesamiento

Tres pasos preparan los datos antes de modelar: se imputan los nulos hoteleros con la mediana del mismo mes (para no romper la estacionalidad), se excluye el período COVID por atípico, y se divide en train/test respetando el orden temporal (nunca se entrena con datos del futuro).

```python
# 1. Imputar nulos hoteleros con la mediana del mismo mes
cols_hotel = ['ush_toh %', 'ush_top %',
              'ush_hab_disponibles', 'ush_plazas_disponibles']
for col in cols_hotel:
    df[col] = df.groupby('mes.1')[col].transform(lambda x: x.fillna(x.median()))

# 2. Excluir período COVID (marzo 2020 - junio 2021) -> quedan 247 registros
mask_covid = (df['fecha'] >= '2020-03-01') & (df['fecha'] <= '2021-06-01')
df_modelo  = df[~mask_covid].copy()

# 3. Split temporal: train hasta 2022 (212 meses) / test desde 2023 (35 meses)
df_train = df_modelo[df_modelo['anio'] <= 2022]
df_test  = df_modelo[df_modelo['anio'] >= 2023]
```

## A.3 · Selección de variables (Correlación + VIF iterativo)

La selección ocurre en dos pasos por cada target. Primero se descartan las features con correlación absoluta con el target inferior a 0,10. Después se ataca la **multicolinealidad**: variables que se explican entre sí (como las dos tasas de ocupación, que correlacionan 0,97) inflan los coeficientes y los vuelven poco fiables. El VIF iterativo elimina de a una la variable más redundante hasta que todas quedan por debajo del umbral.

<div align="center">
  <img src="./matriz_correlacion.png" alt="Matriz de correlación" width="78%"/>
  <br/>
  <em>Correlación entre features y targets. La fuerte correlación entre <code>ush_toh %</code> y <code>ush_top %</code> (0,97) es la que motiva la eliminación por VIF.</em>
</div>

```python
def vif_iterativo(df_t, feats, umbral):
    """Elimina de a UNA la variable con mayor VIF y recalcula,
    hasta que todas queden por debajo del umbral. Se calcula sobre
    variables estandarizadas para que la escala no infle el resultado."""
    feats = list(feats)
    while len(feats) > 1:
        X = StandardScaler().fit_transform(df_t[feats].values.astype(float))
        vifs = [variance_inflation_factor(X, i) for i in range(len(feats))]
        if max(vifs) > umbral:          # si hay multicolinealidad...
            feats.pop(int(np.argmax(vifs)))   # ...elimina la peor y reintenta
        else:
            break
    return feats
```

## A.4 · Modelo y entrenamiento

Se entrena una **Regresión Lineal Múltiple** por cada target (mínimos cuadrados, sin hiperparámetros). El punto clave es el **escalado**: el `StandardScaler` se ajusta **solo con los datos de entrenamiento** y luego se aplica al test. Así se evita la *fuga de información* (que el modelo "vea" indirectamente datos del test durante el entrenamiento).

```python
for col_target, label in TARGETS.items():
    FEATURES = features_seleccionadas[col_target]   # features propias del target
    df_t = df_modelo.dropna(subset=[col_target] + FEATURES)

    X_train = df_t[df_t['anio'] <= 2022][FEATURES].values
    X_test  = df_t[df_t['anio'] >= 2023][FEATURES].values
    y_train = df_t[df_t['anio'] <= 2022][col_target].values
    y_test  = df_t[df_t['anio'] >= 2023][col_target].values

    scaler = StandardScaler()
    X_train_scaled = scaler.fit_transform(X_train)   # fit SOLO en train
    X_test_scaled  = scaler.transform(X_test)        # test solo se transforma

    modelo = LinearRegression().fit(X_train_scaled, y_train)
    y_pred = modelo.predict(X_test_scaled)

    # Métricas de evaluación
    mae  = mean_absolute_error(y_test, y_pred)
    rmse = np.sqrt(mean_squared_error(y_test, y_pred))
    r2   = r2_score(y_test, y_pred)
    r2cv = cross_val_score(modelo, X_train_scaled, y_train, cv=5, scoring='r2').mean()
```

## A.5 · Resultados (conjunto de prueba 2023–2025)

| Variable objetivo | R² | R² CV | RMSE | MAE |
|---|:---:|:---:|:---:|:---:|
| **Viajeros totales** | 0,828 | 0,874 | 3.480 | 2.669 |
| **Pernoctaciones** | 0,807 | 0,903 | 8.114 | 5.337 |
| **Parque Nacional** | 0,452 | 0,241 | 12.308 | 10.239 |

*R²: proporción de varianza explicada · R² CV: validación cruzada (5 folds) · RMSE/MAE: error en unidades del indicador.*

## A.6 · Proyección 2026

Para proyectar el futuro se construye, por cada mes, una fila de predictores con la **mediana histórica de ese mes** (variables hoteleras y climáticas), fijando solo el año y el mes objetivo. Es un escenario base que asume condiciones normales.

```python
def features_futuros(anio, mes, features):
    """Construye los predictores de un mes futuro con la mediana histórica
    de ese mes; año y mes se fijan al período proyectado."""
    fila = df_modelo[df_modelo['mes.1'] == mes][features].median()
    if 'anio'  in fila.index: fila['anio']  = anio
    if 'mes.1' in fila.index: fila['mes.1'] = mes
    return fila.values.reshape(1, -1)

# Cada target se proyecta con su propio modelo y escalador
X_fut = features_futuros(anio, mes, res['features'])
pred  = res['modelo'].predict(res['scaler'].transform(X_fut))[0]
pred  = max(0, round(pred))   # se acota a un mínimo de cero
```

## A.7 · Reproducibilidad

- **Notebook principal:** `01_prediccion_demanda_turistica_v2.ipynb`
- **Descarga de clima:** `00_descarga_clima_openmeteo.ipynb`
- **Dataset integrado:** `data/processed/dataset_turismo_clima.xlsx`
- **Gráficos completos:** carpeta `reports/` (diagnóstico, residuos, importancia de variables, etc.)
- **Repositorio:** https://github.com/Gasparlorenzo/parcial

---

<div align="center">
<sub>

**Informe de Proyección de Demanda Turística · Ushuaia 2026** · Ref. DT-USH-2026-01 · v1.0
Elaborado por Darío Martínez · Julio 2026 · Fuentes: IPIEC · Open-Meteo (ERA5)
Las estimaciones son orientativas y suponen condiciones normales de mercado.

🏔️ Hecho en el fin del mundo · Ushuaia, Tierra del Fuego 🇦🇷

</sub>
</div>
