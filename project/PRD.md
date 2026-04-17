# AstroBookings — Requerimientos

## 1. Requerimientos Funcionales

### FR1 — Gestión de cohetes
El sistema permite registrar cohetes con nombre, capacidad máxima de pasajeros y rango de destinos operables. Un cohete no puede asignarse a un lanzamiento si su rango no cubre el destino indicado.

### FR2 — Gestión de lanzamientos
El sistema permite definir lanzamientos con cohete asignado, destino, fecha, precio por asiento y ocupación mínima requerida. Un lanzamiento no puede tener más reservas que la capacidad del cohete asignado.

### FR3 — Gestión de clientes
El sistema identifica a los clientes por su dirección de correo electrónico. No se requiere autenticación; el registro es implícito al realizar la primera reserva.

### FR4 — Gestión de reservas
El sistema permite a los operadores registrar reservas de plazas para un lanzamiento. La disponibilidad se actualiza automáticamente y no se permite la sobre-venta. Una reserva queda vinculada a un cliente y a un lanzamiento.

### FR5 — Ciclo de vida de los lanzamientos
El sistema gestiona los estados de un lanzamiento de forma unidireccional:
- **programado** → **confirmado** (cuando se alcanza la ocupación mínima)
- **confirmado** → **exitoso** (tras el lanzamiento)
- **programado** → **suspendido** (si no se alcanza la ocupación mínima antes de la fecha)
- **cualquier estado activo** → **cancelado** (por causas técnicas o externas)

### FR6 — Cancelaciones y devoluciones simuladas
El sistema permite cancelar lanzamientos indicando el motivo. Al cancelar, todas las reservas asociadas cambian a estado cancelado y se registra una devolución simulada por cada una de ellas, sin integración real con pasarelas de pago.

---

## 2. Requerimientos Técnicos

### TR1 — Seguridad
Sin autenticación ni autorización: el sistema es de uso interno exclusivo para operadores. No se gestionan datos sensibles más allá del email del cliente.

### TR2 — Persistencia
Los datos se mantienen en memoria durante la ejecución. No se requiere base de datos ni almacenamiento persistente; es un entorno de demostración.

### TR3 — Integración de pagos
Los pagos y devoluciones son simulados. El sistema registra la intención de cobro o devolución sin conectarse a ningún servicio externo real.

### TR4 — Confiabilidad
El sistema debe rechazar operaciones que violen las reglas de negocio (sobre-venta, transiciones de estado inválidas) devolviendo errores descriptivos al operador.

### TR5 — Arquitectura
El sistema se implementa como una API REST para la lógica de negocio y una Aplicación Web para la interfaz del operador.

---

## 3. Reglas de Negocio

- El número de reservas confirmadas de un lanzamiento no puede superar la capacidad del cohete asignado.
- Un lanzamiento solo puede confirmarse si el número de reservas alcanza o supera la ocupación mínima definida.
- Las transiciones de estado de un lanzamiento son unidireccionales; no se puede revertir un estado.
- Un cohete no puede asignarse a un lanzamiento si su rango no incluye el destino del lanzamiento.
- La cancelación de un lanzamiento implica la cancelación automática de todas sus reservas y la generación de devoluciones simuladas.
- Cada reserva está vinculada a exactamente un cliente (identificado por email) y a exactamente un lanzamiento.

---

## 4. Factores Arquitectónicos

- **Sin persistencia**: los datos en memoria simplifican el despliegue y priorizan la validación de lógica de negocio.
- **API REST**: separa la lógica de negocio de la interfaz; facilita pruebas automatizadas y extensión futura.
- **Aplicación Web**: interfaz para operadores sobre la API REST; no requiere diseño orientado al consumidor final.
- **Proyecto de formación**: la simplicidad y la legibilidad del código tienen mayor peso que la escalabilidad o la resiliencia en producción.
- **Simulación de pagos**: desacopla el dominio de reservas de integraciones externas, manteniendo el foco en las reglas de negocio.
