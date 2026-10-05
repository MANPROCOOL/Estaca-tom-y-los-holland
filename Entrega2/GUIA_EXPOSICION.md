# Guía de exposición — Grupo 17

Reparto sugerido para una exposición de aproximadamente 10–12 minutos. Ajustar al tiempo indicado por el curso. Las notas del expositor del PPTX contienen explicaciones y referencias más completas.

| Integrante | Diapositivas | Idea central |
| --- | --- | --- |
| José Flores | 1–4 | Pregunta, datos, dos parámetros y propiedades de los estimadores. |
| Sebastian Alcaide | 5–9 | Estimación clásica, distribuciones del remuestreo propio y comparación de incertidumbre. |
| Pedro Ortiz | 10–13 | Estabilidad, modelo Monte Carlo, escenarios y probabilidad de detección. |
| Miguel Primera | 14–17 | Precisión, error Monte Carlo, conclusiones, límites y uso de IA. |

## Transiciones sugeridas

**Después de la diapositiva 4:** «Ya definimos qué queremos estimar y bajo qué supuestos. Ahora veremos cuánto difieren las medias y cuánta incertidumbre tiene esa diferencia».

**Después de la diapositiva 9:** «Los dos métodos dan errores estándar muy similares. Revisaremos la estabilidad del remuestreo y luego simularemos qué pasaría si cambiara el tamaño de la muestra».

**Después de la diapositiva 13:** «Una muestra grande ayuda a detectar diferencias pequeñas. También permite estimarlas con más precisión, que es la siguiente métrica».

## Preguntas para preparar

**¿Cuáles son los dos parámetros?** Las medias poblacionales de calificación de anuncios de Manhattan y Brooklyn, dentro del alcance definido. Su diferencia es un contraste derivado. El análisis de dos distritos no reemplaza la comparación de los cinco distritos de la Entrega 1.

**¿Por qué estos distritos?** Son los dos con mayor presencia en la muestra. La elección no usa el máximo y mínimo de las medias observadas.

**¿Cuál es la unidad de observación?** Un anuncio. Cada anuncio pesa uno. No observamos la satisfacción de cada huésped ni ponderamos por el número de reseñas.

**¿Qué diferencia hay entre parámetro y estimador?** El parámetro describe la población o modelo y es fijo; el estimador es una función de la muestra, que cambia entre muestras. Su valor calculado es la estimación puntual.

**¿Por qué el estimador es insesgado, consistente y eficiente?** Bajo observaciones independientes con distribución estable y media finita, la media muestral tiene esperanza igual a la media poblacional y converge a ella. Entre estimadores lineales insesgados de la media de observaciones independientes con igual varianza, los pesos iguales minimizan la varianza. Esa eficiencia no se afirma frente a todo estimador posible.

**¿Por qué remuestrear con reemplazo?** Cada observación representa masa de la distribución empírica. El reemplazo genera muestras nuevas del mismo tamaño con repeticiones y omisiones. Sin reemplazo, seleccionar todos los anuncios solo cambia su orden y deja intacta la media.

**¿El bootstrap está implementado por nosotros?** La función del notebook genera índices aleatorios, selecciona observaciones con reemplazo y calcula los estadísticos. NumPy aporta el generador aleatorio; no se utiliza una función de bootstrap de biblioteca.

**¿Un pequeño sesgo bootstrap demuestra sesgo del estimador?** Para la media, el sesgo condicional teórico del bootstrap es cero. La pequeña diferencia entre el promedio de réplicas y la estimación original procede del número finito de réplicas; no prueba sesgo de selección ni ausencia de él.

**¿Por qué 20.000 réplicas?** Se muestran prefijos con distintos números de réplicas y se contrasta el error estándar simulado con su fórmula condicional exacta. El límite inferior del intervalo está cerca de cero; evitamos interpretar cambios numéricos pequeños como una conclusión fuerte.

**¿Bootstrap y Monte Carlo son lo mismo?** Ambos emplean simulación aleatoria. El bootstrap aproxima la distribución del estimador remuestreando los datos. Monte Carlo evalúa probabilidades y precisión bajo modelos explícitos y distintos tamaños muestrales.

