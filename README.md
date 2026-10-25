# Del silbido al piano: examen práctico de Algoritmos Genéticos

IA, Universidad Católica Boliviana. Un silbido se convierte en una melodía tocada por un piano sintético
cuyos parámetros evoluciona un algoritmo genético implementado desde cero.

## Contenido

| Carpeta o archivo | Qué es |
| --- | --- |
| `parte1_silbido_piano.ipynb` | Notebook: notas del silbido, cromosoma, síntesis y fitness |
| `audios/` | Entradas: `silbido.wav` y 5 notas de piano (D4, F4, A4, C5, D5) |
| `salidas/` | Audios generados por el notebook |
| `requirements.txt` | Librerías necesarias |

## Cómo correrlo

1. Python 3.10 o superior. Instalar las librerías: `pip install -r requirements.txt`.
2. Abrir esta carpeta en Visual Studio Code (extensiones Python y Jupyter) y abrir el notebook.
3. Elegir el kernel de Python y ejecutar todas las celdas de arriba abajo.

El notebook lee los audios con la ruta relativa `audios/`, así que debe quedar junto a esa carpeta.
Todas las semillas aleatorias están fijas (2026).

## Audios

Formato WAV mono, 22050 Hz, 16 bits. Las notas de piano son del Steinway B de la
Universidad de Iowa, Musical Instrument Samples (https://theremin.music.uiowa.edu/MIS.html), intensidad mf,
recortadas y normalizadas. El silbido es propio.

## Uso de IA

En el diseño y la implementación se usó asistencia de IA generativa (Claude, Anthropic, 2026), revisada por las
integrantes. No se usa ningún modelo preentrenado de deep learning.
