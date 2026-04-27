# Task: Initialize Python Project Scaffold

## Metadata
- **ID:** P1-T01-TASK-0001
- **Status:** done
- **Phase:** Phase 1 — Foundation
- **Backlog:** P1-T01
- **Packet Path:** tasks/P1-T01-TASK-0001/
- **Dependencies:** none
- **Primary Adapter:** code_adapter
- **Secondary Adapters:** none

## Objective

Create the Python project scaffold for Assay: `pyproject.toml`, `src/assay/` package layout, `tests/` directory, and basic developer tooling (linting, formatting, test runner). The scaffold must install cleanly and pass a lint check before this task is closed.

## Why This Task Exists

All Phase 1, 2, 3, 4, 5, and 7 work depends on a working Python project structure. This is the unblocking first task. Nothing else in the Python backend can start until this scaffold is in place.

See: `docs/working/implementation_plan.md` Phase 1, `docs/working/backlog.md` P1-T01.

## Scope

- `pyproject.toml` with project metadata, dependencies section, and tool config (ruff, mypy, pytest)
- `src/assay/__init__.py` — package init, version string
- `src/assay/cli/` — placeholder package for CLI commands
- `src/assay/runner/` — placeholder package for Playwright runner
- `src/assay/ingest/` — placeholder package for FastAPI ingest layer
- `src/assay/formatter/` — placeholder package for task packet formatter
- `src/assay/config.py` — placeholder for config parsing
- `tests/__init__.py` and `tests/test_placeholder.py` — ensure test runner works
- `Makefile` or `justfile` with `lint`, `test`, `install` targets (optional but preferred)
- `.gitignore` appropriate for Python

## Constraints

- Must use `src/` layout (not flat layout) — consistent with `code_adapter` file patterns
- Placeholder packages must not silently succeed when called — they may be empty `__init__.py` only (not stubs that return success)
- No implementation logic in this task — scaffold only
- Tooling: ruff for linting/formatting, mypy for type checking, pytest for tests
- Python minimum version: 3.11

## Escalation Conditions

- If `pyproject.toml` dependency conflicts arise that block install
- If the chosen package layout conflicts with a CLI entrypoint requirement discovered during scaffolding
