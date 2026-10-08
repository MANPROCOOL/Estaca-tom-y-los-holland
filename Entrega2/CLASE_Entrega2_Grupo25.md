# Clase breve: qué hicimos en la Entrega 2

**Grupo 25 · INF280 · Airbnb NYC**

La Entrega 1 exploró si las calificaciones cambiaban según el distrito. La Entrega 2 estudia un contraste específico: cuánto difieren las medias de Manhattan y Brooklyn, cuánta incertidumbre tiene esa diferencia y cómo afecta el tamaño muestral a su detección.

## 1. De los anuncios a los parámetros

Cada observación es un anuncio con una puntuación registrada entre 1 y 5. Limpiamos el mismo CSV de la Entrega 1 y utilizamos 43.418 anuncios calificados de Manhattan y 41.515 de Brooklyn. No analizamos las calificaciones individuales de cada huésped.

Los parámetros son las medias poblacionales del modelo, μM y μB. Su diferencia derivada es Δ = μM − μB. El estimador es la fórmula aplicada a una muestra; la estimación es el número que obtenemos al aplicarla a nuestros datos.

| Objeto | Ejemplo |
|---|---|
| Parámetro | μM: media del modelo poblacional de Manhattan |
| Estimador | La media muestral: suma de puntuaciones / cantidad de anuncios |
| Estimación | 3,2765, calculada con los anuncios observados de Manhattan |

Brooklyn da 3,2585, de modo que estimamos **Δ = 0,0181 puntos**. Una diferencia positiva favorece a Manhattan en este contraste. Es pequeña en la escala 1–5; no significa que el distrito cause mejores calificaciones.

La sección 3 explica insesgamiento, consistencia y eficiencia con sus condiciones. Insesgado significa que el promedio del estimador en muestreos repetidos coincide con el parámetro objetivo. Consistente significa que se aproxima a él al crecer la muestra. La eficiencia indicada compara estimadores lineales insesgados bajo independencia y varianza común dentro de cada grupo.

## 2. ¿Cuánta incertidumbre tiene la estimación?

La desviación estándar describe la dispersión de las notas individuales. El **error estándar** describe la variación de un estimador entre muestras. Para una media estimamos EE = s/√n; para la diferencia entre grupos independientes sumamos las varianzas de sus medias y tomamos la raíz.

Así obtenemos EE de la diferencia ≈0,008875 y un IC clásico del 95% ≈[0,000665; 0,035455]. El IC añade información sobre la precisión a la estimación puntual. Su cobertura es una propiedad del procedimiento en muestreos repetidos bajo los supuestos del modelo; no es una probabilidad posterior sobre un parámetro fijo.

## 3. Bootstrap: remuestrear para ver variar el estimador

Tratamos los datos observados como una distribución empírica. En cada distrito sorteamos anuncios **con reemplazo**, conservamos su tamaño original, calculamos las medias y las restamos. Repetimos B=20.000 veces.

Ejemplo: `[1,3,5]` puede generar `[5,5,1]`. La media cambia porque algunos registros se repiten y otros no aparecen. Sin reemplazo, tomar todos los datos solo cambiaría su orden y conservaría la media.

Nuestra función `bootstrap_medias` implementa esos pasos con índices aleatorios de NumPy. Cada fila de `boot` contiene dos medias y su diferencia. La desviación de las diferencias estima el EE bootstrap; sus percentiles 2,5 y 97,5 forman el IC percentil.

Obtuvimos EE≈0,008844 e IC≈[0,000550; 0,035416]. Casi coinciden con el enfoque clásico. Revisamos su estabilidad al acumular réplicas y contrastamos su dispersión con una fórmula exacta dentro de la distribución empírica. La sección 4 también explica el origen del método y su utilidad para estadísticas con distribuciones difíciles de derivar.

## 4. Monte Carlo: experimentar con muestras de un modelo

Fijamos las probabilidades observadas de las cinco puntuaciones por distrito. Una muestra de ese modelo puede representarse por cinco conteos multinomiales. Por ejemplo, `[2,1,0,1,1]` representa cinco notas cuya media es 2,6. Así evitamos guardar cada nota individual.

Simulamos muestras de 50, 200, 1.000 y 5.000 anuncios por distrito, y de los tamaños originales. Cada tamaño tiene dos condiciones:

- **Ajustado:** cada distrito conserva sus probabilidades; la diferencia verdadera dentro del modelo es 0,0181.
- **Nulo:** ambos tienen las mismas probabilidades; la diferencia del modelo es cero.

Por cada condición generamos R=20.000 realizaciones y aplicamos Welch bilateral al 5%. En el ajustado, la proporción de rechazos estima la **potencia**. En el nulo, estima los **falsos rechazos**. También contamos cuándo el error de la diferencia estimada es de hasta 0,05 puntos.

Con los tamaños originales, la potencia es **52,83%**, aproximadamente 53%, bajo el modelo ajustado. La precisión de hasta 0,05 ocurrió en 20.000/20.000 realizaciones; eso no demuestra certeza. Los intervalos Wilson cuantifican el error de estimar esas probabilidades mediante un número finito de simulaciones.

Bootstrap usa remuestras de los datos y Monte Carlo es un enfoque general basado en modelos. Aquí, con probabilidades empíricas y tamaños originales, ambos reproducen la misma distribución objetivo de las medias. El aporte adicional de Monte Carlo es variar los tamaños y estudiar un modelo nulo.

## 5. Relación con el enunciado

| Requisito trabajado | Dónde lo resolvemos |
|---|---|
| Elegir uno o dos parámetros vinculados a la Entrega 1 | Sección 2: μM y μB, con Δ como contraste derivado |
| Estimarlos y discutir sesgo, consistencia y eficiencia | Sección 3: medias, diferencia y propiedades condicionadas |
| Explicar origen, motivación y relevancia moderna del bootstrap | Sección 4: fundamento y aplicaciones |
| Implementar bootstrap propio y describir sus pasos | Celda de código 6: `bootstrap_medias` |
| Mostrar distribuciones y comparar con el enfoque clásico | Celdas 7–9 y sección 5 |
| Proponer una situación, modelo, distribuciones y supuestos Monte Carlo | Sección 6 y celdas 10–11 |
| Justificar realizaciones y estudiar estabilidad | Sección 6.4 y celda 12 |
| Interpretar resultados de la simulación | Sección 7 y celdas 13–15 |
| Comunicar conclusiones y respaldarlas con el notebook | Secciones 8–9 y presentación |

Los IC clásicos, las cotas de faltantes y las comprobaciones adicionales apoyan la explicación. Las cotas de faltantes son límites descriptivos del conjunto ampliado, no IC.

## 6. Tres preguntas que debes poder responder

**¿Qué cambia al aumentar n?** La información de cada muestra: las medias varían menos y un mismo efecto puede detectarse con mayor frecuencia.

**¿Qué cambia al aumentar B o R?** La precisión de la aproximación computacional. No aumenta la cantidad de anuncios reales observados.

**¿Por qué tenemos potencia moderada y precisión alta?** Porque detectar Δ distinto de cero y estimarlo con un error de hasta 0,05 son eventos diferentes. La tolerancia 0,05 supera el efecto fijado de 0,0181.

Para estudiar, recorre el notebook por sus 18 celdas numeradas. Identifica en cada una su entrada, la operación principal y la salida. Después practica explicar las funciones `bootstrap_medias` y `simulacion_mc` sin leer sus instrucciones línea por línea.
