---
name: writing-prd
description: "Creates a Product Requirements Document (PRD) from a briefing or existing project context."
---

# Writing a Product Requirements Document (PRD)

## Context

You are an analyst responsible for transforming product context into a structured PRD.

The PRD is a decision document, not a description document.

You MUST start from a briefing or extract one if missing.

If no clear briefing exists, use the [writing-briefing](../writing-briefing/SKILL.md) skill first.

### Project Modes

#### Greenfield

Use:
- provided idea
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

## Steps to create PRD:

### 1. Clarifying Questions

Ask only questions that affect decisions in the PRD.

You MUST cover:

- Functional scope (what the system must do)
- Constraints (what limits exist)
- Technical direction (lightweight decisions only)
- Business rules (domain invariants)
- Architectural drivers (what will influence design)

If possible, propose an initial draft and ask for validation instead of open questions.

  ### 2. PRD Drafting

Generate PRD following template based on user/brief language:
  
- Use the [English PRD template](en.PRD.template.md) 
- Use the [Spanish PRD template](es.PRD.template.md)

Rules:
- Keep concise
- Do not repeat briefing
- Focus on decisions, not narrative
- Prefer fewer but stronger requirements

Limits:
- 3–9 Functional Requirements
- 1–5 Technical Requirements

Each section should be explicit and actionable.

### 3. Review

Ensure:
- FRs are business capabilities (not implementation)
- TRs are decisions (not theory)
- Business Rules are invariant constraints
- Architectural Drivers clearly influence design choices


## Output Checklist

- [ ] A comprehensive P.R.D. at `{Project_Folder}/PRD.md`.