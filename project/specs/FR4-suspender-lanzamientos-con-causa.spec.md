# FR4-suspender-lanzamientos-con-causa

## 1. Problema

Suspender lanzamientos con causa.

### Contexto

El PRD exige que el sistema permita suspender lanzamientos indicando una causa estandarizada (`economica`, `tecnica` o `climatica`) y bloqueando nuevas reservas. Sin esta capacidad, la operación no puede reaccionar formalmente ante riesgos, ni activar el flujo correcto de comunicación y devoluciones.

### Historias de usuario

- Como `operador` quiero **suspender un lanzamiento con una causa obligatoria** para _registrar la decisión operativa con trazabilidad_.
- Como `operador` quiero **bloquear automáticamente nuevas reservas al suspender** para _evitar ventas inválidas_.
- Como `operador` quiero **consultar el historial de suspensión** para _auditar decisiones y preparar acciones posteriores_.

### Fuera de scope

- Motor de predicción automática de suspensión por clima.
- Integración con proveedores meteorológicos reales.
- Replanificación automática de pasajeros a otros lanzamientos.

---

## 2. Solución

Se incorpora un flujo de suspensión explícito sobre la entidad `Lanzamiento`, con transición controlada a `suspendido`, causa estandarizada obligatoria y bloqueo de nuevas reservas. El módulo preserva trazabilidad completa del evento para auditoría, operaciones y ejecución posterior de devoluciones.

### Modelo

#### Lanzamiento (extensión funcional)
- id: `uuid`, identificador único.
- estado: `enum`, valores `programado | confirmado | suspendido | cerrado`.
- causaSuspension: `enum|null`, valores `economica | tecnica | climatica`.
- suspendidoEn: `datetime|null`, fecha/hora del cambio a suspendido.
- suspendidoPor: `string|null`, identificador del operador interno.

**Reglas**:
- Regla1: para transición a `suspendido`, `causaSuspension` es obligatoria.
- Regla2: un lanzamiento `suspendido` no acepta nuevas reservas.
- Regla3: no se permite quitar o cambiar `causaSuspension` sin registrar evento de auditoría.
- Regla4: un lanzamiento `cerrado` no puede volver a `suspendido`.

**Persistencia**:
- Tabla relacional `lanzamientos` (campos de suspensión y timestamps).
- Indices por `estado` y `causaSuspension` para monitoreo operativo.
- Integridad referencial con `reservas.lanzamientoId`.

### Back

API REST propuesta:
- `PATCH /api/lanzamientos/{id}/estado`: transición de estado con validación de reglas.
- `GET /api/lanzamientos/{id}`: incluye detalle de suspensión cuando aplica.
- `GET /api/lanzamientos`: soporta filtros por `estado` y `causaSuspension`.

Reglas de negocio backend:
- Exigir `causaSuspension` válida al solicitar `estado=suspendido`.
- Al confirmar suspensión, denegar de forma inmediata nuevas operaciones de `POST /api/reservas`.
- Registrar evento de dominio `lanzamiento_suspendido` con `causa`, `timestamp`, `actor`.
- Mantener idempotencia: repetir la misma solicitud de suspensión sobre un lanzamiento ya suspendido devuelve respuesta consistente sin duplicar efectos.

Observabilidad:
- Log estructurado por transición de estado y causa.
- Correlation ID entre petición UI, API y operación en base de datos.

### Front

Backoffice interno:
- Acción de "Suspender lanzamiento" en pantalla de detalle.
- Modal obligatorio para seleccionar causa (`económica`, `técnica`, `climática`) y confirmar.
- Indicador visual de lanzamiento suspendido y bloqueo de acciones de reserva.

Flujos:
- Suspender lanzamiento con confirmación explícita.
- Ver causa y fecha de suspensión en listado/detalle.
- Recibir feedback claro cuando se intenta reservar sobre lanzamiento suspendido.

Estados UI:
- `idle`, `loading`, `success`, `error-validacion`, `error-negocio`.

---

## 3. Verificación

- [ ] el sistema DEBE permitir cambiar un lanzamiento a `suspendido` solo si la `causaSuspension` es válida (`economica|tecnica|climatica`).
- [ ] CUANDO un lanzamiento se suspende el sistema DEBE persistir causa, timestamp y actor de la operación.
- [ ] SI se solicita `estado=suspendido` sin causa ENTONCES el sistema DEBE rechazar la operación con error de validación.
- [ ] CUANDO un lanzamiento queda suspendido el sistema DEBE bloquear nuevas reservas para ese lanzamiento.
- [ ] SI el lanzamiento está `cerrado` ENTONCES el sistema DEBE impedir transición a `suspendido`.
- [ ] CUANDO se consulta detalle/listado de lanzamientos el sistema DEBE reflejar estado y causa de suspensión de forma consistente.

### Trazabilidad

- Requerimiento origen PRD: `FR4 — Suspender lanzamientos con causa`.
- Requerimientos técnicos aplicados: `TR1`, `TR3`, `TR4`, `TR6`.

### Suposiciones

- El operador interno que suspende se identifica por un campo simple (`suspendidoPor`) en el MVP.
- El bloqueo de nuevas reservas debe ser inmediato a nivel de backend, independientemente del estado de la UI.

### Preguntas abiertas

- Confirmar si se permite revertir una suspensión (`suspendido -> confirmado`) bajo aprobación operativa en versiones futuras.

---

> Fin de Spec · FR4 · 2026-04-26
