# FR2-planificar-lanzamientos-con-parametros-comerciales-y-operativos

## 1. Problema

Planificar lanzamientos con parámetros comerciales y operativos.

### Contexto

El PRD define que AstroBookings debe permitir crear y gestionar lanzamientos con cohete, fecha/hora, destino, precio por asiento y umbral mínimo de ocupación. Sin esta capacidad, no existe una unidad operativa sobre la que reservar, cobrar o suspender, y no se pueden tomar decisiones financieras antes de la ejecución.

### Historias de usuario

- Como `operador` quiero **crear un lanzamiento con cohete, fecha/hora y destino** para _publicar una oferta operativa válida para reservas_.
- Como `operador` quiero **definir precio por asiento y umbral mínimo de ocupación** para _controlar viabilidad comercial del lanzamiento_.
- Como `operador` quiero **actualizar la planificación de un lanzamiento programado** para _ajustar operación ante cambios sin perder trazabilidad_.

### Fuera de scope

- Optimización automática de precios según demanda.
- Planificación multi-tramo o itinerarios con escalas.
- Integración con proveedores externos de calendario o slot aeroportuario espacial.

---

## 2. Solución

Se incorpora el módulo de lanzamientos como entidad central de planificación, vinculada obligatoriamente a un cohete activo y compatible con el destino. La solución cubre alta, consulta, actualización y cambios de estado controlados en API REST y app interna, con reglas que preservan consistencia operativa y financiera del MVP.

### Modelo

#### Lanzamiento
- id: `uuid`, identificador único.
- coheteId: `uuid`, referencia al cohete asignado.
- fechaHoraSalida: `datetime`, fecha/hora programada.
- destino: `enum`, valores permitidos `Tierra | Luna | Marte`.
- precioAsiento: `number`, valor monetario por asiento.
- umbralMinimoOcupacion: `number`, porcentaje mínimo requerido para decisión operativa.
- estado: `enum`, valores `programado | confirmado | suspendido | cerrado`.
- causaSuspension: `enum|null`, valores `economica | tecnica | climatica` cuando aplique.
- creadoEn: `datetime`, timestamp de alta.
- actualizadoEn: `datetime`, timestamp de última modificación.

**Reglas**:
- Regla1: `coheteId` debe existir y estar `activo=true`.
- Regla2: el `destino` del lanzamiento debe ser compatible con `rangoAccion` del cohete.
- Regla3: `precioAsiento` debe ser mayor que 0.
- Regla4: `umbralMinimoOcupacion` debe estar entre 1 y 100.
- Regla5: solo se permite editar campos operativos/comerciales mientras `estado=programado`.
- Regla6: `causaSuspension` es obligatoria al pasar a `suspendido`.

**Persistencia**:
- Tabla relacional `lanzamientos`.
- Indices por `estado`, `fechaHoraSalida` y `destino` para operación diaria.
- Integridad referencial con `cohetes.id`.

### Back

API REST propuesta:
- `POST /api/lanzamientos`: crea lanzamiento con validaciones de dominio.
- `GET /api/lanzamientos`: lista lanzamientos con filtros por `estado`, `destino`, `coheteId`, rango de fechas.
- `GET /api/lanzamientos/{id}`: obtiene detalle operativo y comercial.
- `PATCH /api/lanzamientos/{id}`: actualiza campos permitidos cuando `estado=programado`.
- `PATCH /api/lanzamientos/{id}/estado`: cambia estado aplicando guardas de transición.

Reglas de negocio backend:
- Rechazar creación/actualización si el cohete no existe o está inactivo.
- Rechazar incompatibilidad entre `destino` y `rangoAccion`.
- Evitar transiciones inválidas de estado (por ejemplo `cerrado` a `programado`).
- Exigir `causaSuspension` al suspender y bloquear nuevas reservas desde ese estado.

Observabilidad:
- Log estructurado en alta, edición de precio/umbral, y transición de estado.
- Traza con `correlationId` para auditoría funcional entre UI, API y persistencia.

### Front

Backoffice interno:
- Pantalla de listado de lanzamientos con filtros por fecha, estado, destino y cohete.
- Formulario de creación/edición con validaciones inmediatas de precio, umbral y compatibilidad destino-cohete.
- Vista de detalle con timeline de cambios de estado.

Flujos:
- Crear lanzamiento programado con feedback de validación.
- Editar parámetros comerciales/operativos mientras esté programado.
- Suspender o confirmar lanzamiento con control de reglas.

Estados UI:
- `idle`, `loading`, `success`, `error-validacion`, `error-negocio`.

---

## 3. Verificación

- [ ] el sistema DEBE permitir crear un lanzamiento con `coheteId`, `fechaHoraSalida`, `destino`, `precioAsiento` y `umbralMinimoOcupacion` válidos, iniciando en estado `programado`.
- [ ] CUANDO se crea o actualiza un lanzamiento el sistema DEBE validar compatibilidad entre `destino` y `rangoAccion` del cohete antes de persistir.
- [ ] SI `precioAsiento <= 0` o `umbralMinimoOcupacion` está fuera de `1..100` ENTONCES el sistema DEBE rechazar la operación con error de validación.
- [ ] CUANDO se intenta editar un lanzamiento en estado distinto de `programado` el sistema DEBE bloquear la actualización de parámetros comerciales y operativos.
- [ ] SI se cambia estado a `suspendido` sin `causaSuspension` ENTONCES el sistema DEBE rechazar la transición con error funcional.
- [ ] CUANDO se lista lanzamientos con filtros por estado, destino y rango de fechas el sistema DEBE responder resultados consistentes con persistencia.

### Trazabilidad

- Requerimiento origen PRD: `FR2 — Planificar lanzamientos con parámetros comerciales y operativos`.
- Requerimientos técnicos aplicados: `TR1`, `TR3`, `TR4`, `TR6`.

### Suposiciones

- El umbral mínimo se modela como porcentaje entero de ocupación (`1..100`) para facilitar reglas del MVP.
- La compatibilidad destino-cohete se evalúa con el `rangoAccion` definido en FR1.

### Preguntas abiertas

- Confirmar si debe permitirse reprogramar `fechaHoraSalida` cuando ya existen reservas en estado `pendiente`.

---

> Fin de Spec · FR2 · 2026-04-26
