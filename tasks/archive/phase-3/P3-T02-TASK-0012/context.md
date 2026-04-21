# Context: P3-T02-TASK-0012

## Required Documents

### Runtime (always load)
- `docs/runtime/PROJECT_RULES.md`

### Canonical (load for this task)
- `docs/canonical/architecture.md` — §2.3 runner constraints, §3 data flow

### Packet Files
- `tasks/P3-T02-TASK-0012/task.md`
- `tasks/P3-T01-TASK-0011/results.md` — run.js output contract (result.json schema)

## Adapter Context
- **Primary Adapter:** code_adapter
- **Secondary Adapters:** none
- **Adapter Rationale:** Python module implementation

## Excluded Context
- `docs/canonical/cli_spec.md` — not needed; runner is not CLI-facing in this task
- `docs/canonical/data_contracts.md` — Grain packet conversion is P3-T03/P4

## Context Sufficiency Note
architecture.md §2.3 and the P3-T01 result.json contract are sufficient to implement and test the runner module.
