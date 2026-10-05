# Entrega 2 — Grupo 17 — Airbnb NYC

INF280, Estadística Computacional. José Flores, Sebastian Alcaide, Pedro Ortiz y Miguel Primera.

La entrega estima las medias de calificación de Manhattan y Brooklyn y su diferencia. Implementa bootstrap propio con 20.000 réplicas y Monte Carlo con 20.000 realizaciones por escenario y condición.

## Archivos

| Archivo o carpeta | Contenido |
| --- | --- |
| `Entrega2_Grupo17_Airbnb.ipynb` | Notebook independiente, con código, explicaciones y resultados ejecutados. |
| `presentacion/Entrega2_Grupo17_Airbnb_revisada.pptx` | Presentación revisada de 17 diapositivas; tablas y gráficos editables, con notas del expositor. |
| `presentacion/Entrega2_Grupo17_Airbnb_revisada.pdf` | Versión revisada de las diapositivas para visualizar o proyectar. |
| `GUIA_EXPOSICION.md` | Reparto sugerido y preguntas para preparar la exposición. |
| `data/Airbnb_Open_Data.csv` | Datos originales, versión 1 de la fuente de Kaggle. |
| `resultados/` | Figuras, tablas CSV, resumen JSON y réplicas comprimidas del notebook. |
| `requirements.txt` | Versiones de las bibliotecas utilizadas en la ejecución comprobada. |

## Ejecutar en VS Code

1. Extraer el ZIP completo, conservando la carpeta `entrega2` y sus subcarpetas.
2. Abrir esa carpeta en VS Code y abrir el notebook.
3. Seleccionar el entorno de Python con NumPy, pandas, SciPy, Matplotlib e IPython/ipykernel.
4. Reiniciar el kernel y ejecutar todas las celdas, en orden. No es necesario ejecutar primero la Entrega 1.

Las versiones fijadas de las bibliotecas requieren Python 3.12 o posterior; el entorno comprobado utiliza Python 3.14.7. Para instalar las dependencias en un entorno propio, ejecutar desde la carpeta `entrega2`:

```powershell
python -m pip install -r requirements.txt
```

El CSV incluido permite ejecutar el análisis sin descargar datos y se verifica mediante SHA-256. El notebook también busca la caché local de Kaggle y, como alternativa opcional, permite descargar la versión 1 con `kagglehub`. Las semillas, tamaños y número de repeticiones están definidos en el notebook.

Si se incorpora al proyecto existente, copiar la carpeta `entrega2` completa dentro de `Estaca-tom-y-los-holland`. La copia del notebook que ya está en la raíz puede abrirse por separado; mantener la estructura completa facilita reproducir la entrega en otro computador.

## Lectura de los resultados

La diferencia estimada es aproximadamente 0,0181 puntos en una escala de 1 a 5. Los intervalos clásico y bootstrap son similares. Las simulaciones muestran cómo el tamaño muestral modifica la precisión y la detección de una diferencia pequeña.

La inferencia está condicionada a los anuncios calificados de esta fuente y a los supuestos del modelo. No establece causalidad ni representatividad probabilística del mercado de Nueva York. Los umbrales de precisión utilizados son referencias exploratorias.

La sección 8.1 añade un diagnóstico descriptivo de calificaciones faltantes: si todas estuvieran entre 1 y 5, la diferencia entre todos los anuncios registrados con distrito conocido quedaría entre 0,0059 y 0,0299 puntos. Estas cotas no son intervalos de confianza. Las comprobaciones finales del notebook contrastan Welch y Wilson con funciones independientes de SciPy.

## Preparación de la entrega

El paquete final se llama `entrega2-grupo17.zip`. La pauta indica entrega del notebook y presentación. Las notas de las diapositivas complementan la explicación oral; el PDF reproduce su contenido visible.

Antes de enviar, cada integrante debe ejecutar o revisar el notebook, comprobar su nombre y comprender los supuestos y resultados. El notebook y la presentación incluyen una declaración de apoyo de ChatGPT/Codex. No se afirma que la revisión individual del grupo ya haya ocurrido.
