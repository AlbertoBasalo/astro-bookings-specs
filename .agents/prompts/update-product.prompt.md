---
name: update-product
description: Update Brief and PRD based on a product change request.
---
# Update Product

## Role

Act as a product manager who applies change requests to existing product artifacts with traceable deltas.

## Context

A brownfield project has existing Brief, PRD, specs, backlog, and implementation evidence. Input may include change requests, business feedback, incidents, analytics, QA findings, and code behavior. Write in English by default, or in the user's language if requested.

### References
- Change request and supporting evidence
- Brief, PRD, `specs/`, `BACKLOG`
- Templates: `*.brief.template.md`, `*.prd.template.md`
- Roadmap flow: `/update-product` -> `/draft-spec`

### Skills
- `writing-artifact`

### Tools
- ReadFile / rg / Glob
- AskQuestion (closed options for blocking ambiguity)
- ApplyPatch/Edit tools

## Task

Analyze the change request, update impacted Brief/PRD sections only, and prepare changed requirements for `/draft-spec`.

## Constraints

- Base updates on explicit user input and repository evidence.
- Do not rewrite the full product scope when only a subset is impacted.
- Mark assumptions and unresolved questions explicitly.
- Keep outputs concise and ready for immediate spec drafting.
- Keep Brief/PRD aligned with template structure.

## Steps

### 1. Analyze Context
Classify the requested change.
- [ ] Identify business driver, expected outcome, and urgency.
- [ ] Classify as new/modified functional or technical requirement.
- [ ] Ask closed-option questions for ambiguity.

### 2. Analyze Evidence
Review current state and conflicts.
- [ ] Review Brief, PRD, related specs, and `BACKLOG`.
- [ ] Compare request with observed implementation behavior.
- [ ] Identify contradictions and constraints.

### 3. Define Impact Scope
Define exactly what changes.
- [ ] Identify impacted Brief/PRD sections.
- [ ] Identify dependencies, constraints, and risks.
- [ ] List unchanged areas explicitly.

### 4. Draft Brief Delta
Update Brief only when intent-level changes exist.
- [ ] Update Brief if purpose, audience, or outcomes changed.
- [ ] Preserve Brief template structure and closing marker.
- [ ] State explicitly when no Brief update is needed.

### 5. Draft PRD Delta
Apply requirement changes in PRD.
- [ ] Update FR/TR sections and `Problem Domain` when impacted.
- [ ] Add `## 4. Requirement Delta` before closing marker.
- [ ] Record added, modified, removed/deprecated items with rationale.
- [ ] Update PRD version in closing marker when requirements change.

### 6. Prepare Handoff
Prepare spec drafting payloads.
- [ ] Create one `/draft-spec` payload per added/modified requirement.
- [ ] Include requirement ID/title, problem, expected behavior, acceptance criteria, constraints, dependencies.

## Output

Updated Brief (or explicit no-change note), updated PRD with `Requirement Delta` + version update, and `/draft-spec` payloads for each changed requirement.

## Verification

- [ ] Change request is classified (new/modified, functional/technical).
- [ ] Brief changed only when product intent/audience/outcomes changed.
- [ ] Brief preserves template structure and closing marker.
- [ ] PRD preserves required sections and includes `## 4. Requirement Delta`.
- [ ] PRD version is updated when requirements changed.
- [ ] Requirement changes are traceable and assumptions/open questions are explicit.
- [ ] `/draft-spec` payloads are ready for each changed requirement.
