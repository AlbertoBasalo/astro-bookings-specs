# Backlog — AstroBookings

# Tabla de Especificaciones

| **Especificación** | Dependencias | Estado | Importancia |
|---|---|---|---|
| FR1-[gestionar-cohetes-y-rango-de-accion](./specs/FR1-gestionar-cohetes-y-rango-de-accion.spec.md) | - | Pendiente | ALTA |
| FR2-[planificar-lanzamientos-con-parametros-comerciales-y-operativos](./specs/FR2-planificar-lanzamientos-con-parametros-comerciales-y-operativos.spec.md) | FR1 | Pendiente | ALTA |
| FR3-[registrar-reservas-sin-exceder-capacidad](./specs/FR3-registrar-reservas-sin-exceder-capacidad.spec.md) | FR1, FR2 | Pendiente | ALTA |
| FR4-[suspender-lanzamientos-con-causa](./specs/FR4-suspender-lanzamientos-con-causa.spec.md) | FR2, FR3 | Pendiente | ALTA |
| FR5-[ejecutar-cobros-y-devoluciones-con-pasarela-ficticia](./specs/FR5-ejecutar-cobros-y-devoluciones-con-pasarela-ficticia.spec.md) | FR3, FR4 | Pendiente | baja |
| TR1-[seguridad-mvp](./specs/TR1-seguridad-mvp.spec.md) | FR1, FR2, FR3, FR4, FR5 | Pendiente | baja |
| TR2-[rendimiento-operativo-mvp](./specs/TR2-rendimiento-operativo-mvp.spec.md) | FR2, FR3 | Pendiente | baja |
| TR3-[confiabilidad-de-estados-y-transacciones](./specs/TR3-confiabilidad-de-estados-y-transacciones.spec.md) | FR3, FR4, FR5 | Pendiente | ALTA |
| TR4-[observabilidad-funcional-mvp](./specs/TR4-observabilidad-funcional-mvp.spec.md) | FR1, FR2, FR3, FR4, FR5 | Pendiente | baja |
| TR5-[integracion-pasarela-ficticia-desacoplada](./specs/TR5-integracion-pasarela-ficticia-desacoplada.spec.md) | FR5 | Pendiente | baja |
| TR6-[persistencia-relacional-e-integridad](./specs/TR6-persistencia-relacional-e-integridad.spec.md) | FR1, FR2, FR3, FR4, FR5 | Pendiente | ALTA |

---

> Convención visual :

- Especificación-pendiente
- _Especificación-en-curso_
- ~~Especificación-completada~~
- **Especificación-bloqueada**
- **~~Especificación-fallida~~**

---

> Fin del Backlog · AstroBookings · 2026-04-26
