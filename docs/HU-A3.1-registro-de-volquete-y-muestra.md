# HU-A3.1: Registro de volquete y su muestra

**Actividad:** A3 — Registro de muestras por volquete

**Como** técnico de muestreo,
**quiero** registrar cada volquete que llega y asociarlo a la pila (polígono) de su labor de origen,
**para** garantizar que toda la carga esté muestreada y que cada muestra cuente para la pila correcta.

## Criterios de aceptación

- [ ] Por cada volquete se registra: pila/polígono, labor, placa, tonelaje, fecha y hora, y código de muestra.
- [ ] Se genera una sola muestra por volquete y no se permite duplicar el código de muestra.
- [ ] Solo se puede asignar el volquete a pilas existentes en el programa de muestreo SIG.
- [ ] El registro funciona desde el punto de muestreo, sin depender de la oficina (móvil o tablet).
- [ ] El tonelaje del volquete debe ser mayor que cero y no superar la capacidad máxima configurada; de lo contrario se rechaza el registro con un mensaje claro.
- [ ] Si no hay conexión, los registros se guardan en el dispositivo y se sincronizan automáticamente al recuperar la señal.

## Trazabilidad

| Nivel | Referencia |
|-------|------------|
| Necesidad de negocio | NN-02 — [nivel 1](spec/01-necesidad-de-negocio.md) |
| Historia de usuario | [nivel 2](spec/02-historias-de-usuario.md) |
| Criterios de aceptación | CA-A3.1-01 a 07 — [nivel 3](spec/03-criterios-de-aceptacion.md) |
| Especificación funcional | RF-01 a RF-05 — [nivel 4](spec/04-especificacion-funcional.md) |
| Especificación técnica preliminar | [nivel 5](spec/05-especificacion-tecnica-preliminar.md) |
