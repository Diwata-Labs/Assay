# Context: P2-T01-TASK-0006

## Required Documents

### Runtime (always load)
- `docs/runtime/PROJECT_RULES.md`

### Canonical (load for this task)
- `docs/canonical/cli_spec.md` — command surface, flags, exit codes, stub policy
- `docs/canonical/architecture.md` — §2.1 CLI component definition

### Working (load if needed)
- `docs/working/backlog.md` — Phase 2 task sequence

### Packet Files
- `tasks/P2-T01-TASK-0006/task.md`
- `tasks/P2-T01-TASK-0006/plan.md`
- `tasks/P2-T01-TASK-0006/deliverable_spec.md`

## Adapter Context
- **Primary Adapter:** code_adapter
- **Secondary Adapters:** none
- **Adapter Rationale:** Pure Python implementation task; no frontend or infra involvement

## Excluded Context
- `docs/canonical/data_contracts.md` — not relevant until Phase 4+
- All Phase 3+ task packets — out of scope

## Context Sufficiency Note
cli_spec.md and architecture.md §2.1 are sufficient to implement the entrypoint and all five command stubs.
