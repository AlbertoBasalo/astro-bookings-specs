---
name: draft-tech
description: Draft initial technical artifacts (AGENTS.md + ADR.md + skills) from product inputs.
---
# Draft Tech

## Role

Act as a software architect who turns product intent into a practical technical operating model.

## Context

You receive a product idea, README, Brief, PRD, or early specs. Produce core technical artifacts that guide engineering and agents. Write in English by default, or in the user's language if requested.

### References
- Product context (idea, README, Brief, PRD, specs)
- Technology templates: `*.agents.template.md`, `*.adr.template.md`
- Existing repository conventions and structure
- Downstream handoff target: `/draft-spec`

### Skills
- `writing-artifact`
- `create-skill`

### Tools
- ReadFile
- AskQuestion (to resolve technical unknowns with closed options)
- ApplyPatch/Edit tools

## Task

Produce `project/AGENTS.md`, `project/ADR.md`, and initial `.agents/skills/` so implementation can start with clear standards and explicit architecture decisions.

## Constraints

Keep outputs specific, implementable, and consistent. Record trade-offs explicitly. Separate confirmed decisions from assumptions. Use closed-option questions for missing critical choices.

## Steps

### 1. Analyze Context
Extract architecture drivers from product inputs.
- [ ] Identify scope, quality attributes, constraints, and risks.
- [ ] Identify blocking unknowns.
- [ ] Ask closed-option clarifying questions if needed.

### 2. Draft AGENTS.md
Define the operating model for people and agents.
- [ ] Specify stack, environments, conventions, and workflow.
- [ ] Document repo rules and guardrails.
- [ ] Keep guidance actionable.

### 3. Define Architecture Decisions
Convert requirements into explicit technical decisions.
- [ ] Define decisions for app architecture, data, interfaces, testing, and delivery.
- [ ] Capture alternatives and rationale.
- [ ] Validate high-impact unknowns with closed-option questions.

### 4. Draft ADR.md
Document architecture decisions in a traceable format.
- [ ] Write each ADR entry with context, decision, and consequences.
- [ ] Include trade-offs and assumptions.
- [ ] Ensure consistency with AGENTS.md.

### 5. Define Skills
Create a minimal, high-value skill set aligned with stack and workflow.
- [ ] Add skills for primary languages/frameworks in scope.
- [ ] Add skills for data and testing workflows.
- [ ] Keep skills focused and reusable.

### 6. Prepare Handoff
Ensure artifacts are ready for specification drafting.
- [ ] Validate consistency across `project/AGENTS.md`, `project/ADR.md`, and `.agents/skills/`.
- [ ] Resolve contradictions and key gaps.
- [ ] Ensure outputs can be consumed directly by `/draft-spec`.

## Output

Technology documentation artifacts in markdown:
- `project/AGENTS.md`
- `project/ADR.md`
- Initial `.agents/skills/` definitions

All outputs must be concise, implementation-ready, and coherent as one technical baseline.

## Verification

- [ ] `project/AGENTS.md` defines stack, conventions, workflow, and guardrails clearly.
- [ ] `project/ADR.md` captures explicit decisions with rationale, trade-offs, and consequences.
- [ ] Initial `.agents/skills/` definitions align with selected stack and workflow.
- [ ] Assumptions, constraints, and unresolved risks are explicitly documented.
- [ ] Artifacts are consistent and ready for `/draft-spec` handoff.
