# HU-A6.1: Carga del día como suma de la carga de tolvas

**Actividad:** A6 — Cálculo de la carga diaria y la ley del blending

**Como** planeador de mina,
**quiero** que el sistema sume lo que se carga a cada tolva desde cada pila y entregue la carga total del día,
**para** saber cuántas toneladas se enviaron a planta y de qué pilas provienen, sin consolidación manual.

## Criterios de aceptación

- [ ] Carga de tolva = suma de toneladas enviadas desde cada pila a esa tolva.
- [ ] Carga del día = suma de las cargas de todas las tolvas.
- [ ] Se muestra el detalle por tolva y por pila de origen.
- [ ] No se puede cargar a una tolva más tonelaje del que tiene disponible la pila.

## Trazabilidad

| Nivel | Referencia |
|-------|------------|
| Necesidad de negocio | NN-03 — [nivel 1](spec/01-necesidad-de-negocio.md) |
| Historia de usuario | [nivel 2](spec/02-historias-de-usuario.md) |
| Criterios de aceptación | CA-A6.1-01 a 04 — [nivel 3](spec/03-criterios-de-aceptacion.md) |
| Especificación funcional | RF-16 a RF-18, RN-04 — [nivel 4](spec/04-especificacion-funcional.md) |
| Especificación técnica preliminar | [nivel 5](spec/05-especificacion-tecnica-preliminar.md) |
