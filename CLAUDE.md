# Proyecto: del silbido al piano

Examen práctico grupal de IA (Algoritmos Genéticos), UCB. El enunciado está en docs/. Grupo de 2 personas.
Un AG implementado desde cero evoluciona 12 parámetros de un sintetizador aditivo de piano para que suene parecido
a 5 notas reales (audios/piano_*.wav). El mejor individuo toca la melodía del silbido (audios/silbido.wav, 24 notas,
transpuesta 2 octavas abajo).

## Reglas
- Prohibido deep learning y modelos preentrenados. Solo numpy, scipy, pandas, matplotlib, IPython y soundfile.
- Un solo notebook final reproducible de principio a fin: silbido_piano.ipynb. Todo se agrega como secciones al final.
- Estilo de estudiante: celdas cortas, nombres naturales en español, comentarios breves, sin banners decorativos ni
  sobreingeniería. Todo el texto en español.
- Semilla fija 2026. Las corridas largas guardan sus resultados en resultados/*.csv; el notebook los lee si existen
  (RECALCULAR = False) y los recalcula si es True.
- No cambies lo implementado en la parte 1 sin avisarme.
- Después de cada cambio, ejecuta el notebook completo para comprobar que corre sin errores.

## Commits
- Commits pequeños y concretos, uno por cada cambio lógico (un operador, una función, una sección, un CSV).
- Mensaje de una línea, en español, en imperativo.
- El autor es solo yo. Nada de Co-Authored-By ni menciones a Claude o a IA en los mensajes.
- No hagas push; yo reviso y lo hago.

## Lo que ya está hecho (parte 1)
- Cromosoma de 12 genes en [0, 1]: a2..a6, ataque, tau_rapido, tau_lento, m, s, B, ruido. codificar y decodificar
  pasan entre [0, 1] y rangos físicos.
- sintetizar_instrumento(notas, duraciones, gen): 6 armónicos, caída doble, ruido de golpe fijo.
- Fitness A = 1 / (1 + d/10), con d = error absoluto medio en dB de la STFT (ventana 1024, salto 256, piso -80 dB,
  hasta 8 kHz) promediado en las 5 notas. Fitness B = (1 + r)/2, con r = correlación de los espectrogramas en dB.
- Una evaluación tarda unos 38 ms.

## Diseño que falta implementar
- Selección: torneo k=3 y ruleta. Cruce: blend-alpha (alpha 0.3) y uniforme. Mutación: gaussiana (sigma 0.1),
  uniforme y no uniforme (sigma baja de 0.2 a 0.02). Los hijos se recortan a [0, 1].
- Combinaciones a comparar: C1 torneo + blend + gaussiana, C2 ruleta + uniforme + uniforme, C3 torneo + blend + no
  uniforme. Métricas: aptitud final, generaciones hasta el 90 % del máximo y diversidad (desviación estándar media
  de los genes) por generación.
- Base: N=60, 100 generaciones, 2 de élite, probabilidad de cruce 0.9, mutación 0.08 por gen, torneo k=3, parada por
  20 generaciones sin mejora mayor a 0.0001.

## 12 configuraciones (cada una con 3 semillas, un factor a la vez)
Población: 20, 60 (base), 150. Probabilidad de cruce: 0.5, 0.9 (base), 0.95. Mutación por gen: 0.02, 0.08 (base),
0.3. Élite: 0, 2 (base), 6. Tamaño del torneo: 2, 3 (base), 5. Inmigración: no (base), sí (reemplaza al 10 % peor si
la diversidad cae bajo 0.05). Son 1 base más 11 variaciones.

## Meta-evaluación
- 10 corridas con semillas distintas de la mejor configuración (tabla y boxplot).
- Baseline: búsqueda aleatoria con 10 semillas, con las mismas evaluaciones que gasta la configuración base (el
  promedio de la tabla de configuraciones, 3855) y además con 6000. Test de Mann-Whitney contra el AG.
- Tornado: cada gen ±10 % del rango desde el mejor individuo, cambio en el fitness A.
- Generalización: probar con una nota no vista (G4).
- Audios finales en salidas/: Gen 0, mejor evolucionado y melodía final.

## Informe
informe/informe.md, de 3 a 4 páginas, con las 5 preguntas teóricas del enunciado, sustentadas con números y gráficos
del proyecto. No inventar resultados que no estén en resultados/.
