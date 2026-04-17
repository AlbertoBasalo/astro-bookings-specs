# AstroBookings

**Idea**  
System to manage space travel bookings for orbital tourism companies.

**Problem**  
Orbital tourism companies need to control seats, bookings, and launch statuses without errors or overbooking.

They operate rockets that travel to destinations such as low Earth orbit, the Moon, or Mars, always with limited capacity.  
Each launch must be profitable: it has a price per seat and a minimum occupancy to avoid being canceled.  
Additionally, cancellations may occur due to technical or weather-related reasons.  
Payments and refunds are managed through external systems.

**Users**
- Company operators (manage fleet, launches, and customer bookings)
    
**Features**
- Manages rockets with limited capacity and range.
- Allows defining launches with price per seat and minimum occupancy.
- Manages customers identified by email.
- Allows booking seats and automatically controls availability.
- Manages the status of launches:    
    - scheduled → confirmed → successful        
    - suspended due to low occupancy        
    - canceled due to technical or external reasons
**Not included**
- Real payments (simulation only)    
- Authentication (internal use by operators)    
- Persistence (in-memory data)    

**Value**  
Allows validating the booking business logic, avoiding overbooking and operational errors.

**Notes**
- Demo project for training purposes, not intended for production.
- Recommended solution via REST API and Web Application.

---

- [GitHub Repository](https://github.com/AlbertoBasalo/astro-bookings)
- Default branch: `main`

- **Autor**: [Alberto Basalo](https://albertobasalo.dev)
- **Ai Code Academy en Español**: [AI code Academy](https://aicode.academy)
- **Redes sociales**:
  - [X](https://x.com/albertobasalo)
  - [LinkedIn](https://www.linkedin.com/in/albertobasalo/)
  - [GitHub](https://github.com/albertobasalo)
