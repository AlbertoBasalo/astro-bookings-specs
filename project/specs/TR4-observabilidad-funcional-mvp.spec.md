# TR4-observabilidad-funcional-mvp

## 1. Problema

Trazabilidad funcional de eventos clave del sistema.

### Contexto

El PRD pide logs estructurados para alta/modificación de lanzamiento, reservas, suspensión, cobro y devolución.

### Historias de usuario

- Como `operador` quiero **rastro de eventos clave** para _auditar qué ocurrió y cuándo_.
- Como `equipo técnico` quiero **logs estructurados** para _diagnosticar incidencias sin inspección manual extensa_.
- Como `equipo del taller` quiero **trazas legibles** para _demostrar comportamiento extremo a extremo_.

### Fuera de scope

- Plataforma enterprise de observabilidad completa.
- Dashboards avanzados con alertado complejo.
- Retención histórica de largo plazo.

---

## 2. Solución

Estandarizar eventos de dominio y formato de log en operaciones críticas del MVP.

### Modelo

#### EventoOperacion
- tipo: `string`
- entidad: `string`
- entidadId: `string`
- timestamp: `datetime`
- correlationId: `string`
- resultado: `string`

**Reglas**:
- Regla1: toda operación crítica debe emitir evento con `correlationId`.
- Regla2: el formato de log debe ser consistente y parseable.

### Back

- Emisión de eventos para: alta/edición de cohete, alta/edición/suspensión de lanzamiento, creación/estado de reserva, cobro y devolución.
- Logging JSON o estructura equivalente.

### Front

- Mostrar mensajes de resultado alineados con eventos de backend.

---

## 3. Verificación

- [ ] el sistema DEBE registrar eventos estructurados para todos los flujos críticos definidos.
- [ ] CUANDO una operación falla el sistema DEBE registrar evento con resultado de error y contexto mínimo.
- [ ] SI se inspeccionan logs por `correlationId` ENTONCES el sistema DEBE permitir reconstruir el flujo principal.
- [ ] CUANDO se ejecuta una demo end-to-end el sistema DEBE evidenciar trazas de cada paso clave.

---

> Fin de Spec · TR4 · 2026-04-26
