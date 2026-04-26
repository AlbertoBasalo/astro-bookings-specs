---
name: draft-spec
description: Draft a new specification from one PRD requirement.
argument-hint: Requirement ID, title, or change request to specify
---
# Draft Spec

## Role

Act as a product+engineering analyst who turns one PRD requirement into an implementable specification.

## Context

A project has product artifacts (Brief, PRD) and a specification area (`specs/`, `BACKLOG`). Input may be a requirement ID/title, change request, or plain text. If no requirement is provided, use the first PRD requirement without a spec. Write in English by default, or in the user's language if requested.

### References
- PRD, Brief, `specs/`, `BACKLOG`
- Templates: `*.spec.template.md`, `*.backlog.template.md`
- Roadmap flow: `/draft-spec` -> `/implement-spec`

### Skills
- `writing-artifact`
- `updating-backlog`

### Tools
- ReadFile / rg / Glob
- AskQuestion (closed options for blocking gaps)
- ApplyPatch/Edit tools

## Task

Select one PRD requirement and produce one spec in `specs/<ID>-<slug>.spec.md` with Problem, Solution, and Verification ready for implementation.

## Constraints

- Base the specification on PRD evidence and explicit user input.
- Do not change product intent while specifying.
- Ask closed-option questions for ambiguous requirements.
- State assumptions explicitly when technical detail is missing.

## Steps

### 1. Analyze Context
Identify the target requirement.
- [ ] Use user-provided requirement ID/title if present.
- [ ] Otherwise select the first PRD requirement not represented in `BACKLOG`.
- [ ] If all are already specified, stop and suggest `/update-spec`.

### 2. Analyze Evidence
Collect only what is needed to draft safely.
- [ ] Read related PRD sections and NFR constraints.
- [ ] Check `specs/` and `BACKLOG` to avoid duplication.
- [ ] Identify dependencies and impacted areas.

### 3. Draft Spec
Write one spec file in `specs/`.
- [ ] Follow template sections: Problem, Solution, Verification.
- [ ] Use concrete, testable verification checks.
- [ ] Add explicit assumptions and open questions if needed.

### 4. Define Traceability
Link requirement and spec clearly.
- [ ] Record PRD requirement -> spec mapping.
- [ ] Keep unresolved items under Open Questions.

### 5. Update BACKLOG
Register the spec for implementation.
- [ ] Use `updating-backlog` skill to create or update the spec row.
- [ ] Set initial status and importance using the centralized backlog policy.
- [ ] Ensure no duplicate row exists for the spec.

## Output

One spec file in `specs/` plus one created/updated `BACKLOG` entry for that spec.

## Verification

- [ ] A single PRD requirement was selected (provided by user or first non-specified one).
- [ ] Spec includes Problem, Solution, and Verification.
- [ ] Verification checks are concrete and testable.
- [ ] Traceability to the source PRD requirement is explicit.
- [ ] BACKLOG contains the created or updated spec with Specification, Dependencies, Status, and Importance.
- [ ] BACKLOG state and importance are aligned with workflow intent.
- [ ] Assumptions and unresolved items are explicit.
