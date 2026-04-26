# {id}-{slug-requerimiento-o-bug}
<!-- ej: FR1-crear-usuario TR3-infraestructura-base-de-datos B99-fallo-en-pagina-de-login -->

## 1. Problema

{Nombre del requerimiento o bug}

### Contexto

{Describe por qué es necesario, quién lo usa y qué impacto tiene en operación o negocio.}

### Historias de usuario

- Como `usuario` quiero **{objetivo principal}** para _{beneficio esperado}_
- Como `usuario` quiero **{objetivo secundario}** para _{beneficio esperado}_
- Como `usuario` quiero **{acción de mantenimiento o corrección}** para _{beneficio esperado}_

### Fuera de scope

- {Tema no cubierto 1}
- {Tema no cubierto 2}
- {Tema no cubierto 3}

---

## 2.Solución

{Resume la solución a alto nivel: interfaz, API, persistencia y decisiones de alcance del MVP.}

<!-- Rellenar las siguientes secciones si son relevantes para la solución propuesta. Sin entrar en detalles de implementación técnica -->

### Modelo

#### Entidad1
- Atributo1: {tipo, descripción}
- Atributo2: {tipo, descripción}

**Reglas**:
- Regla1: {descripción de la regla}
- Regla2: {descripción de la regla}

**Persistencia**:
- Tabla/s relacional `{nombre_tabla}`.
- Indice/s por `{nombre_indice}` para consultas de operación.
- Integridad referencial/es con `{nombre_referencia}`.

### Back

{Describe la solución a nivel de API, lógica de negocio y persistencia.}

### Front

{Describe la solución a nivel de interfaz de usuario, páginas, visualización, flujos y estados.}

---

## 3. Verificación

- [ ] el sistema DEBE {comportamiento obligatorio}
- [ ] CUANDO {evento o acción del usuario} el sistema DEBE {resultado esperado}
- [ ] SI {condición invalida o error} ENTONCES el sistema DEBE {respuesta esperada}
- [ ] CUANDO {acción de actualización o baja} el sistema DEBE {regla de negocio}


---

> Fin de Spec · {spec_id} · {fecha}
