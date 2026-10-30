# Del silbido al piano: examen práctico de Algoritmos Genéticos

IA, Universidad Católica Boliviana. Un silbido se convierte en una melodía tocada por un piano sintético
cuyos parámetros evoluciona un algoritmo genético implementado desde cero.

## Estado

Notebook completo: síntesis, algoritmo genético, comparación de operadores y de configuraciones, y meta-evaluación.
Falta el informe (`informe/informe.md`), que está en preparación.
Informe técnico: Redactado y disponible en el archivo (`informe/informe.md`)
Evaluación perceptual: Encuesta informal completada y registrada en el archivo (`resultados/encuesta.csv`).

## Contenido

| Carpeta o archivo | Qué es |
| --- | --- |
| `silbido_piano.ipynb` | Notebook único: notas del silbido, cromosoma, síntesis, fitness, operadores genéticos, ciclo del AG, comparaciones, configuraciones y meta-evaluación |
| `audios/` | Entradas: `silbido.wav`, las 5 notas de piano de entrenamiento (D4, F4, A4, C5, D5) y `piano_G4.wav`, que solo se usa en la prueba de generalización |
| `salidas/` | Audios generados por el notebook: melodías con la referencia, el Gen 0 y el mejor individuo, y la nota A4 con el Gen 0 y con el mejor |
| `docs/` | Enunciado del examen |
| `resultados/` | CSV de las corridas, los experimentos y encuesta informal: `combinaciones.csv`, `configs.csv`, `meta.csv`, `azar.csv`, `prematura.csv`, `operadores.csv`, `superficie.csv` y `g4_azar.csv`, `encuesta.csv` |
| `informe/` | `informe.md` y las figuras que genera el notebook en `figuras/` |

## Cómo correrlo

1. Python 3.10 o superior. Instalar las librerías: `pip install numpy==2.5.3 scipy==1.18.1 pandas==3.0.5 matplotlib==3.11.2 ipykernel==7.4.0`.
2. Abrir esta carpeta en Visual Studio Code (extensiones Python y Jupyter) y abrir el notebook.
3. Elegir el kernel de Python y ejecutar todas las celdas de arriba abajo.

Las corridas largas ya están guardadas en `resultados/`, y el notebook las lee en vez de volver a calcularlas, así que
ejecutarlo completo tarda unos minutos. Para recalcularlas hay cuatro interruptores que por defecto valen `False`:
`RECALCULAR` (la corrida base y las 15 de las combinaciones, unos 45 minutos), `CORRER_CONFIGS` (las 36 de las
configuraciones, unos 100 minutos), `CORRER_META` (las 10 de la meta-evaluación) y `CORRER_AZAR` (el baseline aleatorio);
estos dos últimos tardaron unos 75 minutos juntos. Los tiempos son de un equipo de 12 núcleos y las corridas se reparten
entre todos. Las configuraciones, la meta-evaluación y el baseline guardan cada corrida apenas termina, así que si algo
se corta, al relanzar solo se calculan las que faltan.

El notebook lee los audios con la ruta relativa `audios/`, así que debe quedar junto a esa carpeta.
Todas las semillas aleatorias están fijas: 2026 en general, 2026 a 2030 en las comparaciones y 101 a 110 en la
meta-evaluación.

## Audios

Formato WAV mono, 22050 Hz, 16 bits. `piano_G4.wav` no se usa para entrenar el instrumento: solo se carga en la prueba
con una nota no vista. Las notas de piano son del Steinway B de la
Universidad de Iowa, Musical Instrument Samples (https://theremin.music.uiowa.edu/MIS.html), intensidad mf,
recortadas y normalizadas. El silbido es propio.
