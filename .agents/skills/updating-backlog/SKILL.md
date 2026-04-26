---
name: updating-backlog
description: Update BACKLOG rows for specs using a single status/importance policy. Use when creating, updating, releasing, or requeuing specs and any prompt must create or modify BACKLOG entries.
---

# Updating Backlog

Canonical workflow for updating `BACKLOG` entries tied to spec lifecycle.

## Context

IMPORTANT: The statuses and fields are in english, but this skill can be used in any language.
Here is a list of potentially translatable words and phrases:

- `Pending`
- `In Progress`
- `Completed`
- `Blocked`
- `Failed`
- `low`
- `HIGH`
- `Dependencies`
- `Specification`
- `Status`
- `Importance`

## When to Use

- Creating a new spec row in `BACKLOG`
- Updating an existing spec row after spec changes
- Marking a released spec as `Completed`
- Requeuing a spec to `In Progress` after release or implementation gaps

## Required Columns

Always preserve and update these columns:
- `Specification`
- `Dependencies`
- `Status`
- `Importance`

Never remove columns from the backlog template.

## Row Identity and Deduplication

Use this precedence to locate an existing row:
1. Exact spec ID match in `Specification` (for example `FR3`, `B07`)
2. Exact spec file link/path match
3. Exact spec title slug match

If a row is found, update it in place.  
If no row is found, create exactly one new row.  
Never duplicate rows for the same spec.

## Status Policy

Allowed statuses:
- `Pending`
- `In Progress`
- `Completed`
- `Blocked`
- `Failed`

Default status by action:
- New spec from draft/report: `Pending`
- Active implementation started: `In Progress`
- Release validated: `Completed`
- Dependency blocker: `Blocked`
- Implemented but validation failed: `Failed`

Transition guardrails:
- `Completed` -> `In Progress` only when new evidence shows unresolved gaps
- `Completed` -> `Pending` only with explicit user instruction
- `Blocked` -> `Pending` only when blocker is resolved
- `Failed` -> `In Progress` after remediation plan is accepted

If transition intent is unclear, ask a closed-option clarification before updating.

## Importance Policy

Use `HIGH` when user/business impact or urgency is high.  
Use `low` otherwise.

Priority of evidence:
1. Explicit user instruction
2. Defect severity / business impact evidence
3. Existing row value (preserve when no new evidence)

If importance cannot be inferred safely, ask a closed-option clarification.

## Specification Cell Convention

- Keep one entry per spec.
- Include spec ID and link/path in `Specification`.
- Apply the project visual convention for the row text based on `Status`.

## Procedure

### 1. Analyze Target Spec
- [ ] Identify spec ID, title, and file path.
- [ ] Identify action context (draft, report, release, requeue).

### 2. Locate or Create Row
- [ ] Search by ID, then link/path, then slug.
- [ ] Update existing row or create one new row.

### 3. Apply Status and Importance
- [ ] Set status using status policy and transition guardrails.
- [ ] Set importance from explicit instruction or impact evidence.
- [ ] Preserve existing dependencies unless new evidence requires change.

### 4. Update Dependencies
- [ ] Update related dependencies based on the current change.
- [ ] Block or unblock dependents based on the current change.

### 4. Validate Consistency
- [ ] Ensure required columns are complete.
- [ ] Ensure no duplicates exist for the spec.
- [ ] Ensure status aligns with current lifecycle evidence.

## Output

One created or updated `BACKLOG` row for the target spec, with normalized status, importance, dependencies, and spec reference.

## Verification

- [ ] Exactly one row exists for the target spec.
- [ ] Status is valid and transition-compliant.
- [ ] Importance is justified or explicitly clarified.
- [ ] Required columns are complete and template-aligned.
