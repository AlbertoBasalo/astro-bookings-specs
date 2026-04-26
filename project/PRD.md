# AstroBookings — Requerimientos

## 1. Requerimientos Funcionales

### FR1 — Gestionar cohetes y su rango de acción
El sistema debe permitir alta, consulta y actualización de cohetes, incluyendo su capacidad total y rango operativo (Tierra, Luna o Marte), para asegurar que los lanzamientos usen vehículos compatibles con su destino.

### FR2 — Planificar lanzamientos con parámetros comerciales y operativos
El sistema debe permitir crear y gestionar lanzamientos asociados a un cohete, fecha/hora, destino, precio por asiento y umbral mínimo de ocupación para soportar decisiones operativas y financieras.

### FR3 — Registrar reservas sin exceder capacidad
El sistema debe registrar reservas por lanzamiento validando capacidad disponible en tiempo real, impidiendo sobreventa y manteniendo trazabilidad del estado de cada reserva.

### FR4 — Suspender lanzamientos con causa
El sistema debe permitir suspender un lanzamiento indicando causa estandarizada (económica, técnica o climática) y cambiando su estado para bloquear nuevas reservas.

### FR5 — Ejecutar cobros y devoluciones con pasarela ficticia
El sistema debe registrar el cobro de reservas confirmadas y, si el lanzamiento se suspende, iniciar y registrar devoluciones completas mediante una pasarela de pago ficticia.

---

## 2. Requerimientos Tecnicos

### TR1 — Seguridad
Para el MVP no se requiere autenticación ni autorización compleja. Debe mantenerse al menos validación de entrada, manejo seguro de errores y no exposición de datos sensibles en logs.

### TR2 — Rendimiento
Las operaciones críticas de consulta y reserva deben responder en tiempos adecuados para operación interna (objetivo inicial: respuesta interactiva en segundos, no procesamiento batch pesado).

### TR3 — Confiabilidad
El sistema debe proteger invariantes de negocio (no sobrecapacidad, no doble estado invalido), manejar fallos de pasarela ficticia con reintentos controlados y mantener consistencia de estados.

### TR4 — Observabilidad
Debe existir trazabilidad de eventos clave: alta/modificación de lanzamiento, creación/cancelación de reserva, suspensión, cobro y devolución, con logs estructurados para auditoría funcional.

### TR5 — Integraciones
La única integración externa en esta fase es la pasarela de pago ficticia. El contrato de integración debe abstraerse para permitir reemplazo futuro por proveedor real sin reescribir reglas de dominio.

### TR6 — Persistencia
El sistema debe persistir los datos en una base de datos relacional para garantizar integridad y trazabilidad de eventos.

---

## 3. Dominio del problema

### 3.1. Entidades y lenguaje ubicuo

- `Cohete`: vehículo con capacidad máxima y rango de acción permitido.
- `Lanzamiento`: viaje planificado con destino, cohete, precio por asiento, umbral mínimo y estado.
- `Reserva`: solicitud de asiento vinculada a un lanzamiento con estado transaccional.
- `Pago`: registro de cobro asociado a una reserva.
- `Devolución`: operación de reembolso por suspensión de lanzamiento.

### 3.2. Reglas de Negocio

- Un cohete no puede tener más de 10 asientos.
- No se puede confirmar una reserva si supera la capacidad del cohete asignado al lanzamiento.
- Un lanzamiento suspendido no admite nuevas reservas y debe conservar causa de suspension.
- Si ocupación confirmada < umbral mínimo en decision operativa, el lanzamiento puede suspenderse por motivo económico.
- Ante suspensión, las reservas cobradas deben pasar a flujo de devolución.
- Estados de lanzamiento sugeridos: `programado` -> `confirmado` o `suspendido` -> `cerrado`.
- Estados de reserva sugeridos: `pendiente` -> `confirmada` -> (`cobrada` | `cancelada`) -> `devuelta` cuando aplique.

---

> Fin del PRD · AstroBookings · v0.1 · 2026-04-26
