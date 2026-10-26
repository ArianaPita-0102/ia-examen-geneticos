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

## 1. ¿Cómo influye la representación del cromosoma en la eficiencia del AG?

El cromosoma tiene 12 genes reales en [0, 1]: las amplitudes de los armónicos 2 a 6, el ataque, las dos caídas (rápida
y lenta), el peso `m` entre ambas, `s`, la inarmonicidad `B` y el ruido del golpe. `decodificar` los lleva a su rango
físico. Las notas no están en el cromosoma: el instrumento evolucionado toca cualquier melodía después.

La representación decide el tamaño del espacio y qué tan bien funcionan los operadores. Con 100 niveles por gen hay
10^24 instrumentos posibles (notebook), imposible de recorrer entero, pero con 12 genes el AG sí puede explorarlo.
Además, como todos los genes están en [0, 1], un mismo sigma de mutación (0.1) y un mismo alpha de cruce (0.3) sirven
para todos.

Un ejemplo de mala codificación sería guardar los genes en unidades físicas. Sus rangos van de 0.002 (`B`) a 2.7
(`tau_lento`), 1350 veces de diferencia, y una mutación de 0.1 sería 50 veces el rango de `B`, que quedaría siempre en
un extremo. Otra mala sería meter las 24 notas en el cromosoma: más genes y un fitness que mezcla melodía con timbre.
La codificación elegida evita las dos. Ninguna alternativa se probó, así que esto es un argumento y no un resultado.

La Figura 1 muestra cuánto pesa cada gen: `a2`, `m` y `a4` bajan el fitness más de 0.012 con un cambio del 10 %, y
`tau_rapido` y `tau_lento` lo mueven menos de 0.001. Dos de los 12 genes casi no influyen.

<p align="center"><img src="figuras/tornado.png" width="55%"><br><em>Figura 1. Cambio del fitness A al mover cada gen ±10 % de su rango desde el mejor individuo.</em></p>
