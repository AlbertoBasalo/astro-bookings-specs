# AstroBookings

**Idea**  
Internal application for AstroBookings to manage its rocket fleet, launches, and space tourism bookings in a simple, operational way.

**Problem**  
AstroBookings must coordinate commercial and flight operations while maintaining strict control over launch status and seat availability.
The company operates rockets with different ranges and capacities, which requires precise planning to avoid overbooking.
Each launch has economic viability considerations and may be suspended or canceled for business or technical reasons.
It also needs to record payments and refunds in demo mode, without integrating real payment gateways.

**Value**
Provide a practical end-to-end management solution for launches and bookings in a training context, improving operational visibility and capacity control for daily execution.

**Users**
- Flight operations staff
- Booking management staff
- Administration/finance staff

**What it does**
- Manages the rocket fleet with range and seat-capacity attributes.
- Plans launches and tracks their operational progression.
- Records bookings while enforcing availability rules to prevent overbooking.
- Handles launch state changes, including suspension for low occupancy and cancellation for technical or external causes.
- Records demo payments and refunds through a fake gateway.

**Out of scope**
- Integration with real payment gateways.
- Advanced security, fraud prevention, or financial compliance rules.
- 24/7 production-grade operations.

**Notes**
- This is a hackathon-style project with intentionally limited scope and fast implementation.
- It is designed for educational use in courses and workshops, not for production deployment.
- Expected solution format: REST API plus an internal web application for employees.
