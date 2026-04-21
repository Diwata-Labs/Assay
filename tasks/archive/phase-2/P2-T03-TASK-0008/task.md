# Task: Wire stub commands with policy enforcement

## Metadata
- **ID:** P2-T03-TASK-0008
- **Status:** done
- **Phase:** Phase 2 — CLI Skeleton
- **Backlog:** P2-T03
- **Packet Path:** tasks/P2-T03-TASK-0008/
- **Dependencies:** P2-T01-TASK-0006
- **Primary Adapter:** code_adapter
- **Secondary Adapters:** none

## Objective
Confirm all CLI commands exit with a non-zero code and print an explicit message when unimplemented, per cli_spec.md §4 (stub policy). Verify exit code assignments match §3. No silent zero-exit stubs permitted.

## Why This Task Exists
Stub policy is a hard contract: any unimplemented command that exits 0 silently would mask missing implementation and break downstream test assumptions.

## Scope
- Verify all 10 stub commands exit 1 with "not implemented" output
- Confirm exit code mapping: 1=general, 2=config, 3=test failure, 4=auth
- No new implementation — this is a verification + documentation task
- All stub policy requirements satisfied by P2-T01

## Constraints
- Exit codes per cli_spec.md §3 — no deviation
- "not implemented" message required per §4

## Escalation Conditions
- Any stub found to exit 0 silently
