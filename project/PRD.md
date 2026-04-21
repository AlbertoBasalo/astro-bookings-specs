# AstroBookings — Requerimientos

## 1. Requerimientos Funcionales

### FR1 — Gestión de flota operativa
El sistema debe permitir mantener un catálogo de cohetes con su capacidad de plazas y alcance operativo para que Operaciones planifique lanzamientos con recursos válidos y visibles.

### FR2 — Planificación y gestión de lanzamientos
El sistema debe permitir crear y administrar lanzamientos asociados a la flota, con fecha y capacidad disponible, para sostener la operación comercial y de vuelo en una vista unificada.

### FR3 — Control de reservas sin overbooking
El sistema debe permitir registrar y cancelar reservas de plazas por lanzamiento, garantizando en todo momento que la ocupación no exceda la capacidad disponible.

### FR4 — Gestión del ciclo de estados del lanzamiento
El sistema debe gestionar el estado operativo de cada lanzamiento (`programado`, `confirmado`, `exitoso`, `suspendido`, `cancelado`) para reflejar su situación real y habilitar decisiones de negocio consistentes.

### FR5 — Gestión económica de viabilidad por lanzamiento
El sistema debe permitir definir un umbral mínimo de ocupación por lanzamiento y utilizarlo para la decisión de suspensión por baja ocupación, evitando operar vuelos no viables económicamente.

### FR6 — Cobros y devoluciones en modo demo
El sistema debe registrar cobros y devoluciones mediante pasarela simulada, incluyendo devolución automática total de reservas activas cuando un lanzamiento sea cancelado o suspendido.

---

## 2. Requerimientos Técnicos

### TR1 — Seguridad
En esta fase de hackathon, se asume un entorno interno de confianza: los usuarios operan con permisos implícitos y sin autenticación inicial. 

### TR2 — Rendimiento
La solución debe priorizar simplicidad y respuesta ágil para operaciones CRUD internas. No se requieren optimizaciones avanzadas ni objetivos de escalado masivo en esta fase.

### TR3 — Confiabilidad
El sistema debe preservar consistencia de capacidad y estados mediante validaciones transaccionales en operaciones críticas (reserva, cancelación, cambio de estado, devolución).

### TR4 — Observabilidad
Se requiere trazabilidad mínima de cambios críticos: transiciones de estado de lanzamientos y eventos de cobro/devolución, con registro de actor, fecha/hora y resultado.

### TR5 — Integraciones
La única integración externa permitida en esta fase es una pasarela de pago fake. Quedan explícitamente fuera integraciones reales de pago u otros sistemas corporativos.

---

## 3. Dominio del problema

### 3.1. Entidades y lenguaje ubicuo

- `Cohete`: recurso de flota con capacidad máxima de 10 plazas y alcance operativo restringido a Tierra, Luna o Marte.
- `Lanzamiento`: evento planificado de vuelo asociado a un cohete y con estado operativo.
- `Reserva`: asignación de plazas a un cliente sobre un lanzamiento específico.
- `Cliente`: persona registrada para reservas, identificada de forma única por email.
- `Pago`: registro de cobro simulado asociado a una reserva.
- `Devolucion`: registro de reembolso simulado asociado a una reserva y su causa.

### 3.2. Reglas de Negocio

- No se permite overbooking: la suma de plazas reservadas activas nunca puede superar la capacidad del lanzamiento.
- El email del cliente es único en el sistema para evitar duplicidades de identidad en reservas.
- El alcance de reservas en esta fase incluye solo alta y cancelación; no se contemplan modificaciones de plazas ni reubicación.
- La capacidad de un cohete no puede superar 10 plazas.
- El rango de acción permitido para un cohete es exclusivamente `Tierra`, `Luna` o `Marte`.
- El umbral de ocupación mínima es configurable por lanzamiento y condiciona su viabilidad económica.
- Los estados válidos del lanzamiento son `programado`, `confirmado`, `exitoso`, `suspendido`, `cancelado`.
- Ante lanzamiento `suspendido` o `cancelado`, toda reserva activa debe generar devolución total automática en modo demo.
