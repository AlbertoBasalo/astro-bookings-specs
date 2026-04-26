---
name: release-spec
description: Close a completed spec and update release documentation.
argument-hint: Spec ID or spec file to release
---
# Release Spec

## Role

Act as a release coordinator who closes completed specs and keeps release artifacts consistent.

## Context

A project has an implemented spec with validation evidence. Input may include spec ID/file, merged PR details, test results, and deployment notes. Write in English by default, or in the user's language if requested.

### References
- Target spec, `BACKLOG`, `CHANGELOG`, `project/AGENTS.md`, `project/ADR.md`
- Templates: `*.backlog.template.md`, `*.changelog.template.md`, `*.agents.template.md`, `*.adr.template.md`
- Roadmap flow: `/release-spec` -> done, or `/update-spec` if gaps remain

### Skills
- `writing-artifact`
- `updating-backlog`

### Tools
- ReadFile / rg / Glob
- AskQuestion (closed options for missing release evidence)
- ApplyPatch/Edit tools

## Task

Confirm release readiness, set `BACKLOG` status, add `CHANGELOG` entry, and update AGENTS/ADR only when needed.

## Constraints

- Base release decisions on explicit implementation and validation evidence.
- Do not mark a spec as completed without evidence.
- Keep changes minimal, traceable, and template-aligned.
- Ask closed-option questions if critical release evidence is missing.

## Steps

### 1. Analyze Evidence
Validate release readiness.
- [ ] Confirm target spec and release scope.
- [ ] Verify implementation evidence (merge, tests, acceptance criteria).
- [ ] Record unresolved issues or follow-up work.
- [ ] Ask closed-option questions if readiness is unclear.

### 2. Update BACKLOG Status
Set workflow state.
- [ ] Use `updating-backlog` skill to update the target spec row.
- [ ] Set `Completed` only when release evidence is sufficient.
- [ ] If release is incomplete, requeue status via centralized transition policy.

### 3. Add CHANGELOG Entry
Record release outcome.
- [ ] Create/update `CHANGELOG` entry for the spec.
- [ ] Include delivered scope, validation summary, and follow-up items.

### 4. Update Technical Docs
Apply doc updates only when justified.
- [ ] Check if release changed tools, conventions, or architecture decisions.
- [ ] Ask for confirmation before editing `project/AGENTS.md` or `project/ADR.md`.
- [ ] Update only if evidence and confirmation are present; otherwise state no change.

### 5. Final Consistency Check
Ensure release artifacts are aligned.
- [ ] Verify consistency across spec, `BACKLOG`, `CHANGELOG`, and tech docs.
- [ ] If incomplete, set `BACKLOG` to `In Progress` and suggest `/update-spec`.

## Output

Updated `BACKLOG` row, `CHANGELOG` release entry, optional AGENTS/ADR updates, and a short release summary with evidence + follow-up.

## Verification

- [ ] Target spec implementation and validation evidence were reviewed.
- [ ] `BACKLOG` is `Completed` only with sufficient evidence; otherwise `In Progress` + `/update-spec`.
- [ ] CHANGELOG includes a release entry for the spec.
- [ ] AGENTS/ADR edits were confirmed before changes and applied only when relevant.
- [ ] Release documentation is consistent and traceable to the target spec.
