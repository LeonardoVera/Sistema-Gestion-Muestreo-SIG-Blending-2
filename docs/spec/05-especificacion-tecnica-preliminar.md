# Nivel 5 — Especificación técnica preliminar

**Responsable:** Desarrollo
**Aprueba:** Responsable técnico
**Estado:** Borrador — propuesta sujeta a decisiones de arquitectura

Traduce la especificación funcional (nivel 4) en una propuesta técnica. Es *preliminar*: los puntos marcados como **[Decisión]** deben confirmarse antes de construir. El repositorio aún no tiene código ni stack definido.

## 1. Alcance técnico

Aplicación con captura en campo (móvil/tablet, con modo sin conexión), cálculo de leyes, bitácora de auditoría y vista de blending. Integración de lectura con el programa de muestreo SIG para obtener las pilas.

## 2. Modelo de datos propuesto

| Entidad | Campos principales |
|---------|--------------------|
| `pila` | id, codigo_sig, poligono, estado (`abierta` \| `cerrada` \| `con_observaciones`), cerrada_por, cerrada_en, justificacion_cierre |
| `volquete` | id, pila_id, labor, placa, tonelaje, registrado_en, registrado_por, turno |
| `muestra` | id, volquete_id (único), codigo (único), ley, tomada_en |
| `tolva` | id, nombre |
| `carga_tolva` | id, fecha, tolva_id, pila_id, toneladas, registrado_por |
| `parametro_planta` | id, ley_min, ley_max, vigente_desde |
| `bitacora` | id, entidad, entidad_id, accion, valor_anterior, valor_nuevo, usuario, fecha_hora, motivo |

Restricciones clave:

- `muestra.volquete_id` único (RF-02) y `muestra.codigo` único (RF-02).
- `volquete.pila_id` referencia una pila sincronizada del SIG (RF-03).
- `volquete.tonelaje` > 0 y ≤ parámetro de capacidad máxima (RF-05).
- No se permiten escrituras sobre volquetes/muestras de una pila `cerrada` (RF-13).

## 3. Cálculo de leyes

| Cálculo | Estrategia propuesta |
|---------|----------------------|
| Ley de pila (RN-01) | Calcular en servidor bajo demanda a partir de volquetes con muestra; **[Decisión]** si se persiste un valor derivado para rendimiento. |
| Ley de tolva y día (RN-02, 03) | Calcular en servidor a partir de `carga_tolva` y la ley vigente de cada pila. |
| Tonelaje disponible (RN-04) | Σ tonelaje de volquetes de la pila − Σ `carga_tolva.toneladas`. |

- Usar tipos decimales exactos (no coma flotante) para ley y tonelaje.
- **[Decisión]** precisión y redondeo (decimales mostrados vs. almacenados).
- La validación de carga (RF-18) debe ser transaccional para evitar sobrecargar una pila con cargas concurrentes.

## 4. Interfaz de servicios (propuesta)

| Método | Ruta | Función |
|--------|------|---------|
| GET | `/pilas` | Pilas del SIG con estado, ley, tonelaje (RF-09, 11, 15) |
| GET | `/pilas/{id}` | Detalle y muestras componentes (RF-12) |
| POST | `/pilas/{id}/cierre` | Cerrar, con justificación si aplica (RF-08, 13) |
| POST | `/pilas/{id}/reapertura` | Reabrir con motivo; requiere rol (RF-14) |
| POST | `/volquetes` | Registrar volquete y muestra (RF-01, 02, 05) |
| PATCH | `/volquetes/{id}/pila` | Corregir pila con bitácora (RF-07) |
| GET | `/volquetes/pendientes` | Sin muestra por pila/turno (RF-06) |
| POST | `/cargas-tolva` | Registrar carga (RF-16, 18) |
| GET | `/blending?fecha=` | Carga y ley por tolva y día (RF-17, 19, 20, 21) |

## 5. Requisitos no funcionales

| Tema | Requisito preliminar |
|------|----------------------|
| Modo sin conexión | Cola local en el dispositivo; sincronización idempotente (clave de cliente por registro) para no duplicar volquetes ni códigos de muestra (RF-04). |
| Resolución de conflictos | **[Decisión]** qué ocurre si un registro offline llega a una pila ya cerrada o con código duplicado. |
| Auditoría | Bitácora inmutable (solo inserción) de asignaciones, cierres y reaperturas (RN-06). |
| Seguridad | Autenticación y autorización por rol (sección 1 de la especificación funcional). |
| Dispositivos | Interfaz web adaptable (móvil/tablet); **[Decisión]** web instalable vs. app nativa. |
| Rendimiento | Cálculo de blending diario en tiempo interactivo para el volumen de un día de operación (volumen por definir). |
| Disponibilidad | Captura en campo debe seguir funcionando con conectividad intermitente. |

## 6. Integración con el programa de muestreo SIG

- Fuente de las pilas/polígonos (RF-03).
- **[Decisión]** mecanismo (API, archivo, base compartida), frecuencia de sincronización y qué hacer si una pila se elimina o cambia en el SIG.

## 7. Estrategia de pruebas

- Pruebas unitarias de las fórmulas RN-01 a RN-04 con los ejemplos numéricos del nivel 3 (1,336; 1,42; 1,38; 90 t disponibles).
- Pruebas de las restricciones de datos (unicidad, tonelaje, pila cerrada).
- Pruebas de sincronización offline (duplicados, orden, conflictos).
- Una prueba por cada ID de criterio de aceptación (CA-…) para trazabilidad.

## 8. Riesgos

| Riesgo | Mitigación |
|--------|------------|
| El criterio de ponderación no es el tonelaje. | Validar el supuesto con Negocio antes de construir A4 y A6. |
| Duplicados al sincronizar registros offline. | Claves idempotentes y restricciones únicas en base de datos. |
| Cambios en el SIG rompen la asignación de pilas. | Definir contrato de integración y manejo de pilas dadas de baja. |
| Cargas concurrentes exceden el tonelaje disponible. | Validación transaccional. |

## 9. Decisiones pendientes

1. Stack tecnológico y hosting.
2. Persistir o calcular las leyes derivadas.
3. Precisión y redondeo.
4. Mecanismo de integración con el SIG.
5. Web adaptable vs. app nativa.
6. Política de conflictos en sincronización offline.

## Aprobación

- [ ] Desarrollo
- [ ] Responsable técnico
