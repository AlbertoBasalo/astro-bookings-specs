# AstroBookings

Sistema MVP para gestionar reservas y operaciones de turismo espacial interno.

## 1. Idea

### 1.1 Problema o necesidad
Una empresa ficticia de turismo espacial necesita coordinar cohetes, lanzamientos y reservas sin sobrepasar capacidad ni perder control operativo ante cancelaciones. Sin un sistema unificado, aumenta el riesgo de sobreventa, decisiones tardías de suspensión y mala gestión de cobros/devoluciones.

### 1.2 Misión u objetivo
Definir y validar en 12 semanas un MVP interno que permita: gestionar cohetes y lanzamientos, registrar reservas con control de capacidad, decidir continuidad de lanzamientos por umbral mínimo de ocupación y ejecutar devoluciones cuando un lanzamiento se suspenda.

### 1.3 Publico objetivo
- Equipo interno de operaciones de vuelos espaciales.
- Equipo administrativo que gestiona reservas y estados de lanzamiento.
- Equipo financiero/operativo que supervisa cobros y devoluciones.

---

## 2. Alcance

### 2.1 Que se incluye
- Gestión de cohetes con rango operativo (Tierra, Luna o Marte).
- Planificación de lanzamientos con precio por asiento y umbral mínimo de ocupación.
- Registro de reservas con validación de capacidad disponible.
- Suspensión de lanzamientos con causa explicita (económica, técnica o climática).
- Flujo de cobro y devolución mediante pasarela de pago ficticia.
- API REST y aplicación web interna para operación diaria.

### 2.2 Que se excluye
- Autenticación, autorización avanzada y seguridad de producción en esta fase.
- Integración con pasarelas de pago reales.
- Experiencia de cliente final público (solo uso interno).
- Optimizaciones de escalado empresarial y alta disponibilidad multi-region.

### 2.3 Limitaciones y notas
- Suposiciones: el volumen inicial es de entrenamiento/demo, no carga real de producción.
- Dependencias externas: servicio ficticio de pagos para simular cobros y devoluciones.
- Advertencias: las reglas de negocio de suspensión dependen de calidad de datos de ocupación.
- Solución técnica recomendada/esperada: backend API REST + frontend web interno con modelo de dominio centrado en cohetes, lanzamientos y reservas.

---

> Fin del Brief · AstroBookings · 2026-04-26
