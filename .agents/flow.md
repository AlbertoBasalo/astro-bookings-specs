# Commands workflow

## Greenfield
- Outline-Product
  - input: idea (optional)
  - output: briefing, prd
- Outline-Technology
  - input: boilerplate (optional)
  - output: agents, add, skills

## Brownfield
- Infer-Product
  - input: codebase
  - output: briefing, prd
- Infer-Technology
  - input: codebase
  - output: agents, add, skills

- Write-Spec
  - input: requirement (optional)
  - output: spec, backlog
- Implement-Spec
  - input: spec (optional)
  - output: plans, code, tests, changelog and backlog update
    - Plan-Spec
      - input: spec (optional)
      - output: plans
    - Implement-Plan
      - input: plan
      - output: code, tests
    - Release-Spec
      - input: spec (optional)
      - output: changelog and backlog update


## Maintenance
- Update-Product
  - input: requirement by user
  - output: prd
- Fix-Spec
  - input: bug by user
  - output: spec, backlog