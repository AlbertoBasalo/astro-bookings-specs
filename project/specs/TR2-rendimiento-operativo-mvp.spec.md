# TR2-rendimiento-operativo-mvp

## 1. Problema

Rendimiento suficiente para operación interna en tiempo interactivo.

### Contexto

El PRD pide respuesta en segundos para consultas y reservas del backoffice. Para un taller/demo, se necesita fluidez visible sin optimización prematura.

### Historias de usuario

- Como `operador` quiero **consultas ágiles** para _trabajar sin esperas largas_.
- Como `operador` quiero **reserva y cambios de estado rápidos** para _mantener continuidad operativa_.
- Como `equipo técnico` quiero **límites de rendimiento básicos** para _detectar regresiones tempranas_.

### Fuera de scope

- Optimización extrema de alta escala.
- Arquitecturas distribuidas complejas.
- Cache multinivel avanzada.

---

## 2. Solución

Definir objetivos de latencia MVP y medidas simples de eficiencia en endpoints críticos.

### Modelo

#### ObjetivoRendimiento
- endpoint: `string`
- objetivoMsP95: `number`

**Reglas**:
- Regla1: operaciones críticas (`GET` listados principales, `POST` reservas) deben mantenerse en respuesta interactiva.
- Regla2: consultas deben usar índices mínimos por claves de búsqueda frecuentes.

### Back

- Índices en consultas críticas (`estado`, `lanzamientoId`, `fecha`).
- Paginación simple en listados.
- Medición de latencia por endpoint.

### Front

- Indicadores de carga consistentes.
- Evitar recargas redundantes en vistas de listado/detalle.

---

## 3. Verificación

- [ ] el sistema DEBE responder operaciones críticas en tiempos interactivos para uso interno.
- [ ] CUANDO se listan entidades voluminosas el sistema DEBE aplicar paginación.
- [ ] SI una consulta crítica no usa índice ENTONCES el sistema DEBE registrar deuda técnica explícita.
- [ ] CUANDO se ejecutan pruebas básicas de carga del taller el sistema DEBE mantener estabilidad sin timeouts frecuentes.

---

> Fin de Spec · TR2 · 2026-04-26
