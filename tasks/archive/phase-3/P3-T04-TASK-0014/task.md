# Task: Wire assay run to runner module

## Metadata
- **ID:** P3-T04-TASK-0014
- **Status:** done
- **Phase:** Phase 3 — Playwright + Docker Runner
- **Backlog:** P3-T04
- **Packet Path:** tasks/P3-T04-TASK-0014/
- **Dependencies:** P3-T02-TASK-0012, P3-T03-TASK-0013
- **Primary Adapter:** code_adapter
- **Secondary Adapters:** none

## Objective
Replace the `_NOT_IMPLEMENTED` stub in the `assay run` CLI command with a real implementation that calls `runner.run()`, then `collect_artifacts()`, prints a summary line, and exits with the correct code (0=pass, 3=fail, 1=inconclusive/error).

## Why This Task Exists
`assay run` is the primary user-facing command. P3-T02 and P3-T03 built the underlying modules; this task wires them together so the CLI is end-to-end functional (modulo Docker availability).

## Scope
- Modify `src/assay/cli/main.py` `run()` command: call `runner.run()`, call `collect_artifacts()`, print outcome, exit with correct code
- Add `tests/test_run_command.py`: unit tests mocking `runner.run` and `collect_artifacts`
- Correct exit codes per cli_spec §3: 0=pass, 1=general error/inconclusive, 3=test failure

## Constraints
- `--target` is required; error with message if omitted
- Config object on `ctx.obj` provides `runner.docker_image` and `output.directory`
- Must not import Docker or call subprocess in CLI layer — delegate entirely to `runner.run()`
- `ArtifactError` from artifact collection maps to exit code 1

## Escalation Conditions
- None
