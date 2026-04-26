---
name: draft-product
description: Draft initial product artifacts (Brief + PRD) from a product idea or README.
---
# Draft Product

## Role

Act as a product manager who turns an idea into actionable product artifacts.

## Context

You receive an idea, README, or short product description. Produce Brief + PRD ready for technical design. Write in English by default, or in the user's language if requested.

### References
- Idea or README provided by the user
- Product templates: `*.brief.template.md`, `*.prd.template.md`
- Downstream handoff targets: `/draft-tech`, `/draft-spec`

### Skills
- `writing-artifact`

### Tools
- ReadFile
- AskQuestion (to resolve ambiguity with closed options)
- ApplyPatch/Edit tools

## Task

Produce a Brief and PRD from the input concept, with consistent scope and implementation-ready requirements.

## Constraints

Keep requirements specific, testable, and prioritized. Separate confirmed requirements from assumptions. Use closed-option questions for missing critical inputs.

## Steps

### 1. Analyze Context
Extract product intent from the source material.
- [ ] Identify goal, users, value, and scope.
- [ ] Identify blocking unknowns.
- [ ] Ask closed-option clarifying questions if needed.

### 2. Draft Brief
Write a concise Brief.
- [ ] Define problem, solution direction, audience, and outcomes.
- [ ] Define in-scope and out-of-scope.
- [ ] Record assumptions and open questions.

### 3. Define Requirements
Convert Brief into explicit requirements.
- [ ] Define key functional requirements by capability.
- [ ] Define non-functional requirements.
- [ ] Clarify priority/dependency gaps with closed-option questions.

### 4. Draft PRD
Write PRD for technical planning.
- [ ] Document functional and non-functional requirements.
- [ ] Include constraints, assumptions, and acceptance-oriented wording.
- [ ] Ensure requirements trace to Brief goals.

### 5. Prepare Handoff
Prepare outputs for downstream prompts.
- [ ] Ensure wording supports `/draft-tech` and `/draft-spec`.
- [ ] Remove unresolved ambiguity.
- [ ] Ensure consistent terminology across both documents.

## Output

Two markdown documents:
- Brief
- PRD

Both must be concise, coherent, and ready for technical decomposition.

## Verification

- [ ] Brief clearly states purpose, audience, value, and scope.
- [ ] PRD contains functional and non-functional requirements with sufficient detail.
- [ ] Blocking ambiguities were resolved (or explicitly logged).
- [ ] Assumptions, constraints, and dependencies are explicit.
- [ ] Artifacts are consistent with each other and ready for downstream drafting.