# AstroBookings

**Idea**  
Sistema para gestionar reservas de viajes espaciales para empresas de turismo orbital.

**Problema**  
Las empresas de turismo espacial necesitan controlar plazas, reservas y estados de lanzamiento sin errores ni sobre-venta.

Operan con cohetes que viajan a destinos como la órbita terrestre, la Luna o Marte, siempre con capacidad limitada.  
Cada lanzamiento debe ser rentable: tiene un precio por asiento y un mínimo de ocupación para no ser suspendido.  
Además, pueden producirse cancelaciones por motivos técnicos o meteorológicos.  
Los pagos y devoluciones se gestionan mediante sistemas externos.

**Usuarios**
- Operadores de la empresa (gestionan flota, lanzamientos y reservas de clientes)
    
**Qué hace**
- Gestiona cohetes con capacidad y alcance limitados.
- Permite definir lanzamientos con precio por asiento y ocupación mínima.
- Gestiona clientes identificados por email.
- Permite reservar plazas y controla la disponibilidad automáticamente.
- Gestiona el estado de los lanzamientos:    
    - programado → confirmado → exitoso        
    - suspendido por baja ocupación        
    - cancelado por causas técnicas o externas
**No incluye**
- Pagos reales (solo simulación)    
- Autenticación (uso interno por operadores)    
- Persistencia (datos en memoria)    

**Valor**  
Permite validar la lógica de negocio de reservas evitando overbooking y errores operativos.

**Notas**
- Proyecto de demo para formación, no pensado para producción.
- Solución recomendada mediante API REST y Aplicación Web.

---

- [Repositorio en GitHub](https://github.com/AlbertoBasalo/astro-bookings)
- Rama por defecto: `main`

- **Autor**: [Alberto Basalo](https://albertobasalo.dev)
- **Ai Code Academy en Español**: [AI code Academy](https://aicode.academy)
- **Redes sociales**:
  - [X](https://x.com/albertobasalo)
  - [LinkedIn](https://www.linkedin.com/in/albertobasalo/)
  - [GitHub](https://github.com/albertobasalo)
