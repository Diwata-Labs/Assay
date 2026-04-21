# Task: CLI unit tests: config, flags, exit codes

## Metadata
- **ID:** P2-T05-TASK-0010
- **Status:** done
- **Phase:** Phase 2 — CLI Skeleton
- **Backlog:** P2-T05
- **Packet Path:** tasks/P2-T05-TASK-0010/
- **Dependencies:** P2-T01-TASK-0006, P2-T02-TASK-0007, P2-T03-TASK-0008, P2-T04-TASK-0009
- **Primary Adapter:** code_adapter
- **Secondary Adapters:** none

## Objective
Ensure test coverage is complete for all Phase 2 CLI work: all stub exit codes, all global flags (including --verbose), config parsing paths, and exit code 2 from the CLI layer. All gaps filled; no untested flag or code path.

## Why This Task Exists
P2-T01–P2-T04 each added tests incrementally. This task does a final sweep to confirm coverage is complete and add any missing cases — particularly --verbose.

## Scope
- Add --verbose flag test to test_cli.py
- Confirm all 4 global flags are tested
- Confirm exit codes 1 and 2 are tested; document 3 and 4 as deferred
- No new implementation

## Constraints
- Tests must use typer.testing.CliRunner
- No mocking of filesystem — use tmp_path fixtures

## Escalation Conditions
- None
