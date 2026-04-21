# Task: Implement --help --version --config --verbose global flags

## Metadata
- **ID:** P2-T04-TASK-0009
- **Status:** done
- **Phase:** Phase 2 — CLI Skeleton
- **Backlog:** P2-T04
- **Packet Path:** tasks/P2-T04-TASK-0009/
- **Dependencies:** P2-T01-TASK-0006, P2-T02-TASK-0007
- **Primary Adapter:** code_adapter
- **Secondary Adapters:** none

## Objective
Ensure all four global flags from cli_spec.md §6 are present and working: `--help` (Typer auto), `--version` (done), `--config` (done), and `--verbose` (missing — must be added). `--verbose` should be accepted and stored on the context object for future commands to read.

## Why This Task Exists
cli_spec.md §6 defines four required global flags. Three were implemented in P2-T01/P2-T02. `--verbose` was not yet added.

## Scope
- Add `--verbose` boolean flag to the root app callback
- Store verbose state on `ctx.obj` (or as a separate context attribute)
- No actual verbose output in stubs — just accept the flag without error

## Constraints
- All four flags per cli_spec.md §6 must be present
- `--verbose` accepted globally, not per-command

## Escalation Conditions
- None
