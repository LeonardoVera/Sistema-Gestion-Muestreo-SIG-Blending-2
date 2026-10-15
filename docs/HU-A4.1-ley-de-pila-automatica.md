# HU-A4.1: Ley de la pila calculada automáticamente

**Actividad:** A4 — Cálculo de ley ponderada por pila

**Como** geólogo de control de calidad,
**quiero** que el sistema calcule la ley de cada pila como el promedio ponderado de las muestras de sus volquetes,
**para** conocer la ley real del mineral sin cálculos manuales en Excel y reducir errores que afectan la recuperación en planta.

## Criterios de aceptación

- [ ] Ley de pila = Σ(ley de muestra × tonelaje del volquete) ÷ Σ tonelaje de volquetes con muestra.
- [ ] El cálculo se actualiza cada vez que se registra o corrige una muestra de esa pila.
- [ ] Se muestran el tonelaje acumulado, el número de volquetes y el número de muestras de la pila.
- [ ] Los volquetes sin muestra no entran en el cálculo y se informan aparte.

## Supuesto a validar

El "ponderado" usa el tonelaje de cada volquete como peso. Si se usa otro criterio, cambian los criterios de aceptación.
