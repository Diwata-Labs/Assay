# Task: Implement assay.toml config parsing with validation

## Metadata
- **ID:** P2-T02-TASK-0007
- **Status:** done
- **Phase:** Phase 2 — CLI Skeleton
- **Backlog:** P2-T02
- **Packet Path:** tasks/P2-T02-TASK-0007/
- **Dependencies:** P2-T01-TASK-0006
- **Primary Adapter:** code_adapter
- **Secondary Adapters:** none

## Objective
Implement `src/assay/config.py` — a module that loads and validates `assay.toml` from the standard locations (project-local `./assay.toml` then `~/.assay/config.toml`), validates the structure, and returns a typed config object. Wire the `--config` flag in the CLI to override the search path. Raise exit code 2 on config errors per cli_spec.md §3.

## Why This Task Exists
Commands in Phase 3+ need config values (docker image, output dir, serve host/port, key store path). This module is the single authoritative config loader so all commands consume it consistently.

## Scope
- `src/assay/config.py` — `AssayConfig` dataclass, `load_config(path)` function
- TOML parsing with `tomllib` (stdlib in Python 3.11+) — no new dependency needed
- Validation: required sections not enforced (all optional with defaults), but unknown keys raise ConfigError
- `--config` in CLI calls `load_config(path)` and stores result in Typer context
- `ConfigError` raises `typer.Exit(2)` when surfaced from CLI
- Tests for valid config, missing file (uses defaults), invalid TOML, unknown key

## Constraints
- Config structure per cli_spec.md §5: `[project]`, `[runner]`, `[output]`, `[serve]`, `[keys]` sections
- All fields optional — sensible defaults for everything
- Exit code 2 on config error (cli_spec.md §3)
- `tomllib` is stdlib in Python 3.11+ — no dependency to add

## Escalation Conditions
- None anticipated
