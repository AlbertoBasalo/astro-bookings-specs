
# Full SSD workflow

```mermaid
flowchart TD
    classDef nd fill:#f8fafc,stroke:#00c4cc,color:#457b9d
    classDef sg fill:#f1f5f9,stroke:#00f2ff,color:#457b9d
    
    %% Estilos de Comandos
    classDef cmdGF fill:#1a472a,stroke:#1a472a,color:#ffffff
    classDef cmdBF fill:#8b4513,stroke:#8b4513,color:#ffffff
    classDef flowOK fill:#f1fff2,stroke:#3ff45e,color:#129f39
    classDef flowKO fill:#fff1f2,stroke:#f43f5e,color:#9f1239

    subgraph R["Requirements"]
        BRF[Brief]:::nd -.-> PRD[PRD]:::nd
    end

    subgraph S["Specifications"]
        SPE[specs/]:::nd -.-> BKL["BACKLOG"]:::nd
    end

    subgraph T["Technology"]
        AGT[AGENTS.md]:::nd -.-> SKI[skills/]:::nd & ADR[ADR]:::nd
    end

    subgraph I["Implementation"]
        PLN[spec.*.plan]:::nd -.-> COD[Source Code + E2E Tests]:::nd
        COD --> RLS[/release-spec/]:::flowOK
        RLS --> BKL & CHL[CHANGELOG]:::nd
        COD --> UPS[/update-spec/]:::flowKO
        UPS --> SPE
    end

    %% Inicio Greenfield
    G([Greenfield]):::nd --- DRP[/draft-product/]:::cmdGF
    DRP --> BRF
    G --- DRT[/draft-tech/]:::cmdGF
    DRT --> AGT

    %% Inicio Brownfield
    B([Brownfield]):::nd --- INP[/infer-product/]:::cmdBF
    INP --> BRF
    B --- INT[/infer-tech/]:::cmdBF
    INT --> AGT
    B --- UPP[/update-product/]:::cmdBF
    UPP --> PRD
    B --- RPS[/report-spec/]:::cmdBF
    RPS --> SPE

    %% Flujo Central
    PRD --> DRS[/draft-spec/]:::flowOK
    DRS --> SPE    
    BKL --> IMS[/implement-spec/]:::flowOK
    IMS --> PLN

    %% Relaciones Tech
    SKI <-.-> COD
    ADR <-.-> PLN

    %% Estilos de líneas (Greenfield y Brownfield)
    linkStyle 6,7,8,9 stroke:#1a472a,stroke-width:2px
    linkStyle 10,11,12,13,14,15 stroke:#8b4513,stroke-width:2px
    
    class R,S,T,I sg
```

## Commands

### From Greenfield
- `/draft-product` - Create initial product requirements (Brief + PRD) for a new project.
- `/draft-tech` - Create initial technology documentation (AGENTS.md, ADR, skills/) for a new project.

### From Brownfield
- `/infer-product` - Derive product requirements from an existing codebase.
- `/infer-tech` - Derive technology documentation from an existing codebase.
- `/update-product` - Update product requirements based on new or changed business needs.

### Spec-driven
- `/draft-spec` - Create a new specification from a requirement (defines problem, solution, and verification).
- `/report-spec` - Create a new specification to address a defect reported by QA or end users.
- `/implement-spec` - Run the implementation cycle for one specification: generate plans, produce code, and validate with tests.
- `/release-spec` - Mark a specification as completed, updating its status in the backlog and recording it in the changelog.
- `/update-spec` - Refine an existing specification based on implementation issues and requeue it for implementation.

## Artifacts

### Product
- `Brief` - A high-level description of the product, its purpose, and its target audience.
- `PRD` - Product Requirements Document, defining the product features and requirements.

### Specifications
- `specs/` - The source of truth for system behavior; a directory of detailed specifications (problem, solution, verification), one per feature or bug.
- `BACKLOG` - A structured list of specifications with their status, priority, and dependencies, used for planning and tracking implementation.

### Technology
- `AGENTS.md` - The entry point for any agent joining the project; defines how agents should operate, including rules, workflows, and artifact conventions.
- `skills/` - A directory of reusable capabilities and guidelines for implementing specific technologies.
- `ADR` - Architecture Decision Records, documenting key technical decisions that influence implementation.

### Implementation
- `spec.*.plan` - A set of implementation plans derived from a single specification, defining ordered steps and tasks.
- `Source Code + E2E Tests` - The implementation of the system, including end-to-end tests that validate specifications.
- `CHANGELOG` - A record of completed specifications, documenting what has been implemented and released.