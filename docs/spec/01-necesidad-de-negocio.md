# Nivel 1 — Necesidad de negocio

**Responsable:** Negocio
**Estado:** Borrador para validación

Este nivel responde *qué problema del negocio se quiere resolver y por qué*, sin describir solución. De aquí se derivan las historias de usuario (nivel 2).

## Contexto

Hoy la ley de las pilas y del blending se calcula de forma manual en Excel. Esto genera errores de cálculo, datos de muestreo incompletos o mal atribuidos, y desviaciones de ley que se descubren cuando el mineral ya llegó a planta, afectando la recuperación.

## Necesidades

| ID | Necesidad | Impacto en el negocio | Actividad |
|----|-----------|-----------------------|-----------|
| NN-01 | Conocer la ley real de cada pila de forma confiable y auditable, sin cálculos manuales. | Menos errores que afectan la recuperación en planta; datos defendibles ante auditoría. | A4 |
| NN-02 | Garantizar que toda la carga que llega esté muestreada y atribuida a la pila correcta. | Una ley de pila basada en datos completos y bien asignados. | A3 |
| NN-03 | Anticipar la carga diaria y la ley que recibirá planta, antes de cargar las tolvas. | Ajustar la mezcla a tiempo en lugar de descubrir la desviación después. | A6 |

## Priorización (WSJF)

Se tomaron las 3 primeras actividades del ranking WSJF: **A4**, **A3** y **A6**.

## Dependencias entre necesidades

`NN-02` (muestras bien registradas) → `NN-01` (ley de pila) → `NN-03` (ley del blending).
La calidad de cada necesidad depende de la anterior.

## Supuestos y preguntas abiertas

- **Supuesto a validar:** el "ponderado" usa el tonelaje de cada volquete como peso. Si el criterio es otro, cambian NN-01 y NN-03 y todos los niveles siguientes.
- Por definir con Negocio: unidad de la ley (p. ej. g/t o %), el rango objetivo de planta y quién lo mantiene.

## Aprobación

- [ ] Negocio
