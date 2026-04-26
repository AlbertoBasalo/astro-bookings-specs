# {id}-{slug-requirement-or-bug}
<!-- eg: FR1-create-user TR3-database-infrastructure B99-login-page-failure -->

## 1. Problem

{Name of requirement or bug}

### Context

{Describe why it's necessary, who uses it, and what impact it has on operations or business.}

### User Stories

- As a `user` I want to **{main objective}** so that _{expected benefit}_
- As a `user` I want to **{secondary objective}** so that _{expected benefit}_
- As a `user` I want to **{maintenance or correction action}** so that _{expected benefit}_

### Out of Scope

- {Topic not covered 1}
- {Topic not covered 2}
- {Topic not covered 3}

---

## 2. Solution

{Summarize the solution at a high level: interface, API, persistence, and MVP scope decisions.}

<!-- Fill in the following sections if they are relevant to the proposed solution. Without entering into technical implementation details -->

### Model

#### Entity1
- Attribute1: {type, description}
- Attribute2: {type, description}

**Rules**:
- Rule1: {description of the rule}
- Rule2: {description of the rule}

**Persistence**:
- Table/s relational `{table_name}`.
- Index/s by `{index_name}` for operation queries.
- Referential integrity with `{reference_name}`.

### Back

{Describe the solution at API, business logic, and persistence level.}

### Front

{Describe the solution at user interface, pages, visualization, flows, and states level.}

---

## 3. Verification

- [ ] The system MUST {mandatory behavior}
- [ ] WHEN {user event or action} the system MUST {expected result}
- [ ] IF {invalid condition or error} THEN the system MUST {expected response}
- [ ] WHEN {update or deletion action} the system MUST {business rule}

---

> End of Spec · {spec_id} · {date}
