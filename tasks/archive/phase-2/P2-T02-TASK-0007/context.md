# Context: P2-T02-TASK-0007

## Required Documents

### Runtime (always load)
- `docs/runtime/PROJECT_RULES.md`

### Canonical (load for this task)
- `docs/canonical/cli_spec.md` — §5 config file structure, §3 exit codes

### Working (load if needed)
- none

### Packet Files
- `tasks/P2-T02-TASK-0007/task.md`
- `tasks/P2-T02-TASK-0007/plan.md`
- `tasks/P2-T02-TASK-0007/deliverable_spec.md`

## Adapter Context
- **Primary Adapter:** code_adapter
- **Secondary Adapters:** none
- **Adapter Rationale:** Pure Python module; no frontend involvement

## Excluded Context
- `docs/canonical/data_contracts.md` — not needed for config parsing
- `docs/canonical/architecture.md` — already read; no new info needed for this task

## Context Sufficiency Note
cli_spec.md §5 fully defines the config structure; sufficient to implement and test the loader.
