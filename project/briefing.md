# AstroBookings

**Idea**  
Aplicación interna para que AstroBookings gestione su flota, lanzamientos y reservas de turismo espacial de forma simple y operativa.

**Problema**  
AstroBookings necesita coordinar operaciones comerciales y de vuelo sin perder control de capacidad ni estado de cada lanzamiento.

Opera una flota de cohetes con distinto alcance y número de plazas, lo que exige planificación precisa para evitar sobreventa.  
Cada lanzamiento tiene viabilidad económica y puede suspenderse o cancelarse por causas de negocio o técnicas.  
Además, necesita registrar cobros y devoluciones en modo demostración, sin integrar pasarelas reales.

**Misión**  
Demostrar, en contexto formativo, una solución rápida de gestión end-to-end para lanzamientos y reservas, asegurando control de capacidad y operación diaria.

**Usuarios**
- Operaciones de vuelos (planifican lanzamientos y actualizan su estado)
- Gestión de reservas (crean y administran reservas sin overbooking)
- Administración/finanzas (registran pagos y devoluciones simuladas)
    
**Qué hace**
- Gestiona flota de cohetes con capacidades y alcance.
- Planifica lanzamientos y su evolución operativa.
- Registra reservas controlando disponibilidad para evitar overbooking.
- Gestiona el estado de los lanzamientos: 
    - programado → confirmado → exitoso 
    - suspendido por baja ocupación 
    - cancelado por causas técnicas o externas
- Registra pagos y devoluciones con pasarela fake para fines demo.
**No incluye**
- Integración con pasarelas de pago reales (solo simulación).
- Reglas avanzadas de seguridad, fraude o cumplimiento financiero.
- Operación productiva 24/7 (proyecto de demo).

**Notas**
- Proyecto en modo hackathon: alcance acotado, implementación simple y rápida.
- Caso de uso educativo para cursos y talleres; no orientado a producción.
- Solución esperada: API REST + aplicación web interna para empleados.
