# FR1-gestionar-cohetes-y-rango-de-accion

## 1. Problema

Gestionar cohetes y su rango de acción.

### Contexto

El PRD define que AstroBookings debe operar lanzamientos compatibles con destino y capacidad. Sin una gestión formal de cohetes (alta, consulta y actualización), no se puede validar correctamente que un lanzamiento use un vehículo apto para Tierra, Luna o Marte, ni limitar reservas según capacidad máxima.

### Historias de usuario

- Como `operador` quiero **registrar un cohete con su capacidad y rango de acción** para _habilitar su uso en la planificación de lanzamientos_.
- Como `operador` quiero **consultar el catálogo de cohetes** para _seleccionar rápidamente un vehículo compatible con el destino_.
- Como `operador` quiero **actualizar los datos operativos de un cohete** para _mantener información confiable para decisiones de negocio_.

### Fuera de scope

- Mantenimiento avanzado de cohetes (telemetría, revisiones técnicas históricas, partes de taller).
- Gestion documental/auditoría legal externa del activo físico.
- Algoritmos de asignación automática de cohete a lanzamiento.

---

## 2. Solución

Se incorpora un módulo de cohetes como fuente de verdad para operaciones: permite CRUD operativo controlado, expone endpoints REST para backoffice y habilita vistas de consulta/edición en la app interna. El dominio se mantiene acotado al MVP con reglas estrictas de validación para garantizar compatibilidad destino-rango y capacidad.

### Modelo

#### Cohete
- id: `uuid`, identificador único.
- nombre: `string`, etiqueta operacional visible.
- capacidadMaxima: `number`, asientos disponibles por lanzamiento.
- rangoAccion: `enum`, valores permitidos `Tierra | Luna | Marte`.
- activo: `boolean`, habilita/deshabilita uso operativo.
- creadoEn: `datetime`, timestamp de alta.
- actualizadoEn: `datetime`, timestamp de última modificación.
- Regla1: `capacidadMaxima` debe ser mayor que 0 y menor o igual que 10.
- Regla2: `rangoAccion` debe pertenecer al enum permitido.
- Regla3: no se permite borrar físicamente; se desactiva (`activo=false`) para preservar trazabilidad.

**Persistencia**:
- Tabla relacional `cohetes`.
- Indice por `rangoAccion` y `activo` para consultas de operación.
- Integridad referencial con `lanzamientos.coheteId`.

### Back

API REST propuesta:
- `POST /api/cohetes`: crea cohete con validaciones de dominio.
- `GET /api/cohetes`: lista cohetes (filtros opcionales por `rangoAccion` y `activo`).
- `GET /api/cohetes/{id}`: obtiene detalle de cohete.
- `PATCH /api/cohetes/{id}`: actualiza campos permitidos (`nombre`, `capacidadMaxima`, `rangoAccion`, `activo`).

Reglas de negocio backend:
- Rechazar `capacidadMaxima` fuera de rango con error de validación.
- Rechazar `rangoAccion` inválido con error de contrato.
- Impedir desactivar un cohete si tiene lanzamientos futuros en estado `programado` o `confirmado`; devolver error funcional y requerir reasignación previa.


Observabilidad: 
- Log estructurado en alta, cambio de capacidad/rango y desactivación.
- Correlation ID propagado para trazabilidad entre UI y API.

### Front

Backoffice interno:
- Pantalla de listado de cohetes con filtros por rango y estado.
- Formulario de alta/edicion con validaciones inmediatas.
- Indicadores de disponibilidad (`activo`) y capacidad.

Flujos:
- Alta de cohete con feedback de éxito/error de validación.
- Edición de atributos operativos.
- Desactivación con mensaje explícito cuando existan lanzamientos dependientes.

Estados UI:
- `idle`, `loading`, `success`, `error-validacion`, `error-negocio`.

---

## 3. Verificación

- [ ] el sistema DEBE permitir crear un cohete con `nombre`, `capacidadMaxima` valida (1..10), `rangoAccion` valido y estado inicial `activo=true`.
- [ ] CUANDO se consulta el listado de cohetes el sistema DEBE devolver filtros por `rangoAccion` y `activo` de forma consistente con la base de datos.
- [ ] SI `capacidadMaxima` es 0, mayor que 10 o no numérica ENTONCES el sistema DEBE rechazar la operación con error de validación y sin persistir cambios.
- [ ] SI `rangoAccion` no es `Tierra`, `Luna` o `Marte` ENTONCES el sistema DEBE rechazar la operación con error de contrato.
- [ ] CUANDO se intenta desactivar un cohete con lanzamientos futuros `programado`/`confirmado` el sistema DEBE bloquear la acción e informar la dependencia.
- [ ] CUANDO se actualiza un cohete valido el sistema DEBE persistir cambios, registrar evento de auditoria y reflejar el resultado en la API y la UI.

### Trazabilidad

- Requerimiento origen PRD: `FR1 — Gestionar cohetes y su rango de acción`.
- Requerimientos técnicos aplicados: `TR1`, `TR3`, `TR4`, `TR6`.

### Suposiciones

- La capacidad máxima de 10 asientos es una regla vigente del dominio y debe aplicarse en este módulo.
- La desactivación lógica cubre la necesidad MVP de "baja" sin borrado físico.

### Preguntas abiertas

- Confirmar si la capacidad máxima de 10 aplica a todos los rangos o si debe parametrizarse por tipo de cohete en iteraciones futuras.

---

> Fin de Spec · FR1 · 2026-04-26
