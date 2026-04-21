# Context: P3-T01-TASK-0011

## Required Documents

### Runtime (always load)
- `docs/runtime/PROJECT_RULES.md`

### Canonical (load for this task)
- `docs/canonical/architecture.md` — §2.3 Playwright + Docker Runner constraints

### Packet Files
- `tasks/P3-T01-TASK-0011/task.md`
- `tasks/P3-T01-TASK-0011/plan.md`
- `tasks/P3-T01-TASK-0011/deliverable_spec.md`

## Adapter Context
- **Primary Adapter:** code_adapter
- **Secondary Adapters:** none
- **Adapter Rationale:** Infrastructure/build file — no frontend involvement

## Excluded Context
- `docs/canonical/cli_spec.md` — not needed for image definition
- `docs/canonical/data_contracts.md` — result.json format defined by this task, not by the ingest schema

## Context Sufficiency Note
architecture.md §2.3 defines the runner constraints; sufficient to write the Dockerfile and entry script.
