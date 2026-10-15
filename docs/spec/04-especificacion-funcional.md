# Nivel 4 — Especificación funcional

**Responsables:** Equipo
**Aprueba:** BP (Business Partner)
**Estado:** Borrador para validación

Describe *qué hace el sistema* para cumplir los criterios de aceptación (nivel 3): roles, estados, reglas, cálculos, pantallas y mensajes. No define tecnología.

## 1. Roles y permisos

| Rol | Registrar volquete/muestra | Corregir asignación | Ver ley de pila | Cerrar pila | Reabrir pila | Cargar tolvas | Ver blending |
|-----|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
| Técnico de muestreo | ✔ | — | — | — | — | — | — |
| Jefe de control de calidad | ✔ | ✔ | ✔ | ✔ | — | — | — |
| Geólogo de control de calidad | — | — | ✔ | — | — | — | — |
| Superintendente de planeamiento | — | — | ✔ | ✔ | ✔ (rol autorizado) | — | ✔ |
| Planeador de mina | — | — | ✔ | — | — | ✔ | ✔ |
| Superintendente de operaciones | — | — | ✔ | — | — | — | ✔ |

> Por confirmar con el BP: qué roles son "autorizados" para reabrir una pila y cuáles pueden cerrarla.

## 2. Entidades de negocio

- **Pila (polígono):** definida en el programa de muestreo SIG. Tiene estado.
- **Volquete:** placa, labor de origen, tonelaje, fecha y hora, pila asignada.
- **Muestra:** código único, ley, hora; una por volquete.
- **Tolva:** destino de carga diaria.
- **Carga de tolva:** toneladas enviadas desde una pila a una tolva en un día.

## 3. Estados de la pila

```
Abierta ──cerrar──▶ Cerrada ──reabrir (rol autorizado + motivo)──▶ Abierta
   │
   └── "Con observaciones" cuando hay volquetes sin muestra, o se cerró con justificación
```

| Estado | Significado | Se puede registrar/corregir |
|--------|-------------|:--:|
| Abierta | Ley provisional, puede cambiar | Sí |
| Con observaciones | Tiene volquetes sin muestra o cierre justificado | Sí, si no está cerrada |
| Cerrada | Ley definitiva, bloqueada | No |

## 4. Requisitos funcionales

### Registro de muestras (A3)

| ID | Requisito | Criterios |
|----|-----------|-----------|
| RF-01 | Registrar volquete con pila/polígono, labor, placa, tonelaje, fecha/hora y código de muestra. | CA-A3.1-01 |
| RF-02 | Una muestra por volquete; código de muestra único. | CA-A3.1-02, 03 |
| RF-03 | Solo permitir pilas existentes en el programa de muestreo SIG. | CA-A3.1-04 |
| RF-04 | Operar desde móvil o tablet en el punto de muestreo, también sin conexión con sincronización posterior. | CA-A3.1-05, 07 |
| RF-05 | Validar tonelaje > 0 y ≤ capacidad máxima configurada. | CA-A3.1-06 |
| RF-06 | Listar volquetes sin muestra por pila y turno, con antigüedad. | CA-A3.2-01 |
| RF-07 | Corregir la pila asignada a un volquete con bitácora (quién, qué, cuándo). | CA-A3.2-02 |
| RF-08 | Impedir el cierre de una pila con volquetes sin muestra salvo justificación. | CA-A3.2-03, 04 |

### Ley de pila (A4)

| ID | Requisito | Criterios |
|----|-----------|-----------|
| RF-09 | Calcular la ley de pila como promedio ponderado por tonelaje de volquetes con muestra. | CA-A4.1-01, 02, 05 |
| RF-10 | Recalcular al registrar o corregir una muestra. | CA-A4.1-03 |
| RF-11 | Mostrar tonelaje acumulado, nº de volquetes y nº de muestras; informar aparte los volquetes sin muestra. | CA-A4.1-02, 04 |
| RF-12 | Mostrar detalle de muestras que componen la ley (volquete, tonelaje, ley, hora). | CA-A4.2-01 |
| RF-13 | Cerrar la pila y bloquear su edición. | CA-A4.2-02 |
| RF-14 | Reabrir una pila cerrada solo con rol autorizado, registrando el motivo. | CA-A4.2-03, 04 |
| RF-15 | Mostrar el estado de la pila (abierta, cerrada, con observaciones). | CA-A4.2-05 |

