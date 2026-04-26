---
name: writing-artifact
description: 'Create or update SDD documentation artifacts (Brief, PRD, Spec, etc.) from templates. Use when writing, drafting, or updating any project artifact: brief, prd, spec, backlog, changelog, ADR, AGENTS.md. Triggers: draft artifact, create artifact, write artifact, fill template, redact document.'
argument-hint: 'artifact type to create (e.g. brief, prd, spec)'
---

# Writing Artifact

Guided workflow for creating or updating SDD project artifacts from templates.

## When to Use

- Drafting a new artifact (Brief, PRD, Spec, ADR, BACKLOG, CHANGELOG…)
- Updating an existing artifact with new information
- Filling a template for any SDD document
- Triggered by `/create-artifact`, `/draft-artifact`, or explicit user request to write a document

## Templates

Templates are placed in `./assets/` and named `{language}.{artifact_type}.template.md`.

Examples: `en.brief.template.md`, `es.prd.template.md`

- **Languages**: `en` (English, default), `es` (Spanish)
- **Selection logic**: see the **Template Selection** section below.

## Template Selection

Use this table to resolve the template file from the user's request:

| User asks for…                            | Artifact type | Template file                  |
|-------------------------------------------|---------------|--------------------------------|
| brief, product brief, resumen de producto | `brief`       | `{lang}.brief.template.md`     |
| prd, product requirements, requisitos     | `prd`         | `{lang}.prd.template.md`       |
| spec, specification, feature spec         | `spec`        | `{lang}.spec.template.md`      |
| backlog, task list, lista de tareas       | `backlog`     | `{lang}.backlog.template.md`   |
| agents, agents.md, agent instructions     | `agents`      | `{lang}.agents.template.md`    |
| adr, architecture decision                | `adr`         | `{lang}.adr.template.md`       |
| plan, implementation plan                 | `plan`        | `{lang}.plan.template.md`      |
| changelog, release notes                  | `changelog`   | `{lang}.changelog.template.md` |

**Language (`{lang}`)**: infer from the user's request language or an explicit argument. Default to `en`.

**Fallback order** when the resolved file does not exist in `./assets/`:
1. Try `en.{artifact_type}.template.md`.
2. If still missing, use the closest existing template as structural reference and adapt it.
3. Inform the user that no specific template was found and describe the structure being used.

## Procedure

### Step 1 — Evaluate Context and Select Template

1. Identify the artifact type from the user's request using the **Template Selection** table above.
2. Determine the language (`en` or `es`) from the request language or explicit argument; default to `en`.
3. Resolve the template filename: `{lang}.{artifact_type}.template.md`.
4. Check that the file exists in `./assets/`; apply the fallback order if not.
5. Check the workspace for related existing artifacts (PRD, Brief, BACKLOG) to understand context.

### Step 2 — Ask to Complete the Template

1. Review the loaded template and identify all `{placeholder}` fields.
2. Normalize equivalent placeholders to one canonical key when needed (for example, use one key consistently for project name).
3. Check whether any placeholders can already be inferred from existing workspace artifacts.
4. Use the `vscode_askQuestions` tool to collect only the information that cannot be inferred.
5. Keep questions minimal and grouped — avoid asking one question per placeholder.

### Step 3 — Draft (Create or Update) the Artifact

1. If creating: determine the correct output path under `docs/` or `project/`.
2. If updating: read the existing file first to preserve unchanged sections.
3. Fill all placeholders with collected and inferred values.
4. Write the file using the appropriate tool  for new files or for updates.

### Step 4 — Verify the Artifact

1. Read back the written file and confirm:
   - All `{placeholder}` tokens have been replaced.
   - The document structure matches the template.
   - File path follows workspace conventions.
2. Report the file path to the user as a markdown link.
