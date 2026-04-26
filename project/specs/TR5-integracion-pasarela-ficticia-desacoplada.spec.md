# TR5-integracion-pasarela-ficticia-desacoplada

## 1. Problema

Integrar pasarela ficticia sin acoplar reglas de dominio al proveedor.

### Contexto

El PRD define una única integración externa (pasarela ficticia) y exige abstraer su contrato para reemplazo futuro por un proveedor real.

### Historias de usuario

- Como `equipo técnico` quiero **un contrato de integración abstracto** para _sustituir proveedor sin reescribir dominio_.
- Como `operador` quiero **cobros/devoluciones consistentes** para _operar sin depender de detalles del proveedor_.
- Como `equipo del taller` quiero **simular resultados de pasarela** para _validar flujos de éxito y fallo_.

### Fuera de scope

- Soporte multi-proveedor en paralelo.
- Integraciones reales con certificación externa.
- Reconciliación financiera compleja.

---

## 2. Solución

Implementar un adaptador de pasarela con interfaz estable para cobro y devolución, aislando la lógica de negocio.

### Modelo

#### PaymentGateway
- cobrar(payload): `resultado`
- devolver(payload): `resultado`

**Reglas**:
- Regla1: dominio usa solo la interfaz, nunca detalles internos del proveedor.
- Regla2: respuestas de pasarela se normalizan a estados de negocio.

### Back

- Adapter `pasarela-ficticia` detrás de interfaz `PaymentGateway`.
- Mapeo de errores técnicos a errores operativos controlados.
- Trazabilidad de request/response con sanitización.

### Front

- No depende de contrato externo; consume solo estados de negocio del backend.

---

## 3. Verificación

- [ ] el sistema DEBE procesar cobro/devolución usando interfaz desacoplada del proveedor.
- [ ] CUANDO cambie la implementación de pasarela el sistema DEBE mantener reglas de negocio sin cambios mayores.
- [ ] SI la pasarela devuelve error técnico ENTONCES el sistema DEBE mapearlo a respuesta funcional controlada.
- [ ] CUANDO se ejecutan pruebas de integración de demo el sistema DEBE cubrir escenarios de éxito y fallo.

---

> Fin de Spec · TR5 · 2026-04-26
