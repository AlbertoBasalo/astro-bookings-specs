# {F1}. {Nombre de la funcionalidad}

## Definición del problema

### Contexto

{Describe el problema o la necesidad que resuelve esta feature. ¿A quién afecta y por qué es importante?
Céntrate en el "por qué", no en la solución. 2–3 frases.}

### Historias de usuario

- Como {`rol`} quiero {**acción**} para {_beneficio_}

---

## Boceto de la solución

{Una o dos frases cortas sobre el enfoque. Independiente de la tecnología.}

### Modelo

| Entidad | Atributo | Tipo | Restricciones |
|--------|----------|-------------|-------------|
| `{Entidad}` | `{Atributo}` | `{Tipo#?}` | min, max... |

> leyenda: `#` para único, `?` para opcional (requrido por defecto)

### Back

- {responsabilidad principal — persistencia, validación, regla de negocio}
- {prohibición explícita que no debe implmentarse}
- {comportamiento opcional que puede implmentarse}

### Front

- {responsabilidad principal — persistencia, validación, regla de negocio}
- {prohibición explícita que no debe implmentarse}
- {comportamiento opcional que puede implmentarse}

### Contract

| Método | Endpoint | Success | Error |
|--------|----------|---------|-------|
| `{METHOD}` | `{/api/resource}` | `{2xx}` | `{4xx}` |
| `{METHOD}` | `{/api/resource/:id}` | `{2xx}` | `{4xx}` |

**Request — `{OperationName}`**

```json
{
  "{field}": "{type}"
}
```

**Response — `{ResourceName}`**

```json
{
  "id":      "{uuid}",
  "{field}": "{type}"
}
```

**Error response**

```json
{
  "code":    "{http status code}",
  "error":   "{machine-readable code}",
  "message": "{human-readable description}"
}
```

---

## Criterios de aceptación

- [ ] el {sistema} DEBE {comportamiento siempre verdadero}
- [ ] CUANDO {evento o acción de usuario} el {sistema} DEBE {respuesta esperada}
- [ ] SI {condición de error o no deseada} ENTONCES el {sistema} DEBE {comportamiento seguro/correcto}

---

## Fuera de scope

- {Elemento explícitamente excluido}

---

## Preguntas abiertas

- {Pregunta que debe resolverse antes o durante la implementación.}
