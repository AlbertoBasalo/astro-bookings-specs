# {F1}. {Feature Name}

---

## Problem definition

### Context

{Describe the problem or need this feature addresses. Who is affected and why does it matter?
Focus on the "why", not the solution. 2–4 sentences.}

### User stories

- As a {role} I want to {**action**} so that {benefit}

---

## Solution sketch

{One or two sentences on the approach. Technology-neutral.}

### Model

| Entity | Attribute | Type | Constraints |
|--------|----------|-------------|-------------|
| `{Entity}` | `{Attribute}` | `{Type#?}` | min, max... |

> legend: `#` for unique, `?` for optional

### Back

- MUST {core responsibility — persistence, validation, business rule}
- MUST NOT {explicit prohibition}
- MAY {optional behaviour}

### Front

- MUST {presentation or interaction responsibility}
- MUST NOT {explicit prohibition}
- MAY {optional behaviour}

### Contract

| Method | Endpoint | Success | Error |
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

## Acceptance criteria

- [ ] the {system} SHALL {always-true behavior}
- [ ] WHEN {event or user action} the {system} SHALL {expected response}
- [ ] IF {unwanted or error condition} THEN the {system} SHALL {safe/correct behavior}

---

## Out of scope

- {Explicitly excluded item}

---

## Open questions

- {Question that must be resolved before or during implementation.}