**¿Por qué una distribución multinomial?** Cada puntuación toma uno de cinco valores. Bajo sorteos independientes con probabilidades fijas, los conteos por puntuación tienen distribución multinomial. Es una forma exacta y eficiente de simular esos sorteos y recuperar sus medias y varianzas.

**¿Qué distingue los dos modelos Monte Carlo?** El ajustado conserva las frecuencias observadas por distrito. El nulo asigna a ambos la distribución conjunta, por lo que sus medias son iguales. El primero estima detección bajo una diferencia fijada; el segundo examina falsos rechazos.

**¿Aumentar B o R equivale a aumentar n?** No. B y R reducen el error numérico de la simulación. El tamaño n controla la variabilidad estadística de las muestras. Repetir más veces una simulación no agrega anuncios observados.

**¿Qué significa la potencia de aproximadamente 52,78%?** Bajo el modelo ajustado y los tamaños originales, esa es la fracción simulada de pruebas de Welch que rechazan la igualdad de medias. No es la probabilidad de que la hipótesis alternativa sea verdadera. Un resultado significativo observado no garantiza que toda muestra futura sea significativa.

**¿Esa potencia confirma externamente el hallazgo?** No. El efecto utilizado se estimó con la misma muestra: es un ejercicio condicionado al modelo ajustado. Su intervalo Monte Carlo, aproximadamente 52,08%–53,47%, cuantifica el error numérico de simulación y no la incertidumbre al estimar las probabilidades del modelo.

**¿La superposición de las curvas bootstrap de las medias significa igualdad?** No. Las curvas describen la variabilidad de cada estimador por separado. Para estudiar la diferencia utilizamos directamente sus réplicas y su intervalo.

**¿Qué muestran las cotas para calificaciones faltantes?** Al asignar valores extremos de 1 o 5 a los 140 faltantes de Manhattan y 116 de Brooklyn, la diferencia descriptiva de todos los anuncios con distrito conocido queda entre 0,0059 y 0,0299 puntos. Es un rango determinista; no es un IC y no corrige anuncios que nunca entraron al dataset.

**¿Qué significa el intervalo de confianza del 95%?** Describe la cobertura del procedimiento en muestreo repetido bajo sus supuestos. No asigna una probabilidad posterior del 95% al parámetro fijo después de observar el intervalo.

**¿La precisión simulada del 100% es una certeza?** El evento ocurrió en todas las 20.000 realizaciones del escenario original. El intervalo Wilson cuantifica el error Monte Carlo y tiene un límite inferior menor que uno. Además, el resultado es condicional al modelo.

**¿Los falsos rechazos son exactamente 5%?** No. Las tasas simuladas están próximas al nivel nominal, pero incluyen error Monte Carlo y la aproximación del contraste para puntuaciones discretas. No se afirma que todos los intervalos contengan el 5%.

**¿Una diferencia detectable es necesariamente relevante?** No. La diferencia estimada es pequeña en la escala 1–5. Los umbrales 0,05, 0,10 y 0,20 son referencias exploratorias y no constituyen estándares validados de importancia práctica ni una prueba formal de equivalencia.

**¿Qué límites deben mencionarse?** La escala es ordinal; trabajar con medias supone interpretar sus distancias numéricas. La inclusión de anuncios y la ausencia de calificaciones pueden afectar el alcance. La independencia es un supuesto y el distrito no se asignó aleatoriamente. No se infiere causalidad ni representatividad de todo NYC.

**¿Igualdad de medias implica independencia?** No. Dos distribuciones pueden tener la misma media y diferir en otras propiedades. El contraste de medias responde una pregunta más específica que independencia completa.

**¿Cómo se utilizó IA?** ChatGPT/Codex apoyó el análisis, programación, comprobaciones y redacción inicial. Cada integrante debe revisar y comprender el trabajo antes de presentarlo y mantener la declaración incluida en los archivos.
