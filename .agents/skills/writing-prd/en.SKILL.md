---
name: writing-prd
description: Creates a Product Requirements Document (PRD) from a briefing or existing project context. To be used in new or existing projects, creating or updating their requirements document.
---

# Writing a Product Requirements Document (PRD)

## Role

Act as a business analyst specialized in **application development**. Your goal is to transform the product context into a structured PRD.

## Task

Create or update the PRD based on the briefing and project context.

## Context

Start from a briefing. If no clear briefing exists, use the [writing-briefing](../writing-briefing/SKILL.md) skill first to create it.  
Ask for clarification if needed.

### Project modes

#### Greenfield
Use:
- idea provided
- briefing document `{Project_Folder}/briefing.md`
- `{Root_Folder}/README.md` if available

#### Brownfield
Analyze existing system:
Focus on:
- `{Root_Folder}/README.md`
- `{Root_Folder}/CHANGELOG.md`
- `{Root_Folder}/docs`
- `{Root_Folder}/AGENTS.md`
- `{Project_Folder}/PRD.md`, `ADD.md`, specs
- codebase structure (high level only)
Goal: extract intent + constraints, not implementation details.


## Steps to create the PRD:

### 1. Clarifying questions

Ask only questions that affect decisions in the PRD.

You MUST cover:

- Functional scope (what the system must do)
- Constraints (what limits exist)
- Technical direction (lightweight decisions only)
- Business rules (domain invariants)
- Architectural drivers (what will influence design)

If possible, propose an initial draft and ask for validation instead of open questions.

### 2. Writing the PRD

Generate PRD following template based on briefing language:
  
- Use the [English PRD template](en.PRD.template.md) 
- Use the [Spanish PRD template](es.PRD.template.md)

Rules:
- Keep concise
- Do not repeat briefing
- Focus on decisions, not narrative
- Prefer fewer but stronger requirements

Límites:
- 3–9 Functional Requirements (if the application is complex, make the requirements less specific, because they will be detailed in future specification documents)

## Verificación 

- [ ] A comprehensive PRD at `{Project_Folder}/PRD.md`.
- [ ] FRs are business capabilities (not implementation)
- [ ] TRs are decisions (not theory)
- [ ] Business Rules are invariants