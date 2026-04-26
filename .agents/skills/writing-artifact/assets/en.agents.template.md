# AGENTS.md — {project_name}

## Product

{short description of the product, its purpose, and main features}

## Environment

### Configuration

- **Root_Folder**: `/`
- **Agents_Folder**: `/.agents` | `/.claude` | `/.github`
- **Agents_file**: `/AGENTS.md` | `/CLAUDE.md` | `/.github/copilot-instructions.md`
- **Project_Folder**: `/project` | `/docs`
- **OS dev**: `Windows` | `Linux` | `MacOS`
- **Terminal**: `PowerShell` | `Git Bash` | `Terminal`
- **Default branch**: `main` | `master` | `trunk`
- **Git remote**: {URL of the git remote repository}

### Behavior

- When using templates, replace {placeholders} with concrete values.
- Code and documentation must be in {documentation_language}.
- Chat responses must be in the language of the user prompt.
- Sacrifice grammar for conciseness when needed to fit response limits.
- Always lint with `npm run lint` before staging and committing changes.

### Conventions

Use slugs with hyphens for any identifiers: `add-task`, `fix-bug`, `update-deps`.

## Technology

### Stack

- **Language**: {Programming language(s) used in the project}
- **Framework**: {Framework(s) used in the project}
- **Database**: {Database(s) used in the project}
- **Security**: {Security configuration}
- **Testing**: {Testing frameworks}
- **Logging**: {Logging configuration}

### Workflow

```bash
# Set up the project
{setup_commands}

# While developing, watch for changes and run tests automatically
# Watch and compile the project while developing
{watch_and_build_commands}
# Watch and run unit tests while writing tests
{watch_unit_test_commands}
# Static linting and type checking after writing code
{lint_and_typecheck_commands}

# Run unit tests
{unit_test_commands}
# Run end-to-end tests
{e2e_test_commands}

# Run all tests before merging or publishing
{all_test_commands}

# Build/Compile the project for production
{production_build_commands}
# Run the project as a production server
{production_run_commands}
```

### TreeView

```text
.                         # Project root
├── {agents_file}         # This file contains instructions for agents
├── README.md             # Project overview
├── {agents_folder}/      # Agents skills and prompts
│   └── skills/           # Agent skills for specific tasks
├── {project_folder}/     # Project-specific documentation
│   ├── ADR.md            # Architecture Decision Records
│   ├── PRD.md            # Product Requirements Document
│   └── specs/            # Project specifications
├── src/                  # Application source
└── other/                # Any other relevant folders or files
```

---

> End of AGENTS.md · {project_name} · {date}
