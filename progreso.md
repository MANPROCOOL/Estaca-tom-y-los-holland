# Progreso — Laboratorio 1: Análisis Exploratorio de Datos (INF280)

**Curso:** Estadística Computacional (INF280), USM — 2026-1
**Tutor:** Cristobal Duarte
**Entrega:** domingo 13 de septiembre, 23:55 hrs (AULA)

## Dataset

**Airbnb Open Data (NYC)** — [kaggle.com/datasets/arianazmoudeh/airbnbopendata](https://www.kaggle.com/datasets/arianazmoudeh/airbnbopendata)

> Nota: el dataset original propuesto (Star Categorization - Giants and Dwarfs) fue **rechazado** por el tutor por no tener suficientes variables categóricas y estar orientado a Machine Learning en vez de EDA. Este dataset de Airbnb ya fue **aprobado**.

102.599 filas, 26 columnas originales. Contiene mezcla real de variables categóricas (`room_type`, `neighbourhood_group`, `cancellation_policy`, etc.) y continuas (`price`, `minimum_nights`, `availability_365`, etc.), con problemas de calidad genuinos.

## Qué se ha hecho hasta ahora

### 1. Carga de datos
- Descarga vía `kagglehub.dataset_download("arianazmoudeh/airbnbopendata")`.
- Semilla fija (`RANDOM_STATE = 42`) para reproducibilidad.

### 2. Limpieza de datos
- **Duplicados:** se eliminaron 541 filas duplicadas exactas (mismo `id`).
- **Typos en `neighbourhood_group`:** corregidos "manhatan" → Manhattan, "brookln" → Brooklyn.
- **`price` y `service_fee`:** venían como texto (`"$966 "`) → limpiados y convertidos a `float`.
- **Nombres de columnas:** normalizados a snake_case (`neighbourhood group` → `neighbourhood_group`, etc.).
- **Valores imposibles corregidos a NaN:**
  - `minimum_nights` negativo (13 filas).
  - `availability_365` fuera del rango [0, 365] (431 negativos + 2.754 sobre 365).
- **Columnas eliminadas** por ser casi vacías o no aportar variación:
  - `license` (102.597 nulos de 102.599).
  - `house_rules` (~51% nulos, texto libre).
  - `country` y `country_code` (prácticamente constantes: 100% "United States"/"US").

### 3. Detección de outliers (criterio IQR)
- `price`, `service_fee`, `availability_365`: **0 outliers** (distribuciones acotadas).
- `minimum_nights`: 18.240 outliers (cola larga, valores hasta 5.645 noches).
- `number_of_reviews`: 11.120 outliers (distribución muy asimétrica).

### 4. Visualizaciones hechas
- Univariada + boxplot de `price`.
- Univariada (log) + boxplot de `minimum_nights`.
- Bivariada: `price` según `neighbourhood_group` y según `room_type`.
- Scatter: `number_of_reviews` vs `price`.
- Stacked bar: proporción de `room_type` por `neighbourhood_group`.

### 5. Hallazgo clave — `price` y `review_rate_number` parecen ruido/simulados
- Los boxplots de `price` por barrio y por tipo de alojamiento son casi idénticos entre grupos (no hay diferencia real).
- ANOVA de `review_rate_number` por `cancellation_policy`: F=0.0400, **p=0.9608** (no significativo).
- T-test de `review_rate_number` por `instant_bookable`: t=1.0123, **p=0.3114** (no significativo).
- **Conclusión:** estas dos variables probablemente no reflejan comportamiento real de mercado. Se documentará como **limitación del dataset**, y no se usarán como variables principales de la hipótesis.

### 6. Pregunta de investigación elegida ✅
- **Variables principales:** `room_type` y `neighbourhood_group` (ambas categóricas).
- **Pregunta:** ¿Existe asociación entre el tipo de alojamiento (`room_type`) y el barrio (`neighbourhood_group`) donde se ubica?
- **H₀:** son independientes. **H₁:** están asociados.
- **Test:** Chi-cuadrado de independencia → **χ² = 2708.85, p ≈ 0** → se rechaza H₀. Hay asociación real y fuerte (ej. los "Hotel room" están casi exclusivamente en Manhattan).
- **Variables secundarias propuestas:** `availability_365` (disponibilidad real) y `price`/`minimum_nights` (como control, aclarando la limitación de `price`).

## Qué falta

- [ ] Diccionario de datos formal en el informe (ya generado en el notebook, falta pegarlo en el PDF).
- [ ] Visualizaciones univariadas de `room_type` y `neighbourhood_group` (conteos de barras).
- [ ] Redactar el párrafo de "Observar con lupa" (reflexión sobre price/review_rate_number vs room_type/neighbourhood_group).
- [ ] Redactar párrafo de limitaciones del dataset.
- [ ] Justificar por escrito la elección de variables secundarias.
- [ ] Armar el informe/PDF de presentación, declarando el uso de IA (Claude) como apoyo en código y redacción.
- [ ] Verificar que el notebook corra de principio a fin sin errores (Run all).
- [ ] Empaquetar como `entrega1_grupoX.zip` (PDF + .ipynb) y subir a AULA antes del domingo 13/09 23:55.

## Herramientas de IA utilizadas

Se usó **Claude** (Anthropic) como apoyo para: escribir y depurar código de limpieza de datos, generar visualizaciones con matplotlib/seaborn, correr pruebas estadísticas (ANOVA, t-test, chi-cuadrado) e interpretar resultados. Todo el código fue revisado y comprendido por el equipo.

---
*Este archivo se actualiza a medida que avanza el trabajo — revísenlo antes de tocar el notebook para no duplicar trabajo.*