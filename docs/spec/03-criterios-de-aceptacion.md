# Nivel 3 — Criterios de aceptación

**Responsables:** Negocio + calidad
**Estado:** Borrador para validación

Cada criterio de la historia se reescribe como escenario verificable (Dado / Cuando / Entonces) con un ID, para poder probarlo. Las cifras de los ejemplos son ilustrativas.

> **Supuesto:** el peso del ponderado es el tonelaje del volquete.

---

## HU-A3.1 — Registro de volquete y su muestra

| ID | Escenario |
|----|-----------|
| CA-A3.1-01 | **Dado** un volquete que llega, **cuando** el técnico lo registra, **entonces** se guardan pila/polígono, labor, placa, tonelaje, fecha y hora, y código de muestra. |
| CA-A3.1-02 | **Dado** un volquete ya registrado con su muestra, **cuando** se intenta crear otra muestra para el mismo volquete, **entonces** el sistema lo impide. |
| CA-A3.1-03 | **Dado** un código de muestra existente, **cuando** se intenta registrar otro volquete con el mismo código, **entonces** se rechaza indicando que está duplicado. |
| CA-A3.1-04 | **Dado** una pila que no existe en el programa de muestreo SIG, **cuando** se intenta asignar un volquete a ella, **entonces** no se permite y solo se ofrecen pilas existentes. |
| CA-A3.1-05 | **Dado** un técnico en el punto de muestreo con móvil o tablet, **cuando** registra un volquete, **entonces** puede completarlo sin usar la oficina. |
| CA-A3.1-06 | **Dado** un tonelaje igual a 0, negativo o mayor a la capacidad máxima configurada, **cuando** se intenta guardar, **entonces** se rechaza con un mensaje claro. |
| CA-A3.1-07 | **Dado** que no hay conexión, **cuando** el técnico registra volquetes, **entonces** se guardan en el dispositivo y se sincronizan al recuperar la señal. |

## HU-A3.2 — Alerta de volquetes sin muestra o mal asignados

| ID | Escenario |
|----|-----------|
| CA-A3.2-01 | **Dado** volquetes sin muestra, **cuando** el jefe consulta pendientes, **entonces** ve la lista por pila y por turno con su antigüedad. |
| CA-A3.2-02 | **Dado** un volquete asignado a una pila equivocada, **cuando** se corrige la pila, **entonces** queda registrado quién cambió qué (valor anterior y nuevo) y cuándo. |
| CA-A3.2-03 | **Dado** una pila con volquetes sin muestra, **cuando** se intenta cerrar sin justificación, **entonces** el sistema no lo permite. |
| CA-A3.2-04 | **Dado** una pila con volquetes sin muestra, **cuando** se cierra con justificación, **entonces** el cierre se completa y la justificación queda guardada. |

## HU-A4.1 — Ley de la pila calculada automáticamente

| ID | Escenario |
|----|-----------|
| CA-A4.1-01 | **Dado** una pila con volquete 1 (30 t, ley 1,20) y volquete 2 (25 t, ley 1,50), **cuando** se calcula, **entonces** la ley de pila es (30×1,20 + 25×1,50) ÷ 55 = **1,336**. |
| CA-A4.1-02 | **Dado** el caso anterior más un volquete 3 de 20 t sin muestra, **cuando** se calcula, **entonces** la ley sigue siendo 1,336 y el volquete 3 aparece aparte como sin muestra. |
| CA-A4.1-03 | **Dado** una pila con ley calculada, **cuando** se registra o corrige una muestra, **entonces** la ley se recalcula automáticamente. |
| CA-A4.1-04 | **Dado** una pila, **cuando** se consulta, **entonces** se muestran tonelaje acumulado, número de volquetes y número de muestras. |
| CA-A4.1-05 | **Dado** una pila sin ninguna muestra, **cuando** se consulta, **entonces** no se muestra ley (sin dato) en lugar de 0. |

## HU-A4.2 — Trazabilidad y cierre de la ley de pila

| ID | Escenario |
|----|-----------|
| CA-A4.2-01 | **Dado** la ley de una pila, **cuando** el usuario abre el detalle, **entonces** ve volquete, tonelaje, ley y hora de cada muestra que la compone. |
| CA-A4.2-02 | **Dado** una pila cerrada, **cuando** alguien intenta registrar o corregir un volquete o muestra en ella, **entonces** el sistema lo bloquea. |
| CA-A4.2-03 | **Dado** una pila cerrada, **cuando** un usuario con rol autorizado la reabre indicando el motivo, **entonces** la pila vuelve a abierta y el motivo queda registrado. |
| CA-A4.2-04 | **Dado** una pila cerrada, **cuando** un usuario sin rol autorizado intenta reabrirla, **entonces** no puede. |
| CA-A4.2-05 | **Dado** cualquier pila, **cuando** se consulta, **entonces** se muestra su estado: abierta, cerrada o con observaciones. |

## HU-A6.1 — Carga del día como suma de la carga de tolvas

| ID | Escenario |
|----|-----------|
| CA-A6.1-01 | **Dado** la tolva 1 con 40 t de la pila A y 60 t de la pila B, **cuando** se calcula, **entonces** la carga de la tolva 1 es **100 t**. |
| CA-A6.1-02 | **Dado** la tolva 1 con 100 t y la tolva 2 con 50 t, **cuando** se calcula el día, **entonces** la carga del día es **150 t**. |
| CA-A6.1-03 | **Dado** la carga del día, **cuando** se consulta el detalle, **entonces** se ve por tolva y por pila de origen. |
| CA-A6.1-04 | **Dado** una pila con 90 t disponibles, **cuando** se intenta cargar más de 90 t en total a tolvas, **entonces** el sistema lo rechaza indicando el tonelaje disponible. |

## HU-A6.2 — Ley esperada del blending diario

| ID | Escenario |
|----|-----------|
| CA-A6.2-01 | **Dado** la tolva 1 con 40 t de la pila A (ley 1,30) y 60 t de la pila B (ley 1,50), **cuando** se calcula, **entonces** la ley de la tolva 1 es (40×1,30 + 60×1,50) ÷ 100 = **1,42**. |
| CA-A6.2-02 | **Dado** además la tolva 2 con 50 t de ley 1,30, **cuando** se calcula el día, **entonces** la ley del día es (100×1,42 + 50×1,30) ÷ 150 = **1,38**. |
| CA-A6.2-03 | **Dado** que una tolva usa una pila abierta, **cuando** se muestra su ley, **entonces** se marca visiblemente como provisional. |
| CA-A6.2-04 | **Dado** el rango objetivo definido por planta, **cuando** la ley de una tolva o del día queda fuera de él, **entonces** el sistema emite una alerta. |

---

## Aprobación

- [ ] Negocio
- [ ] Calidad
