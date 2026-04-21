# Task: Implement CLI entrypoint with Typer

## Metadata
- **ID:** P2-T01-TASK-0006
- **Status:** done
- **Phase:** Phase 2 — CLI Skeleton
- **Backlog:** P2-T01
- **Packet Path:** tasks/P2-T01-TASK-0006/
- **Dependencies:** P1-T01-TASK-0001
- **Primary Adapter:** code_adapter
- **Secondary Adapters:** none

## Objective
Implement the `assay` CLI entrypoint using Typer. Wire all five top-level commands (`run`, `schedule`, `serve`, `report`, `key`) as stubs that exit with a non-zero code and a "not implemented" message per stub policy (cli_spec.md §4). Implement `--version`, `--help`, and `--config` global flags. The entrypoint must be importable and the installed `assay` command must work.

## Why This Task Exists
Phase 2 goal is a working CLI skeleton with all commands on the surface and correct exit codes. P2-T02 through P2-T05 all depend on this entrypoint existing first.

## Scope
- Add `typer` to `pyproject.toml` dependencies
- Implement `src/assay/cli/main.py` with Typer app and all five commands as stubs
- `--version` prints `assay <version>` and exits 0
- `--config` global option accepted and stored in Typer context
- All stub commands print "not implemented" and exit 1
- `assay` entrypoint already wired in `pyproject.toml` — confirm it points to `assay.cli:app`

## Constraints
- Stub commands must not silently succeed (cli_spec.md §4)
- Exit codes per cli_spec.md §3: general error = 1, config error = 2, test failure = 3, auth error = 4
- No implementation logic in this task — stubs only
- `schedule`, `key` are command groups with subcommands; wire as Typer sub-apps

## Escalation Conditions
- Typer version conflict with existing dependencies
