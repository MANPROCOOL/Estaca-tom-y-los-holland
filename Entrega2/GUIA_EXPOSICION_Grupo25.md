# Guía de exposición — Entrega 2 — Grupo 25

Presentación de 13 diapositivas. Reparto sugerido para unos 12 minutos, además de preguntas.

## José Flores: diapositivas 1–3 (3 minutos)

Presenta la pregunta sobre calificaciones por distrito. Explica que la Entrega 1 comparó cinco medias con ANOVA (F=11,3048; p<0,001), mientras que la V de Cramér=0,0200 corresponde a la tabla distrito × puntuación. En esta entrega elegimos dos parámetros: μM y μB, y derivamos Δ. La elección de Manhattan y Brooklyn responde al tamaño muestral, sin seleccionar los promedios extremos. La unidad es un anuncio calificado, con peso 1. Describe las 102.058 filas limpias, las 43.418 y 41.515 calificaciones válidas y los 140 y 116 faltantes.

## Sebastian Alcaide: diapositivas 4–8 (4 minutos)

Distingue parámetro, estimador y estimación. La media es insesgada cuando las observaciones tienen esperanza μg; la independencia por sí sola no garantiza representatividad. Explica consistencia y eficiencia entre estimadores lineales bajo las condiciones del modelo. El bootstrap propio remuestrea índices con reemplazo, conserva los tamaños y repite B=20.000 veces. Presenta a Efron (1979) y su relevancia para estadísticas con distribución difícil de derivar. Compara la estimación, los EE y los IC. Las dos curvas de medias y el histograma de Δ describen réplicas, no puntuaciones individuales. El sesgo bootstrap teórico de las medias es cero y el desplazamiento numérico se debe a B finito.

## Pedro Ortiz: diapositivas 9–10 (2 minutos)

Explica el modelo categórico 1–5, las probabilidades empíricas y los conteos multinomiales. Se mantienen las probabilidades fijas. Cada escenario tiene un modelo ajustado y otro nulo, con R=20.000 realizaciones y Welch bilateral al 5%. Con 200 anuncios por distrito, la potencia es 5,34%; con los tamaños originales es aproximadamente 53%. La potencia usa el efecto ajustado con estos datos, por lo que no es validación externa. El modelo nulo común controla falsos rechazos bajo igualdad de distribuciones. Explica el papel de n frente a R.

## Miguel Primera: diapositivas 11–13 (3 minutos)

Define el evento de precisión: error de la diferencia estimada respecto al valor del modelo de hasta 0,05 puntos. Ocurrió 20.000 de 20.000 veces con los tamaños originales; su límite inferior Wilson es 99,98%. El resultado no establece certeza poblacional. Distingue error de simulación y variabilidad por muestreo. Cierra con la diferencia de 0,0181 puntos y sus IC, las cotas [0,0059; 0,0299] al incorporar faltantes, los supuestos de independencia y escala ordinal, y el alcance condicionado a la fuente. Declara el apoyo de Claude y ChatGPT/Codex.

## Cifras de la ejecución comprobada

- Potencia original: 52,83%, IC Monte Carlo Wilson [52,14%; 53,52%]. En exposición: aproximadamente 53%.
- Diferencia: 0,018060 puntos; IC clásico [0,000665; 0,035455]; IC bootstrap [0,000550; 0,035416].
- EE clásico: 0,008875; EE bootstrap: 0,008844; razón: 0,996.
- Eventual error ≤0,05: 20.000 éxitos entre 20.000 simulaciones con tamaños originales. Límite Wilson inferior: 99,98%.
- Cotas descriptivas con faltantes: [0,005891; 0,029893].

## Preguntas para preparar la exposición

**¿Por qué Manhattan y Brooklyn?** Son los distritos con más anuncios, según el EDA. La selección no usa el mayor y el menor promedio. La diferencia pequeña permite estudiar cómo tamaño, precisión y detección se relacionan.

**¿Igualdad de medias implica independencia?** No. ANOVA y Welch contrastan medias. El chi-cuadrado del EDA contrasta independencia entre distrito y categoría de puntuación. La V de Cramér cuantifica esa asociación categórica.

**¿Qué significa un IC del 95%?** La cobertura del procedimiento en muestreos repetidos bajo sus supuestos. No es una probabilidad posterior del parámetro fijo.

**¿Qué significa potencia de aproximadamente 53%?** Si el modelo ajustado fuera la población y repitiéramos muestras de esos tamaños, Welch rechazaría la igualdad de medias aproximadamente en el 53% de los casos. El efecto fijado proviene de esta misma muestra.

**¿Por qué hay precisión alta y potencia moderada?** El error tolerado de 0,05 puntos es mayor que la diferencia del modelo, 0,0181. Estimar cerca del valor verdadero y rechazar Δ=0 son eventos distintos.

**¿Un 100% de éxitos prueba certeza?** No. Es una proporción de 20.000 simulaciones. Wilson conserva un límite inferior menor que 100%, y el modelo también tiene supuestos e incertidumbre no incorporada.

**¿Son intervalos de confianza las cotas de faltantes?** No. Son extremos descriptivos al asignar 1 o 5 a calificaciones ausentes de anuncios con distrito conocido. Amplían el conjunto de anuncios y no corrigen selección ni anuncios no registrados.

**¿Por qué cambia alguna cifra al ejecutar en otro equipo?** Las secuencias de Generator no se garantizan entre todas las versiones y plataformas de NumPy. El paquete incluye las versiones de esta ejecución. Los resultados de simulación se interpretan junto con su error Monte Carlo.

**¿La diferencia es relevante?** Es pequeña en la escala codificada 1–5. Los umbrales 0,05, 0,10 y 0,20 son exploratorios. No demuestran equivalencia formal ni relevancia causal.

**¿B y R son lo mismo?** B cuenta remuestras bootstrap; R cuenta realizaciones del modelo Monte Carlo por escenario y condición. Ambos controlan error numérico, mientras que n controla la información de cada muestra.

**¿Se asume normalidad en las notas?** No. Las puntuaciones son discretas 1–5. Los intervalos t de las medias se usan como aproximaciones de muestra grande, con las condiciones de muestreo indicadas.

**¿Son exactamente insesgados los estimadores?** Bajo el modelo con E(Ygi)=μg, sí. Esa propiedad no elimina sesgo de selección ni garantiza que los anuncios representen todo NYC.

## Ensayo del equipo

Comprobar el reparto y los tiempos, ensayar transiciones y revisar las notas de las diapositivas. Cada integrante debe poder explicar el modelo, el remuestreo y las limitaciones. La ejecución técnica comprobada no acredita por sí sola la revisión personal del grupo.
