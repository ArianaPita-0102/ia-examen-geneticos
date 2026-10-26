# Del silbido al piano: informe

IA, Universidad Católica Boliviana. Examen práctico grupal de Algoritmos Genéticos.
Integrantes: ______________________ y ______________________

## Resumen

Un algoritmo genético (AG) hecho desde cero evoluciona los 12 parámetros de un piano sintético aditivo para que suene
parecido a 5 notas reales (D4, F4, A4, C5, D5). El mejor individuo toca la melodía del silbido (24 notas, bajadas 2
octavas). El fitness A vale 1 / (1 + d/10), donde d es el error medio en dB entre los espectrogramas de la nota
sintética y la real.

Con 10 semillas el AG llega a 0.7321 ± 0.0005, contra 0.7164 ± 0.0032 de una búsqueda aleatoria con 6000 evaluaciones.
Los números salen de `resultados/*.csv`; los pocos que vienen de una salida del notebook llevan la marca (notebook).
Las figuras se generan en `silbido_piano.ipynb` y se guardan en `informe/figuras/`. Las notas de piano son del
Steinway B de la Universidad de Iowa (Musical Instrument Samples, https://theremin.music.uiowa.edu/MIS.html).
