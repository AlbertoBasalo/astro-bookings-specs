# FR5-ejecutar-cobros-y-devoluciones-con-pasarela-ficticia

## 1. Problema

Ejecutar cobros y devoluciones con pasarela ficticia.

### Contexto

El PRD establece que las reservas confirmadas deben poder cobrarse y que, ante suspensión de lanzamiento, deben ejecutarse devoluciones completas mediante una pasarela ficticia. Sin este flujo no se puede cerrar el circuito comercial del MVP ni validar consistencia entre estados operativos y transaccionales.

### Historias de usuario

- Como `operador` quiero **cobrar una reserva confirmada** para _materializar el ingreso del lanzamiento_.
- Como `operador` quiero **iniciar devoluciones completas cuando un lanzamiento se suspende** para _cumplir la política comercial y evitar incidencias_.
- Como `operador` quiero **consultar estado de cobros y devoluciones** para _auditar cada transacción y resolver fallos_.

### Fuera de scope

- Soporte a pagos parciales o en cuotas.
- Integración con proveedores reales de pago.
- Gestión fiscal/contable avanzada (impuestos, conciliación bancaria).

---

## 2. Solución

Se incorpora una capa de pagos desacoplada del dominio de reservas mediante un contrato de pasarela (`gateway`) ficticia. El sistema registra cobros para reservas confirmadas y ejecuta devoluciones completas al suspender un lanzamiento, manteniendo trazabilidad de intento, resultado y reintentos controlados.

### Modelo

#### Pago
- id: `uuid`, identificador único.
- reservaId: `uuid`, referencia a la reserva.
- monto: `number`, importe total cobrado.
- estado: `enum`, valores `iniciado | aprobado | rechazado`.
- referenciaExterna: `string|null`, id devuelto por la pasarela ficticia.
- creadoEn: `datetime`, timestamp de creación.
- actualizadoEn: `datetime`, timestamp de último cambio.

#### Devolucion
- id: `uuid`, identificador único.
- pagoId: `uuid`, referencia al pago aprobado.
- monto: `number`, importe devuelto (100% en MVP).
- estado: `enum`, valores `iniciada | aprobada | rechazada`.
- referenciaExterna: `string|null`, id de operación en pasarela.
- creadaEn: `datetime`, timestamp de creación.
- actualizadaEn: `datetime`, timestamp de último cambio.

**Reglas**:
- Regla1: solo reservas `confirmada` pueden iniciar cobro.
- Regla2: al aprobar cobro, la reserva pasa a `cobrada`.
- Regla3: ante lanzamiento `suspendido`, toda reserva `cobrada` debe iniciar devolución completa.
- Regla4: no se permite más de una devolución aprobada por pago.
- Regla5: los fallos de pasarela ficticia se gestionan con reintentos controlados.

**Persistencia**:
- Tablas relacionales `pagos` y `devoluciones`.
- Indices por `reservaId`, `pagoId` y `estado` para operación.
- Integridad referencial con `reservas.id` y `pagos.id`.

### Back

API REST propuesta:
- `POST /api/reservas/{id}/cobro`: inicia y registra cobro.
- `POST /api/lanzamientos/{id}/devoluciones`: inicia devoluciones para reservas cobradas del lanzamiento.
- `GET /api/pagos`: lista pagos por `reservaId` y `estado`.
- `GET /api/devoluciones`: lista devoluciones por `pagoId` y `estado`.

Reglas de negocio backend:
- Validar estado de reserva antes de cobrar.
- Encapsular pasarela ficticia detrás de interfaz (`PaymentGateway`) para reemplazo futuro.
- Ejecutar devoluciones idempotentes por pago para evitar doble reembolso.
- Aplicar política de reintentos con límite y registrar resultado final (`aprobada`/`rechazada`).

Observabilidad:
- Eventos de dominio: `cobro_iniciado`, `cobro_aprobado`, `cobro_rechazado`, `devolucion_iniciada`, `devolucion_aprobada`, `devolucion_rechazada`.
- Logs estructurados con `correlationId`, `reservaId`, `pagoId`, `devolucionId`.

### Front

Backoffice interno:
- Acción de cobro sobre reservas confirmadas.
- Vista de estados transaccionales por reserva.
- Flujo de ejecución de devoluciones desde detalle de lanzamiento suspendido.

Flujos:
- Cobrar reserva y reflejar transición de estado.
- Lanzar devoluciones masivas de un lanzamiento suspendido.
- Mostrar errores de pasarela y resultado de reintentos.

Estados UI:
- `idle`, `loading`, `success`, `error-validacion`, `error-pasarela`, `error-negocio`.

---

## 3. Verificación

- [ ] el sistema DEBE permitir cobrar una reserva solo cuando su estado sea `confirmada`.
- [ ] CUANDO un cobro es aprobado el sistema DEBE registrar el pago y actualizar la reserva a estado `cobrada`.
- [ ] SI se intenta cobrar una reserva en estado distinto de `confirmada` ENTONCES el sistema DEBE rechazar la operación con error funcional.
- [ ] CUANDO un lanzamiento se suspende el sistema DEBE iniciar devolución completa para cada reserva `cobrada` asociada.
- [ ] SI la pasarela ficticia falla ENTONCES el sistema DEBE ejecutar reintentos controlados y dejar trazabilidad del resultado final.
- [ ] CUANDO una devolución es aprobada el sistema DEBE evitar una segunda devolución aprobada para el mismo pago.

### Trazabilidad

- Requerimiento origen PRD: `FR5 — Ejecutar cobros y devoluciones con pasarela ficticia`.
- Requerimientos técnicos aplicados: `TR1`, `TR3`, `TR4`, `TR5`, `TR6`.

### Suposiciones

- La devolución MVP es siempre del 100% del monto cobrado.
- El contrato de la pasarela ficticia expone operación síncrona de cobro/devolución con respuesta de estado.

### Preguntas abiertas

- Confirmar política de reintentos (cantidad máxima y ventana temporal) para errores transitorios de pasarela.

---

> Fin de Spec · FR5 · 2026-04-26
