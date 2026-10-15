# HU-A6.2: Ley esperada del blending diario

**Actividad:** A6 — Cálculo de la carga diaria y la ley del blending

**Como** superintendente de operaciones,
**quiero** ver la ley ponderada del blending de cada tolva y del día completo, a partir de la ley de las pilas que la componen,
**para** anticipar la ley que recibirá planta y ajustar la mezcla antes de cargar, en lugar de descubrir la desviación después.

## Criterios de aceptación

- [ ] Ley de tolva = Σ(ley de pila × toneladas aportadas) ÷ Σ toneladas de la tolva.
- [ ] Ley del día = Σ(ley de tolva × toneladas de tolva) ÷ Σ toneladas del día.
- [ ] Si se usa una pila abierta (ley aún provisional), el sistema lo marca visiblemente.
- [ ] Se alerta cuando la ley de una tolva o del día sale del rango objetivo definido por planta.

## Supuesto a validar

El "ponderado" usa el tonelaje como peso. Si se usa otro criterio, cambian los criterios de aceptación.

## Trazabilidad

| Nivel | Referencia |
|-------|------------|
| Necesidad de negocio | NN-03 — [nivel 1](spec/01-necesidad-de-negocio.md) |
| Historia de usuario | [nivel 2](spec/02-historias-de-usuario.md) |
| Criterios de aceptación | CA-A6.2-01 a 04 — [nivel 3](spec/03-criterios-de-aceptacion.md) |
| Especificación funcional | RF-19 a RF-21, RN-02, RN-03 — [nivel 4](spec/04-especificacion-funcional.md) |
| Especificación técnica preliminar | [nivel 5](spec/05-especificacion-tecnica-preliminar.md) |
