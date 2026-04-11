# AstroBookings Español

Una **API backend** y una **WebApp frontend** para ofrecer reservas de lanzamientos de cohetes.
- Los cohetes tienen plazas limitadas y un rango operativo.
- Los lanzamientos se programan para un cohete en una fecha futura.
- Cada lanzamiento ofrece asientos con precios y umbrales mínimos de pasajeros para ser rentables.
- Un lanzamiento pasa por los siguientes estados: `programado` → `confirmado` → `exitoso`.
- Pero puede ser `suspendido` si no hay pasajeros suficientes o `cancelado` por razones técnicas.
- Un operador o pasajero se identifica por su dirección de correo electrónico y tiene un nombre.
- Los operadores de la plataforma pueden administrar cohetes y lanzamientos.
- Los operadores gestiona cancelaciones y devoluciones a pasajeros.
- Un pasajero puede reservar una plaza en un lanzamiento, sin superar las plazas disponibles.
- A los pasajeros se les factura la reserva, y los pagos se procesan a través de una pasarela simulada.
- A los pasajeros se les devuelve el importe en caso de suspensión o cancelación del lanzamiento.

> [!WARNING]
> AstroBookings es una empresa ficticia de viajes espaciales.
> El sistema está diseñado con fines de demostración y formación. 
> No está pensado para uso en producción; no se requiere seguridad ni base de datos en la fase inicial.

---

- [Repositorio en GitHub](https://github.com/AlbertoBasaloLabs/astro-bookings)
- Rama por defecto: `main`

- **Autor**: [Alberto Basalo](https://albertobasalo.dev)
- **Ai Code Academy en Español**: [AI code Academy](https://aicode.academy)
- **Redes sociales**:
  - [X](https://x.com/albertobasalo)
  - [LinkedIn](https://www.linkedin.com/in/albertobasalo/)
  - [GitHub](https://github.com/albertobasalo)
