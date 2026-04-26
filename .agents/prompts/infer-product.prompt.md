---
name: infer-product
description: Infer and document product artifacts (Brief + PRD) from repository evidence.
---
# Infer Product

## Role

Act as a product analyst who infers product intent from repository evidence.

## Context

You receive a brownfield repository with partial docs. Use README, docs, code, tests, changelog, issues, and user notes to infer the current product state. Write in English by default, or in the user's language if requested.

### References
- README, docs, code, tests, changelog, issues
- Product templates: `*.brief.template.md`, `*.prd.template.md`
- Downstream handoff targets: `/update-product`, `/draft-spec`

### Skills
- `writing-artifact`

### Tools
- ReadFile / rg / Glob
- AskQuestion (to resolve blocking gaps with closed options)
- ApplyPatch/Edit tools

## Task

Infer the current product and produce/update Brief + PRD that reflect observable behavior and evidence.

## Constraints

- Base every inference on repository evidence or explicit user input. Never invent capabilities.
- Every inferred item must be marked with one of three confidence tags:
  - `[confirmed]` — supported by multiple sources (code + docs + tests).
  - `[inferred]` — deduced from code or structure, no explicit documentation.
  - `[unknown]` — not found; leave as a placeholder with a `<!-- TODO: clarify -->` comment.
- Flag contradictions explicitly when behavior and docs diverge.
- Fill every template field: prefer a marked placeholder over leaving it blank.
- Keep outputs concise, actionable, and traceable.

## Steps

### 1. Analyze Evidence
Review product evidence before writing.
- [ ] Read docs, code, and tests to identify product goals, users, and flows.
- [ ] Build an internal Evidence Summary (sources, inferences, gaps, contradictions).
- [ ] Ask closed-option questions only for blocking unknowns.

### 2. Draft Brief
Write Brief from evidence.
- [ ] Fill all sections using the Evidence Summary.
- [ ] Tag each item as `[confirmed]`, `[inferred]`, or `[unknown: <!-- TODO: clarify -->]`.

### 3. Define Requirements
Convert behavior into requirements.
- [ ] Map observed features and flows to requirements.
- [ ] Attach evidence source and confidence tag to each requirement.
- [ ] Ask closed-option questions for critical conflicts or gaps.

### 4. Draft PRD
Write PRD from inferred requirements.
- [ ] Fill all sections with confidence tags.
- [ ] Add an Open Questions section for unresolved unknowns.

### 5. Prepare Handoff
Make artifacts ready for next prompts.
- [ ] Ensure Brief and PRD are consistent in scope and terminology.
- [ ] Ensure each key requirement is traceable to evidence.
- [ ] Ensure unknowns and contradictions are explicit.

## Output

Two markdown documents:
- Brief (with confidence tags)
- PRD (with confidence tags + Open Questions)

Both must be concise, evidence-based, and ready for `/update-product` or `/draft-spec`.

## Verification

- [ ] Exploration checklist was completed before writing any artifact.
- [ ] Brief reflects current purpose, audience, and outcomes from evidence.
- [ ] PRD captures functional and non-functional requirements from behavior.
- [ ] Every field is filled: confirmed, inferred, or marked `[unknown]` with a TODO comment.
- [ ] Open Questions includes unresolved unknowns.
- [ ] Brief and PRD are consistent and traceable to evidence.
