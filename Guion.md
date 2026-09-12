# Guion de Presentación — Airbnb NYC (EDA)
**INF280 · 14 slides · 4 integrantes · presentación lineal (1 turno cada uno)**

Reparto sugerido: Slides 1–4 → **Integrante A** · Slides 5–8 → **Integrante B** · Slides 9–11 → **Integrante C** · Slides 12–14 → **Integrante D** (además cierra y coordina preguntas).

Tiempo estimado total: 9–11 minutos (ajusten el ritmo según lo que pida el tutor).

---

## TURNO 1 — Integrante A (slides 1 a 4) · ~2:30 min

**[Slide 1 — Título]**
> "Buenas tardes. Somos el grupo [nombre del grupo] y hoy les presentamos nuestro Análisis Exploratorio de Datos sobre Airbnb en Nueva York. La pregunta que guía este trabajo es si el barrio donde se ubica un alojamiento determina la calificación que reciben los anfitriones. Somos cuatro integrantes: [nombres], y nuestro tutor es Cristobal Duarte."

**[Slide 2 — Motivación]**
> "Elegimos este dataset por tres razones. Primero, el alquiler de corto plazo tiene un impacto urbano real: transforma la vivienda y el turismo en ciudades densas como Nueva York. Segundo, a diferencia de datasets de juguete como Iris o Titanic, este trae problemas de calidad genuinos —duplicados, errores de tipeo, formatos inconsistentes— que nos permitieron aplicar un proceso de limpieza real. Y tercero, mezcla variables categóricas y continuas: cinco distritos, cuatro tipos de alojamiento, precios, reseñas y políticas de cancelación."

**[Slide 3 — Dataset]**
> "El dataset viene de Kaggle y originalmente tenía 102 mil 599 filas y 26 columnas, repartidas en 5 distritos y 4 tipos de alojamiento. Después de nuestra limpieza —que vamos a detallar en un momento— quedamos con 102 mil 58 filas y 22 columnas, cumpliendo de sobra el mínimo de 200 observaciones que pide la pauta."

**[Slide 4 — Problemas de calidad]**
> "Antes de analizar nada, tuvimos que limpiar varios problemas reales. Encontramos 541 filas duplicadas exactas, que eliminamos. Había errores de tipeo como 'manhatan' en vez de Manhattan, que corregimos manualmente. Las columnas de precio y tarifa de servicio venían como texto, con el símbolo de dólar incluido, así que las convertimos a número. También encontramos valores físicamente imposibles: noches mínimas negativas, y disponibilidad anual fuera del rango de 0 a 365 días, casi 3 mil 200 filas. Y finalmente descartamos dos columnas casi vacías: license, con solo 2 valores no nulos de 102 mil, y house_rules, con más de la mitad nula."

*(Transición)* → "Le paso la palabra a [nombre B], que va a mostrarles cómo detectamos outliers y qué encontramos al visualizar los datos."

---

## TURNO 2 — Integrante B (slides 5 a 8) · ~2:45 min

**[Slide 5 — Outliers IQR]**
> "Para detectar valores atípicos usamos el criterio del rango intercuartílico, como pide la pauta. Variables como price, service_fee y availability_365 no mostraron outliers, porque son distribuciones acotadas. En cambio, minimum_nights tuvo 18 mil 240 outliers, con casos de hasta 5 mil 645 noches mínimas, y number_of_reviews tuvo 11 mil 120. Esto es esperable en variables de conteo y duración, no significa que sean errores."

**[Slide 6 — Distribución de variables principales]**
> "Nuestras variables principales son neighbourhood_group y review_rate_number. Como ven en el gráfico de la izquierda, Manhattan y Brooklyn concentran casi el 83% de todos los listados, mientras que Staten Island tiene menos del 1%. Y en el gráfico de la derecha, algo interesante: las calificaciones de 2 a 5 estrellas tienen conteos casi idénticos, alrededor de 23 mil cada una. Esto ya nos hizo sospechar que algo raro pasa con esta variable."

**[Slide 7 — Hallazgo: precio plano]**
> "Y acá viene uno de nuestros hallazgos más importantes al 'observar con lupa'. La mediana de precio en Manhattan es 628 dólares, y en el Bronx es 623 dólares: menos de 1% de diferencia. En un mercado real, un departamento completo en Manhattan debería costar bastante más que una habitación en un barrio periférico. Esta planicie nos hace sospechar que la variable price fue anonimizada o generada sintéticamente en el dataset original, y lo documentamos como limitación."

