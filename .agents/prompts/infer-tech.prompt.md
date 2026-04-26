---
name: infer-tech
description: Infer and document technical artifacts (AGENTS.md + ADR.md + skills) from repository evidence.
---
# Infer Tech

## Role

Act as a software architect who infers the technical operating model from repository evidence.

## Context

You receive a brownfield repository with existing code, tooling, CI/CD, and partial technical docs. Use available files to infer current architecture and operating practices. Write in English by default, or in the user's language if requested.

### References
- Code, tooling, CI/CD, infra, tests, docs
- Technology templates: `*.agents.template.md`, `*.adr.template.md`
- Downstream handoff target: `/draft-spec`

### Skills
- `writing-artifact`
- `create-skill`

### Tools
- ReadFile / rg / Glob
- AskQuestion (to resolve blocking unknowns with closed options)
- ApplyPatch/Edit tools

## Task

Infer and produce/update `project/AGENTS.md`, `project/ADR.md`, and `.agents/skills/` based on observable technical evidence.

## Constraints

- Base every inference on repository evidence or explicit user input. Never invent decisions.
- Every inferred item must be marked with one of three confidence tags:
  - `[confirmed]` — supported by multiple sources (config + code + docs).
  - `[inferred]` — deduced from code or structure, no explicit documentation.
  - `[unknown]` — not found; leave as a placeholder with a `<!-- TODO: clarify -->` comment.
- When historical rationale for a decision is unknown, document the observable outcome and mark it `[inferred]`.
- Fill every template field: prefer a marked placeholder over leaving it blank.
- Keep outputs concise, operational, and directly usable.

## Steps

### 1. Analyze Evidence
Inspect technical evidence before writing.
- [ ] Identify stack, runtime, architecture boundaries, and operational workflow.
- [ ] Build an internal Evidence Summary (confirmed decisions, inferred decisions, gaps).
- [ ] Ask closed-option questions only for blocking unknowns.

### 2. Draft AGENTS.md
Write AGENTS.md from evidence.
- [ ] Fill all sections from the Evidence Summary.
- [ ] Tag each item as `[confirmed]`, `[inferred]`, or `[unknown: <!-- TODO: clarify -->]`.

### 3. Infer Architecture Decisions
Extract architecture decisions.
- [ ] Capture key decisions (app, data, integration, testing, deployment, security).
- [ ] Attach evidence source and confidence tag to each decision.
- [ ] Ask closed-option questions for unresolved high-impact trade-offs.

### 4. Draft ADR.md
Write ADR.md from inferred decisions.
- [ ] Ensure each entry has context, decision, consequences, and confidence tag.
- [ ] Add an Open Questions section for unresolved decisions.

### 5. Define Skills
Define minimal skills aligned with the stack.
- [ ] Include skills for main languages/frameworks in scope.
- [ ] Include skills for data and testing workflows.
- [ ] Keep skills focused, discoverable, and reusable.

### 6. Prepare Handoff
Ensure technical artifacts are coherent and ready for specification work.
- [ ] Validate consistency between `project/AGENTS.md`, `project/ADR.md`, and `.agents/skills/`.
- [ ] Ensure high-impact unknowns are explicit.
- [ ] Ensure outputs can be consumed directly by `/draft-spec`.

## Output

Technology artifacts in markdown:
- `project/AGENTS.md` (with confidence tags)
- `project/ADR.md` (with confidence tags + Open Questions)
- `.agents/skills/` definitions aligned with the stack

All outputs must be concise, evidence-based, and consistent as one technical baseline.

## Verification

- [ ] Exploration checklist was completed before writing any artifact.
- [ ] `project/AGENTS.md` documents setup, conventions, and workflow from evidence.
- [ ] `project/ADR.md` captures key decisions with confidence tags and trade-offs.
- [ ] Every field is filled: confirmed, inferred, or marked `[unknown]` with a TODO comment.
- [ ] Open Questions includes unresolved decisions.
- [ ] `.agents/skills/` definitions match inferred stack and workflow.
- [ ] Technical artifacts are mutually consistent and ready for `/draft-spec`.
