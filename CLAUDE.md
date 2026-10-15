# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Estado del repositorio

Sistema de gestión de muestreo SIG y blending para una operación minera: registro de volquetes y muestras (A3), ley ponderada por pila (A4) y carga diaria y ley del blending (A6).

Hoy el repo contiene **solo documentación** (`README.md`, que solo tiene el título, y `docs/`). No hay código, stack, build, lint ni tests definidos; el stack es una decisión pendiente (ver nivel 5 de la spec). No inventes comandos de build/test: si se agrega código, actualiza esta sección.

## Metodología: Spec-Driven Development (SDD)

La especificación manda. El código y los cambios se derivan de ella, no al revés. Los documentos están escritos en español y forman una escalera de lo general a lo verificable:

| Nivel | Archivo | Responsable / aprueba |
|-------|---------|-----------------------|
| 1. Necesidad de negocio | `docs/spec/01-necesidad-de-negocio.md` | Negocio |
| 2. Historia de usuario | `docs/spec/02-historias-de-usuario.md` + `docs/HU-*.md` | Negocio + equipo |
| 3. Criterio de aceptación | `docs/spec/03-criterios-de-aceptacion.md` | Negocio + calidad |
| 4. Especificación funcional | `docs/spec/04-especificacion-funcional.md` | Equipo, aprueba el BP |
| 5. Especificación técnica preliminar | `docs/spec/05-especificacion-tecnica-preliminar.md` | Desarrollo, aprueba el responsable técnico |

### Orden de lectura obligatorio antes de cualquier cambio

1. `README.md`
2. Las historias de usuario: `docs/HU-*.md` (una por archivo; el catálogo y las dependencias están en `docs/spec/02-historias-de-usuario.md`).
3. La spec, en orden de nivel 1 a 5, en `docs/spec/`.

No modifiques ni escribas código sin haber leído al menos la HU afectada y los niveles 3 a 5 que la referencian.

### Trazabilidad

Cada HU termina con una sección **Trazabilidad** que apunta a su necesidad (`NN-xx`), sus criterios (`CA-Axx-nn`) y sus requisitos (`RF-nn`, `RN-nn`). Los IDs son la cadena que une los niveles:

`NN` (necesidad) → `HU-Ax.y` → `CA-Ax.y-nn` → `RF-nn` / `RN-nn` → especificación técnica

## Reglas de trabajo

- **Un cambio se propaga hacia abajo.** Si cambia un nivel, revisa y actualiza todos los niveles inferiores y la sección Trazabilidad de las HU afectadas. Mantén los IDs estables; no los renumeres.
- **Código y pruebas citan IDs.** Toda funcionalidad implementada debe poder rastrearse a un `RF`/`CA`; se prueba un criterio de aceptación por prueba. Los ejemplos numéricos del nivel 3 (ley de pila 1,336; tolva 1,42; día 1,38; 90 t disponibles) sirven como casos de prueba de las fórmulas.
- **No decidas lo que la spec deja abierto.** Las preguntas abiertas del nivel 4 (para el BP) y las **[Decisión]** del nivel 5 (para el responsable técnico) requieren aprobación; no las resuelvas por tu cuenta, señálalas.
- **Aprobaciones.** Las casillas de aprobación de cada documento indican si un nivel está validado; no las marques tú.
- **Si el código contradice la spec**, la spec gana salvo que el usuario indique lo contrario; propón el cambio de spec primero.

## Conocimiento de dominio que cruza varios documentos

- **Supuesto a validar:** el "ponderado" usa el **tonelaje del volquete como peso**. Aplica a RN-01, RN-02, RN-03 y a los criterios de A4 y A6. Si cambia, cambia todo lo que depende de él.
- **Cadena de cálculo:** muestra → ley de pila (RN-01) → ley de tolva (RN-02) → ley del día (RN-03). Una pila sin muestras no tiene ley (no es 0).
- **Dependencias entre HU:** A3.1 → A3.2 y A4.1 → A4.2 → A6.1 → A6.2. El orden de construcción sugerido está en el nivel 2, no sigue la numeración.
- **Estados de pila:** abierta, con observaciones, cerrada. Una pila cerrada bloquea su edición y solo un rol autorizado la reabre con motivo. La ley de una pila abierta es provisional y debe marcarse así en el blending.
- **Bitácora:** asignaciones, cierres y reaperturas se registran con quién, qué y cuándo (RN-06).
- **Captura en campo:** el registro de volquetes debe funcionar desde móvil/tablet, incluso sin conexión, con sincronización idempotente.
- **Integración:** las pilas/polígonos provienen del programa de muestreo SIG; el mecanismo de integración está sin decidir.

## Git

- Rama de trabajo actual: `fix/HU-A3.1`, con remoto `origin` (GitHub: LeonardoVera/Sistema-Gestion-Muestreo-SIG-Blending-2); la rama principal es `main`.
- Mensajes de commit en español con prefijo convencional (`docs:`, `fix:`), p. ej. `docs: generacion de specs`.
- El usuario ha pedido commits sin línea de coautoría.
- `gh` (GitHub CLI) no está instalado en esta máquina; los PR se abren desde la web.
