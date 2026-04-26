# FR3-registrar-reservas-sin-exceder-capacidad

## 1. Problema

Registrar reservas sin exceder capacidad.

### Contexto

El PRD exige registrar reservas por lanzamiento validando capacidad disponible en tiempo real para impedir sobreventa y mantener trazabilidad de estado. Este flujo protege el ingreso y la confianza operativa, ya que una reserva inválida impacta cobros, devoluciones y experiencia del equipo interno.

### Historias de usuario

- Como `operador` quiero **crear una reserva asociada a un lanzamiento disponible** para _asignar asientos de forma confiable_.
- Como `operador` quiero **confirmar que hay capacidad antes de guardar la reserva** para _evitar sobreventa y conflictos posteriores_.
- Como `operador` quiero **consultar y actualizar el estado transaccional de una reserva** para _mantener trazabilidad del ciclo operativo_.

### Fuera de scope

- Selección de asiento específico dentro del cohete.
- Gestión de listas de espera automáticas.
- Gestión de identidad avanzada de pasajeros y documentación de viaje.

---

## 2. Solución

Se define un módulo de reservas con control transaccional de capacidad por lanzamiento y máquina de estados explícita. La reserva solo se confirma si hay cupo disponible en el momento de la operación; además, la solución conserva historial de cambios para auditoría y soporte de cobros/devoluciones en fases posteriores.

### Modelo

#### Reserva
- id: `uuid`, identificador único.
- lanzamientoId: `uuid`, referencia al lanzamiento.
- pasajeroNombre: `string`, nombre visible de operación.
- pasajeroDocumento: `string`, identificador operativo básico.
- estado: `enum`, valores `pendiente | confirmada | cobrada | cancelada | devuelta`.
- precioSnapshot: `number`, precio por asiento capturado al momento de confirmar.
- creadaEn: `datetime`, timestamp de creación.
- actualizadaEn: `datetime`, timestamp de último cambio.

**Reglas**:
- Regla1: no se puede crear reserva para lanzamientos `suspendido` o `cerrado`.
- Regla2: la confirmación de reserva requiere capacidad disponible (`confirmadas + cobradas < capacidadMaxima`).
- Regla3: la validación de capacidad debe ejecutarse de forma transaccional para evitar carreras concurrentes.
- Regla4: las transiciones de estado deben respetar el flujo `pendiente -> confirmada -> (cobrada | cancelada) -> devuelta`.
- Regla5: al confirmar, `precioSnapshot` captura el precio vigente del lanzamiento y no cambia después.

**Persistencia**:
- Tabla relacional `reservas`.
- Indices por `lanzamientoId`, `estado` y `pasajeroDocumento` para operación y auditoría.
- Integridad referencial con `lanzamientos.id`.

### Back

API REST propuesta:
- `POST /api/reservas`: crea reserva y valida capacidad/estado de lanzamiento.
- `GET /api/reservas`: lista reservas con filtros por `lanzamientoId`, `estado`, `pasajeroDocumento`.
- `GET /api/reservas/{id}`: obtiene detalle y estado actual.
- `PATCH /api/reservas/{id}/estado`: actualiza estado con validación de transición.

Reglas de negocio backend:
- Bloquear creación cuando el lanzamiento no admite reservas.
- Ejecutar confirmación con lock transaccional sobre el lanzamiento para impedir sobreventa en concurrencia.
- Rechazar transiciones de estado inválidas con error funcional.
- Registrar eventos de dominio: `reserva_creada`, `reserva_confirmada`, `reserva_cancelada`, `reserva_devuelta`.

Observabilidad:
- Log estructurado por operación y por cambio de estado de reserva.
- Correlación por `correlationId` para trazar desde UI hasta persistencia.

### Front

Backoffice interno:
- Formulario de alta de reserva desde detalle de lanzamiento.
- Lista de reservas por lanzamiento con contador de ocupación confirmada.
- Vista de detalle con estado actual e historial de cambios.

Flujos:
- Crear reserva y recibir respuesta inmediata de cupo.
- Gestionar transición de estado permitida según ciclo de vida.
- Mostrar bloqueos por capacidad completa o lanzamiento no reservable.

Estados UI:
- `idle`, `loading`, `success`, `error-validacion`, `error-capacidad`, `error-negocio`.

---

## 3. Verificación

- [ ] el sistema DEBE registrar una reserva para un lanzamiento `programado` o `confirmado` solo si existe capacidad disponible.
- [ ] CUANDO dos solicitudes concurrentes intentan reservar el último cupo el sistema DEBE confirmar solo una y rechazar la otra sin sobrepasar `capacidadMaxima`.
- [ ] SI el lanzamiento está `suspendido` o `cerrado` ENTONCES el sistema DEBE rechazar nuevas reservas con error funcional.
- [ ] CUANDO una reserva pasa a `confirmada` el sistema DEBE persistir `precioSnapshot` con el precio vigente del lanzamiento.
- [ ] SI se intenta una transición de estado fuera del flujo permitido ENTONCES el sistema DEBE bloquearla y mantener estado previo.
- [ ] CUANDO se consulta reservas por `lanzamientoId` y `estado` el sistema DEBE devolver resultados consistentes con la persistencia y la ocupación calculada.

### Trazabilidad

- Requerimiento origen PRD: `FR3 — Registrar reservas sin exceder capacidad`.
- Requerimientos técnicos aplicados: `TR1`, `TR2`, `TR3`, `TR4`, `TR6`.

### Suposiciones

- El registro de pasajero en MVP requiere solo nombre y documento para trazabilidad interna.
- La reserva nace en estado `pendiente` y se confirma dentro de la misma operación cuando hay capacidad.

### Preguntas abiertas

- Confirmar si debe existir timeout automático para reservas `pendiente` no cobradas en una ventana temporal definida.

---

> Fin de Spec · FR3 · 2026-04-26
