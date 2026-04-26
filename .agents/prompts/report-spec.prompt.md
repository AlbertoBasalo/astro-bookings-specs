---
name: report-spec
description: Create or update a bug specification from a defect report.
argument-hint: Bug ID, incident summary, failing behavior, or affected requirement
---
# Report Spec

## Role

Act as a product+engineering analyst who converts a defect report into a spec-ready artifact.

## Context

A project has product artifacts (Brief, PRD), `specs/`, `BACKLOG`, and defect evidence (logs, tests, incidents, QA notes). Input may include bug ID, failing scenario, logs, or screenshots. Write in English by default, or in the user's language if requested.

### References
- Defect evidence, PRD, `specs/`, `BACKLOG`
- Templates: `*.spec.template.md`, `*.backlog.template.md`
- Roadmap flow: `/report-spec` -> `/implement-spec`

### Skills
- `writing-artifact`
- `updating-backlog`

### Tools
- ReadFile / rg / Glob
- AskQuestion (closed options for blocking gaps)
- ApplyPatch/Edit tools

## Task

Analyze the defect, decide create-vs-update, and produce one actionable bug spec with aligned `BACKLOG` entry. Use `Bxx` IDs for bug specs.

## Constraints

- Base all conclusions on explicit evidence from reports, tests, logs, code behavior, or user input.
- Do not hide uncertainty: document assumptions and unknowns explicitly.
- Ask closed-option questions when evidence is insufficient for safe scope.
- Keep output concise and actionable.

## Steps

### 1. Analyze Defect
Classify defect scope and impact.
- [ ] Capture symptom, impact, affected flow, and reproducibility.
- [ ] Record expected vs observed behavior.
- [ ] Ask closed-option questions for blocking gaps.

### 2. Decide Strategy
Choose create vs update.
- [ ] Check `specs/` and `BACKLOG` for overlap.
- [ ] Create new bug spec if no spec covers the defect.
- [ ] Update existing spec only when defect is clearly in scope.
- [ ] Default to create when uncertain and duplication risk is low.

### 3. Draft Spec
Create or update the target spec.
- [ ] Use Problem, Solution, Verification sections.
- [ ] Include regression checks for the defect.
- [ ] Use `Bxx` ID format for new bug specs.

### 4. Define Traceability
Link evidence and requirements.
- [ ] Link defect source to the spec.
- [ ] Link affected PRD requirement(s) when applicable.
- [ ] Keep unresolved items under Open Questions.

### 5. Update BACKLOG
Register the bug spec for implementation.
- [ ] Use `updating-backlog` skill to create or update the spec row.
- [ ] Apply status/importance from the centralized backlog policy.
- [ ] Ensure no duplicate row exists for the spec.

## Output

One created/updated bug spec, one created/updated `BACKLOG` row, and a short decision note (`created` vs `updated` + rationale).

## Verification

- [ ] Defect evidence was analyzed (symptom, impact, expected vs observed).
- [ ] The create-vs-update decision is explicit and justified.
- [ ] Spec follows template structure and includes testable verification criteria.
- [ ] Defect-to-spec traceability is explicit.
- [ ] BACKLOG contains the created or updated spec with Specification, Dependencies, Status, and Importance.
- [ ] BACKLOG state and importance match defect severity/urgency.
- [ ] Assumptions and unresolved items are explicit.
