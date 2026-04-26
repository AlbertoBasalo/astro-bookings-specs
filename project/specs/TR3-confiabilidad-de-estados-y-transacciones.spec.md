# TR3-confiabilidad-de-estados-y-transacciones

## 1. Problema

Proteger invariantes del dominio y consistencia transaccional.

### Contexto

El PRD exige no sobrecapacidad, no estados inválidos y manejo de fallos de pasarela ficticia con reintentos controlados.

### Historias de usuario

- Como `operador` quiero **evitar sobreventa** para _no generar reservas inválidas_.
- Como `operador` quiero **transiciones de estado válidas** para _preservar trazabilidad funcional_.
- Como `equipo técnico` quiero **reintentos controlados** para _mitigar fallos transitorios de pago/devolución_.

### Fuera de scope

- Orquestación distribuida compleja.
- Saga multi-servicio real.
- Recuperación automática avanzada ante desastre.

---

## 2. Solución

Aplicar reglas de consistencia en backend con validación de transiciones y transacciones atómicas en operaciones críticas.

### Modelo

#### InvarianteDominio
- nombre: `string`
- regla: `string`

**Reglas**:
- Regla1: nunca confirmar reservas por encima de capacidad.
- Regla2: solo transiciones de estado permitidas en lanzamiento/reserva.
- Regla3: reintentos de pasarela con límite definido y registro de resultado final.

### Back

- Locks transaccionales en confirmación de reserva.
- Validadores de máquina de estados.
- Estrategia de reintentos (máximo N intentos) para errores transitorios.

### Front

- Mensajes claros cuando una transición o reserva es rechazada por regla de consistencia.

---

## 3. Verificación

- [ ] el sistema DEBE impedir sobrecapacidad bajo concurrencia.
- [ ] CUANDO se intenta una transición inválida el sistema DEBE rechazarla sin alterar estado previo.
- [ ] SI la pasarela falla de forma transitoria ENTONCES el sistema DEBE ejecutar reintentos dentro del límite configurado.
- [ ] CUANDO finaliza una operación crítica el sistema DEBE dejar trazabilidad de éxito o fallo final.

---

> Fin de Spec · TR3 · 2026-04-26
