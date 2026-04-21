# Context: P3-T03-TASK-0013

## Required Documents

### Runtime (always load)
- `docs/runtime/PROJECT_RULES.md`

### Canonical (load for this task)
- `docs/canonical/architecture.md` — §2.3 runner output, §3 data flow

### Packet Files
- `tasks/P3-T03-TASK-0013/task.md`
- `tasks/P3-T01-TASK-0011/results.md` — result.json schema from run.js

## Adapter Context
- **Primary Adapter:** code_adapter
- **Secondary Adapters:** none
- **Adapter Rationale:** Pure Python file I/O module

## Excluded Context
- `docs/canonical/data_contracts.md` — Grain packet format is Phase 4, not this task

## Context Sufficiency Note
The run.js result.json contract and architecture §2.3 are sufficient to implement artifact collection.