### Blending (A6)

| ID | Requisito | Criterios |
|----|-----------|-----------|
| RF-16 | Registrar toneladas cargadas a cada tolva desde cada pila. | CA-A6.1-01 |
| RF-17 | Calcular la carga de cada tolva y la carga total del día, con detalle por tolva y pila de origen. | CA-A6.1-01, 02, 03 |
| RF-18 | Rechazar cargas que excedan el tonelaje disponible de la pila. | CA-A6.1-04 |
| RF-19 | Calcular la ley de cada tolva y del día, ponderadas por toneladas. | CA-A6.2-01, 02 |
| RF-20 | Marcar visiblemente las leyes que usan pilas abiertas como provisionales. | CA-A6.2-03 |
| RF-21 | Alertar cuando la ley de tolva o del día sale del rango objetivo de planta. | CA-A6.2-04 |

## 5. Reglas de negocio y cálculos

| ID | Regla |
|----|-------|
| RN-01 | Ley de pila = Σ(ley muestra × tonelaje volquete) ÷ Σ tonelaje de volquetes con muestra. |
| RN-02 | Ley de tolva = Σ(ley pila × toneladas aportadas) ÷ Σ toneladas de la tolva. |
| RN-03 | Ley del día = Σ(ley tolva × toneladas tolva) ÷ Σ toneladas del día. |
| RN-04 | Tonelaje disponible de pila = tonelaje acumulado de la pila − toneladas ya cargadas a tolvas. |
| RN-05 | Una pila sin muestras no tiene ley; no puede aportar a una ley de blending (decisión por confirmar con el BP: bloquear o advertir). |
| RN-06 | Todo cambio de asignación, cierre o reapertura queda en bitácora con usuario y fecha/hora. |
| RN-07 | El tonelaje disponible considera solo el tonelaje de volquetes registrados (con o sin muestra) — por confirmar. |

## 6. Pantallas principales

| Pantalla | Usuario | Contenido |
|----------|---------|-----------|
| Registro de volquete | Técnico | Formulario con pila (lista de pilas SIG), labor, placa, tonelaje, código de muestra; indicador de conexión/pendiente de sincronizar. |
| Pendientes de muestra | Jefe de CC | Tabla por pila y turno con antigüedad; acción de corregir asignación. |
| Detalle de pila | Geólogo / Planeamiento | Ley, tonelaje, nº volquetes y muestras, estado, listado de muestras, volquetes sin muestra, acciones cerrar/reabrir. |
| Carga de tolvas | Planeador | Matriz tolva × pila con toneladas y disponible de cada pila. |
| Blending del día | Planeador / Operaciones | Ley y carga por tolva y del día, marca de provisional, alertas fuera de rango. |

## 7. Mensajes clave

- "El código de muestra ya existe."
- "La pila seleccionada no existe en el programa de muestreo SIG."
- "El tonelaje debe ser mayor que 0 y no superar {capacidad} t."
- "La pila tiene {n} volquetes sin muestra. Ingrese una justificación para cerrarla."
- "La pila está cerrada. Solo un usuario autorizado puede reabrirla."
- "La pila {x} solo tiene {disp} t disponibles."
- "Ley provisional: incluye pilas abiertas."
- "La ley de la tolva {n} ({valor}) está fuera del rango objetivo ({min}–{max})."

## 8. Preguntas abiertas para el BP

1. ¿Qué roles pueden cerrar y cuáles reabrir una pila?
2. ¿Qué pasa con una pila sin muestras en el blending: se bloquea o se advierte?
3. ¿Se define "turno" por horario fijo? ¿Cuáles son los turnos?
4. ¿El rango objetivo es único o varía por día/tolva?
5. ¿Cuántos elementos/leyes se manejan (uno o varios)?

## Aprobación

- [ ] Equipo
- [ ] BP