**[Slide 8 — room_type vs distrito]**
> "Como variable secundaria de contexto, cruzamos el tipo de alojamiento con el distrito. Acá sí encontramos una relación real y fuerte: el test chi-cuadrado dio 2708.85, con un p-valor menor a 10 elevado a menos 16, así que rechazamos la hipótesis nula de independencia. Por ejemplo, Manhattan concentra casi el 100% de las habitaciones de hotel, 100 de 115 en todo el dataset."

*(Transición)* → "Ahora [nombre C] les va a presentar nuestra pregunta de investigación principal y los resultados del test de hipótesis."

---

## TURNO 3 — Integrante C (slides 9 a 11) · ~2:30 min

**[Slide 9 — Pregunta e hipótesis]**
> "Nuestra pregunta de investigación es: ¿existe asociación entre el distrito donde se ubica un alojamiento y la calificación que le otorgan los huéspedes? Formulamos esto como una hipótesis nula, H0, que dice que la calificación promedio es igual en los cinco distritos; y una hipótesis alternativa, H1, que dice que difiere en al menos uno. Usamos un nivel de significancia de 0.05 y el test elegido fue ANOVA de una vía."

**[Slide 10 — Resultados ANOVA]**
> "El resultado del ANOVA nos dio un estadístico F de 11.30, con un p-valor prácticamente cero, 3.6 por 10 elevado a menos 9. Como el p-valor es menor que 0.05, rechazamos H0: sí hay una diferencia estadísticamente significativa entre distritos. Como ven en el gráfico, Staten Island destaca con la calificación media más alta, aunque hay que tener cuidado porque su muestra es chica, solo 943 listados."

**[Slide 11 — Cramér's V]**
> "Pero acá quisimos ir un paso más allá, porque con una muestra de más de 100 mil datos, hasta una diferencia mínima se vuelve estadísticamente significativa. Por eso calculamos también el tamaño del efecto con la V de Cramér, que nos dio solo 0.02, una asociación extremadamente débil. Y si lo llevamos a términos concretos: la diferencia entre el distrito mejor calificado y el peor calificado es de apenas 0.14 puntos en una escala de 1 a 5. Nuestra conclusión es que, aunque el resultado es significativo, el distrito no es un factor determinante en la práctica."

*(Transición)* → "Para cerrar, le paso la palabra a [nombre D], que va a hablarles de las limitaciones del dataset y nuestras conclusiones finales."

---

## TURNO 4 — Integrante D (slides 12 a 14) · ~2:00 min + preguntas

**[Slide 12 — Limitaciones]**
> "Es importante ser honestos sobre las limitaciones de este trabajo. Primero, hay una representatividad geográfica muy desigual: Manhattan y Brooklyn concentran el 83% de los datos. Segundo, como mencionamos, price y review_rate_number muestran patrones que sugieren generación sintética, no necesariamente el comportamiento real del mercado. Tercero, el dataset es una fotografía estática, no captura estacionalidad ni cambios regulatorios recientes en Nueva York. Y cuarto, encontramos errores de captura evidentes, como disponibilidades sobre 365 días, que muestran falta de validación al ingresar los datos."

**[Slide 13 — Conclusiones y uso de IA]**
> "En resumen: encontramos una asociación estadística real pero de magnitud despreciable entre distrito y calificación. En cambio, el tipo de alojamiento sí depende fuertemente del distrito. Y detectamos que dos variables clave del dataset probablemente no reflejan datos de mercado orgánicos. Como equipo, usamos Claude de Anthropic para la limpieza de datos, las visualizaciones y las pruebas estadísticas, y Gemini de Google para la estructuración del informe y el cálculo de la V de Cramér. Todos revisamos y entendemos cada línea de código y cada resultado, así que estamos preparados para responder preguntas sobre cualquier parte del análisis."

**[Slide 14 — Cierre]**
> "Muchas gracias por su atención. Quedamos atentos a sus preguntas."

---

## Notas de coordinación para el equipo

- **Practiquen las transiciones en voz alta** — la rúbrica de presentación evalúa "orden, coherencia y estructura", y los cambios de turno abruptos bajan puntaje. Usen las frases de transición sugeridas o adapten una propia, pero no salten de un integrante a otro sin decir nada.
- **Cada uno debe poder responder preguntas de CUALQUIER parte del análisis**, no solo de su turno — la rúbrica de "respuestas a preguntas del equipo de ayudantes" no distingue quién presentó qué.
- **Reemplacen los corchetes** `[nombre del grupo]`, `[nombres]`, `[nombre B]`, `[nombre C]`, `[nombre D]` por los datos reales antes de ensayar.
- Este guion es una base — ajústenlo a como hablan naturalmente. Leerlo palabra por palabra en la presentación real baja puntos en "expresión oral" (la pauta penaliza falta de naturalidad).
- Tiempo total estimado: ~10 minutos de exposición, dejando margen para preguntas del equipo de ayudantes.