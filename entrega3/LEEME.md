# Entregable 3 - Grupo 25

José Flores, Sebastian Alcaide, Pedro Ortiz y Miguel Primera. INF280, UTFSM.

## Contenido del ZIP

- `Entrega3_Grupo25.ipynb`: análisis ejecutado con resultados y gráficos.
- `Presentacion_Entrega3_Grupo25.pdf`: presentación de 19 diapositivas.
- `LEEME.md`: instrucciones de ejecución y alcance.

## Ejecución

El notebook descarga automáticamente `Airbnb_Open_Data.csv` desde Kaggle mediante `kagglehub`, sin depender de un CSV incluido en el ZIP. Se usa la misma fuente de E2, fijando la versión 1 para reproducir los datos anteriores. La primera ejecución necesita conexión a internet. Kagglehub puede reutilizar su caché en ejecuciones posteriores.

En Python local:

```bash
python -m pip install -r requirements.txt
python -m jupyter lab
```

Abrir el notebook y ejecutar todas las celdas en orden. En Colab basta subir el notebook; no hace falta subir el CSV ni crear una carpeta `data`. Si faltan dependencias, ejecutar `%pip install -q kagglehub statsmodels` antes de las importaciones.

El esquema sigue E2: portada, declaración de IA, importaciones y funciones de formato, descarga, limpieza, pares completos y análisis. Se conservan los nombres de variables, las funciones de presentación de tablas y la función bootstrap de la entrega anterior. Los apartados nuevos responden a la pauta de E3.

Las semillas son 2026 para bootstrap, 2028 para la partición de bondad de ajuste, 2029 para su calibración y 2030 para la partición predictiva. El notebook regenera todas las réplicas, sin requerir un archivo de simulaciones previamente guardado.

## Alcance y entrega

Se desarrollan los cuatro apartados obligatorios: intervalos de confianza, bondad de ajuste, dos contrastes y regresión. La factibilidad de la regresión propuesta debe comprobarse con el tutor, como indica la pauta. El bonus opcional de ML queda fuera porque requiere aprobación del tutor. La guía de defensa explica la validación interna usada para el modelo categórico saturado de E2.

La entrega corresponde al **domingo 8 de noviembre de 2026 a las 23:55**, hora de Chile. Solo el encargado sube `entrega3-grupo25.zip` a AULA. No se ha enviado el trabajo a AULA, Discord ni al tutor.

La base son únicamente el notebook y el PDF oficiales de E2. ChatGPT/Codex apoyó la elaboración. El grupo debe comprender y revisar el trabajo antes de entregarlo.
