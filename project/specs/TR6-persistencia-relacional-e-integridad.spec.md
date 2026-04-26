# TR6-persistencia-relacional-e-integridad

## 1. Problema

Persistencia relacional para integridad y trazabilidad de datos.

### Contexto

El PRD exige base de datos relacional para asegurar integridad referencial y consistencia de las operaciones del dominio.

### Historias de usuario

- Como `operador` quiero **datos consistentes entre módulos** para _evitar contradicciones operativas_.
- Como `equipo técnico` quiero **integridad referencial explícita** para _proteger relaciones de negocio_.
- Como `equipo del taller` quiero **persistencia estable** para _demostrar flujos repetibles entre sesiones_.

### Fuera de scope

- Sharding y escalado horizontal avanzado.
- Estrategias complejas de replicación multi-región.
- Data warehouse analítico.

---

## 2. Solución

Definir esquema relacional mínimo para cohetes, lanzamientos, reservas, pagos y devoluciones, con claves, índices y constraints básicas.

### Modelo

#### Entidades mínimas
- `cohetes`
- `lanzamientos`
- `reservas`
- `pagos`
- `devoluciones`

**Reglas**:
- Regla1: claves primarias y foráneas obligatorias entre entidades relacionadas.
- Regla2: restricciones de dominio críticas se validan en aplicación y, donde aplique, en base de datos.
- Regla3: timestamps de creación/actualización para trazabilidad básica.

### Back

- Repositorios sobre BD relacional con transacciones en operaciones críticas.
- Migraciones versionadas para crear/ajustar esquema.
- Índices mínimos para consultas de operación.

### Front

- Sin acoplamiento directo a base de datos; consumo vía API.

---

## 3. Verificación

- [ ] el sistema DEBE persistir entidades de dominio en tablas relacionales con relaciones válidas.
- [ ] CUANDO se crea una entidad hija el sistema DEBE validar existencia de su entidad padre.
- [ ] SI se intenta romper integridad referencial ENTONCES el sistema DEBE rechazar la operación.
- [ ] CUANDO se reinicia la aplicación el sistema DEBE conservar datos operativos previamente registrados.

---

> Fin de Spec · TR6 · 2026-04-26
