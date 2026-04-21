# Context: P1-T01-TASK-0001

## Required Documents

### Runtime (always load)
- `docs/runtime/PROJECT_RULES.md`

### Canonical (load for this task)
- `docs/canonical/architecture.md` — package structure must match defined subsystems (CLI, runner, ingest, formatter)
- `docs/canonical/cli_spec.md` — scaffold must accommodate the command surface defined there

### Working (load if needed)
- `docs/working/implementation_plan.md` — Phase 1 goals and exit criteria
- `docs/working/backlog.md` — P1-T01 through P1-T05 context

### Packet Files
- `tasks/P1-T01-TASK-0001/task.md`
- `tasks/P1-T01-TASK-0001/plan.md`
- `tasks/P1-T01-TASK-0001/deliverable_spec.md`

## Excluded Context

- `docs/canonical/data_contracts.md` — schema definitions are not needed for scaffold
- `docs/canonical/workflow_spec.md` — workflow not relevant at scaffold stage
- `docs/working/open_questions.md` — Q2 (CLI framework) is noted but not blocking this task

## Context Sufficiency Note

Architecture and CLI spec are sufficient to determine the correct package layout; implementation plan provides phase exit criteria for acceptance.
