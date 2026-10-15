# Nivel 2 — Historias de usuario

**Responsables:** Negocio + equipo
**Estado:** Borrador para validación

Cada historia describe *quién necesita qué y para qué*, y se vincula a una necesidad de negocio (nivel 1). El detalle completo de cada una está en su propio archivo.

## Catálogo

| ID | Historia | Rol | Necesidad | Detalle |
|----|----------|-----|-----------|---------|
| HU-A3.1 | Registro de volquete y su muestra | Técnico de muestreo | NN-02 | [HU-A3.1](../HU-A3.1-registro-de-volquete-y-muestra.md) |
| HU-A3.2 | Alerta de volquetes sin muestra o mal asignados | Jefe de control de calidad | NN-02 | [HU-A3.2](../HU-A3.2-alerta-volquetes-sin-muestra.md) |
| HU-A4.1 | Ley de la pila calculada automáticamente | Geólogo de control de calidad | NN-01 | [HU-A4.1](../HU-A4.1-ley-de-pila-automatica.md) |
| HU-A4.2 | Trazabilidad y cierre de la ley de pila | Superintendente de planeamiento | NN-01 | [HU-A4.2](../HU-A4.2-trazabilidad-y-cierre-de-pila.md) |
| HU-A6.1 | Carga del día como suma de la carga de tolvas | Planeador de mina | NN-03 | [HU-A6.1](../HU-A6.1-carga-diaria-de-tolvas.md) |
| HU-A6.2 | Ley esperada del blending diario | Superintendente de operaciones | NN-03 | [HU-A6.2](../HU-A6.2-ley-esperada-del-blending.md) |

## Orden de construcción sugerido

Por dependencias de datos (no por numeración):

1. **HU-A3.1** → base de datos de volquetes y muestras.
2. **HU-A3.2** → calidad del dato.
3. **HU-A4.1** → ley de pila.
4. **HU-A4.2** → cierre y trazabilidad.
5. **HU-A6.1** → carga por tolva.
6. **HU-A6.2** → ley del blending (requiere A4 y A6.1).

## Dependencias

| Historia | Depende de |
|----------|------------|
| HU-A3.2 | HU-A3.1 |
| HU-A4.1 | HU-A3.1 |
| HU-A4.2 | HU-A4.1, HU-A3.2 (justificación de cierre) |
| HU-A6.1 | HU-A4.1 (tonelaje disponible de la pila) |
| HU-A6.2 | HU-A4.1, HU-A4.2 (estado abierta/cerrada), HU-A6.1 |

## Aprobación

- [ ] Negocio
- [ ] Equipo
