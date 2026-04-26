# TR1-seguridad-mvp

## 1. Problema

Seguridad mínima para MVP sin autenticación avanzada.

### Contexto

El PRD indica que en esta fase no se requiere auth compleja, pero sí controles básicos para evitar entradas inválidas, errores inseguros y exposición de datos sensibles en logs.

### Historias de usuario

- Como `equipo interno` quiero **validación de entrada homogénea** para _evitar datos corruptos y fallos de negocio_.
- Como `equipo interno` quiero **errores controlados** para _operar sin filtrar detalles técnicos innecesarios_.
- Como `equipo técnico` quiero **logs sin datos sensibles** para _mantener trazabilidad segura en demo y evolución_.

### Fuera de scope

- Autenticación de usuarios y gestión de sesiones.
- Autorización por roles/permisos granulares.
- Cifrado avanzado de datos en reposo.

---

## 2. Solución

Definir una capa transversal de validación y manejo de errores para todas las APIs del MVP.

### Modelo

#### ErrorSeguro
- code: `string`
- message: `string`
- correlationId: `string`

**Reglas**:
- Regla1: toda entrada de API debe validarse antes de ejecutar reglas de dominio.
- Regla2: errores de validación/negocio no deben incluir stacktrace en respuesta.
- Regla3: logs deben omitir datos sensibles (documento completo, referencias de pago completas).

### Back

- Middleware de validación por endpoint.
- Middleware global de errores con mapeo HTTP consistente.
- Sanitización de campos sensibles antes de loguear.

### Front

- Mostrar mensajes de error funcionales y claros.
- No exponer errores técnicos crudos al operador.

---

## 3. Verificación

- [ ] el sistema DEBE rechazar entradas inválidas con errores de validación consistentes.
- [ ] CUANDO ocurre una excepción el sistema DEBE responder sin stacktrace ni detalle sensible.
- [ ] SI un evento genera log ENTONCES el sistema DEBE ocultar datos sensibles configurados.
- [ ] CUANDO el front recibe error de backend el sistema DEBE mostrar mensaje operativo entendible.

---

> Fin de Spec · TR1 · 2026-04-26
