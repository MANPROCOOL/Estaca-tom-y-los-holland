# Entrega 2 — Grupo 25 — Airbnb NYC

INF280, Estadística Computacional. José Flores, Sebastian Alcaide, Pedro Ortiz y Miguel Primera. Tutor: Cristobal Duarte.

La entrega estima las medias de calificación de Manhattan y Brooklyn y su diferencia. Implementa bootstrap propio con B=20.000 réplicas y Monte Carlo con R=20.000 realizaciones por escenario y condición.

## Contenido

| Archivo o carpeta | Contenido |
|---|---|
| `Entrega2_Grupo25_Airbnb.ipynb` | Notebook independiente, ejecutado, con 18 celdas de código. |
| `presentacion/Presentacion_Entrega2_Grupo25.pptx` | Presentación de 13 diapositivas con gráficos y tablas editables, y notas. |
| `presentacion/Presentacion_Entrega2_Grupo25.pdf` | Versión para visualizar o proyectar. |
| `Revision_y_presentacion_Grupo25.docx` | Revisión final y reparto de la exposición. |
| `GUIA_EXPOSICION_Grupo25.md` | Guion de 13 diapositivas, cifras y preguntas de preparación. |
| `data/Airbnb_Open_Data.csv` | CSV original, versión 1 de Kaggle. |
| `resultados/` | Figuras, tablas, resumen JSON y réplicas de esta ejecución. |
| `requirements.txt` | Versiones comprobadas de las bibliotecas. |

## Ejecutar

1. Extraer el ZIP completo, conservando `entrega2/` y sus subcarpetas.
2. Abrir `entrega2/` en VS Code o Jupyter y seleccionar un entorno de Python 3.12.
3. Instalar las dependencias desde esa carpeta: `python -m pip install -r requirements.txt`.
4. Reiniciar el kernel y ejecutar las celdas en orden. No hace falta ejecutar primero la Entrega 1.

El entorno comprobado usa Python 3.12.14, NumPy 2.3.5, pandas 2.2.3, SciPy 1.17.0 y Matplotlib 3.10.8. La ejecución incluye el CSV y no necesita descargar datos. En Colab, situar el CSV en `data/Airbnb_Open_Data.csv`. La descarga opcional mediante `kagglehub` se usa solo si falta el archivo.

SHA-256 del CSV: `ecb59a7598d2aaf7dc2ed00c724648a319d93a916a3d4767e2bed0dbe0f1a7f8`. El notebook detiene la ejecución si no coincide.

Las semillas y los tamaños están definidos al inicio. NumPy no garantiza secuencias idénticas entre todas sus versiones y plataformas. Si se cambia el entorno, las cifras de simulación pueden variar: deben interpretarse junto con su error Monte Carlo. La presentación y la guía de este paquete usan las cifras de la ejecución comprobada.

## Interpretación

La diferencia estimada es 0,0181 puntos en una escala codificada 1–5. Los IC clásico y bootstrap casi coinciden. La potencia bajo el modelo ajustado es aproximadamente 53% con los tamaños originales. La inferencia está condicionada a los anuncios calificados de esta fuente y a los supuestos de independencia y estabilidad. No identifica causalidad ni demuestra representatividad del mercado de NYC.

Las cotas de faltantes [0,0059; 0,0299] son límites descriptivos para el conjunto ampliado con distrito conocido. No son intervalos de confianza. Los umbrales de magnitud 0,05, 0,10 y 0,20 son exploratorios.

## Entrega

El paquete final se llama `entrega2-grupo25.zip`. Incluye notebook, presentación, CSV y dependencias. La revisión y el guion son material de apoyo. La declaración de IA distingue el análisis y la actualización de ChatGPT/Codex del aporte de Claude a la revisión y presentación inicial.

Para incorporar al proyecto local, copiar la carpeta `entrega2` completa. Revisar el notebook y ensayar la exposición antes de enviar a AULA.
