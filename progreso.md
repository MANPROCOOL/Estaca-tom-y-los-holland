# Progreso — Laboratorio 1: Análisis Exploratorio de Datos (INF280)

**Curso:** Estadística Computacional (INF280), USM — 2026-1  
**Tutor:** Cristobal Duarte  
**Entrega:** domingo 13 de septiembre, 23:55 hrs (AULA)  

---

## Dataset

**Airbnb Open Data (NYC)** — [kaggle.com/datasets/arianazmoudeh/airbnbopendata](https://www.kaggle.com/datasets/arianazmoudeh/airbnbopendata)

> **Nota:** El dataset original propuesto (*Star Categorization - Giants and Dwarfs*) fue descartado por no tener suficientes variables categóricas y estar orientado a Machine Learning. Este dataset de Airbnb cuenta con la aprobación del tutor.

* **Volumen original:** 102.599 filas, 26 columnas.
* **Volumen limpio:** 102.058 filas, 22 columnas (mantiene NaNs sin recurrir a `dropna` masivo ni imputaciones artificiales).

---

## Consolidación del Trabajo del Equipo (Decisión Metodológica)

Debido a trabajo en paralelo y descoordinado entre los integrantes del grupo, se habían generado 4 notebooks con enfoques y resultados divergentes (`Codigo_Entregable_1_estaca.ipynb`, `Texto_Entregable_1_informe.ipynb`, `Informe_.ipynb` e `Informe2_.ipynb`). Se procedió a una **unificación y consolidación total en dos notebooks definitivos**:

1. **`Codigo_Entregable_1_estaca.ipynb` (Notebook de Código):**
   * Se adoptó la limpieza base completa sobre el dataset íntegro (102.058 filas tras deduplicación), descartando la versión de filtrado agresivo con `dropna` e imputación con mediana de `Informe_.ipynb` e `Informe2_.ipynb`.
   * Se integró la corrección de valores imposibles (`availability_365` y `minimum_nights`) directamente dentro del bloque de limpieza real con salidas verificadas.
   * Se eliminaron celdas duplicadas y celdas sin ejecutar al final del notebook.
   * Se estructuraron los análisis estadísticos de la variable secundaria (`room_type` vs `neighbourhood_group`) y de la pregunta principal (`review_rate_number` vs `neighbourhood_group`: ANOVA + Chi² + V de Cramér).

2. **`Texto_Entregable_1_informe.ipynb` (Notebook de Informe de Texto):**
   * Estructuración completa: Portada, Declaración de IA dual, Motivación, Diccionario de datos de 26 variables, Justificación de limpieza, Estadística descriptiva y outliers (IQR), Análisis visual "con lupa", Pregunta de investigación e hipótesis resueltas formalmente, y Limitaciones.
   * Se reemplazó el placeholder inconcluso `**termianr el analisis estadistico` por el análisis consolidado riguroso.
   * Se eliminaron los notebooks redundantes `Informe_.ipynb` e `Informe2_.ipynb` del repositorio tras integrar sus aportes valiosos (como la V de Cramér y la detección IQR).

---

## Qué se ha hecho

### 1. Carga de datos
- Descarga automatizada vía `kagglehub.dataset_download("arianazmoudeh/airbnbopendata")`.
- Semilla fijada (`RANDOM_STATE = 42`) para garantizar reproducibilidad total.

### 2. Limpieza de datos (Integrada en Bloque Principal)
- **Duplicados exactos:** Eliminación de 541 filas duplicadas (102.599 $\to$ 102.058 filas).
- **Corrección tipográfica:** Unificación de nombres en `neighbourhood_group` ("manhatan" $\to$ Manhattan, "brookln" $\to$ Brooklyn).
- **Formato monetario:** Extracción de símbolos (`$`, `,`) en `price` y `service_fee`, convirtiendo a `float` y preservando `NaN`.
- **Nombres de columnas:** Normalizados a estándar `snake_case`.
- **Columnas descartadas:** Eliminación de `license` (~100% nula), `house_rules` (>51% nula, texto libre), `country` y `country_code` (invariantes, 100% US).
- **Valores físicamente imposibles convertidos a `NaN`:**
  - `availability_365`: 431 registros negativos y 2.754 superiores a 365 días (total: 3.185 registros inválidos corregidos a `NaN`).
  - `minimum_nights`: 13 registros con valores negativos corregidos a `NaN`.

### 3. Detección cuantitativa de outliers (Criterio IQR)
- `price`, `service_fee`, `availability_365`: **0 outliers** (distribuciones acotadas naturalmente o tras depuración física).
- `minimum_nights`: **18.240 outliers** (cola pesada asimétrica con estadías de hasta 5.645 noches).
- `number_of_reviews`: **11.120 outliers** (distribución de ley de potencias típica de interacción en plataformas).

### 4. Visualizaciones y Hallazgo Clave ("Observar con Lupa")
- Boxplots de `price` por distrito y tipo de habitación revelan medianas casi idénticas (sin gradiente de mercado centro-periferia).
- Promedios de calificaciones por distrito fluctúan en un rango estrechísimo (entre 3.26 y 3.40 en escala 1-5).
- T-test de `review_rate_number` por `instant_bookable`: $t = 1.0123, p = 0.3114$ (no significativo).
- ANOVA de `review_rate_number` por `cancellation_policy`: $F = 0.0400, p = 0.9608$ (no significativo).
- **Conclusión de calidad:** `price` y `review_rate_number` presentan indicios de haber sido modificados sintéticamente o capturados con ruido en el dataset original. Se documenta formalmente como limitación del dataset.

### 5. Pregunta de Investigación e Hipótesis Estadísticas ✅
- **Pregunta Principal:** ¿Existe asociación entre el distrito (`neighbourhood_group`) y la calificación otorgada por los huéspedes (`review_rate_number`) en Airbnb NYC?
  - **$H_0$:** La calificación promedio es independiente del distrito ($\\mu_{\\text{Bronx}} = \\mu_{\\text{Brooklyn}} = \\mu_{\\text{Manhattan}} = \\mu_{\\text{Queens}} = \\mu_{\\text{Staten Island}}$).
  - **$H_1$:** La calificación promedio difiere significativamente en al menos un distrito.
  - **Test Principal (ANOVA de una vía):** $F = 11.3048, p = 3.596 \times 10^{-9} \approx 0.0000 \implies$ Se rechaza $H_0$ a nivel $\\alpha = 0.05$.
  - **Medida Complementaria de Tamaño de Efecto (Chi-cuadrado y V de Cramér):**
    - $\\chi^2 = 162.53, df = 16, p \approx 0.0000$.
    - **V de Cramér:** $V = 0.0200$ sobre el dataset completo ($N = 101.712$), concordante con el $V = 0.0523$ explorado en submuestra.
    - **Conclusión con lupa:** El rechazo de $H_0$ es un artefacto de la potencia del gran tamaño muestral ($N > 100.000$). La magnitud del efecto ($V = 0.0200$) demuestra que la asociación es extremadamente débil / prácticamente nula en el mundo real.
- **Variable Secundaria de Contexto:** `room_type` vs `neighbourhood_group`:
  - Test Chi-cuadrado de independencia: $\\chi^2 = 2708.85, p < 10^{-16}, df = 12 \implies$ Asociación estructural contundente (Manhattan monopoliza habitaciones de hotel y lidera departamentos enteros, mientras Brooklyn y Queens concentran habitaciones privadas).

---

## Estado de Avance y Tareas

- [x] Unificación y consolidación de los 4 notebooks paralelos en 2 definitivos (`Codigo_Entregable_1_estaca.ipynb` y `Texto_Entregable_1_informe.ipynb`).
- [x] Limpieza de datos integrada en bloque continuo con outputs ejecutados (valores imposibles de disponibilidad y noches mínimas).
- [x] Diccionario de datos formal con las 26 variables en tabla HTML.
- [x] Detección cuantitativa de outliers por método IQR documentada.
- [x] Redacción de reflexiones "Observar con lupa" (comportamiento de precios y calificaciones).
- [x] Resolución formal de la hipótesis estadística (reemplazo del placeholder por ANOVA + V de Cramér).
- [x] Justificación e interpretación de la variable secundaria de contexto (`room_type`).
- [x] Declaración explícita y transparente del uso de herramientas de IA (Claude y Gemini).
- [x] Eliminación de archivos redundantes (`Informe_.ipynb` e `Informe2_.ipynb`).
- [x] Verificación de ejecución limpia y secuencial del notebook de código.
- [ ] Empaquetar como `entrega1_grupoX.zip` (PDF exportado desde el informe de texto + `.ipynb` de código) y subir a AULA antes del domingo 13/09 23:55.

---

## Herramientas de Inteligencia Artificial Utilizadas

Se utilizaron de manera complementaria y transparente:
* **Claude (Anthropic):** Desarrollo y depuración del código de limpieza en Pandas, scripts de visualizaciones (Matplotlib/Seaborn), ejecución y cálculo de pruebas de hipótesis (ANOVA, Chi-cuadrado) y redacción de secciones de motivación, limitaciones y conclusiones.
* **Gemini (Google):** Estructuración preliminar del informe en formato Markdown, asesoría en el diseño de la función de outliers (método IQR), formulación inicial de la tabla de contingencia y cálculo del tamaño del efecto mediante la V de Cramér.

Todo el código, cálculos e interpretaciones fueron revisados, validados y comprendidos en su totalidad por el equipo.
