# Task: Set up developer tooling

## Metadata
- **ID:** P1-T05-TASK-0005
- **Status:** done
- **Phase:** Phase 1 — Foundation
- **Backlog:** P1-T05
- **Packet Path:** tasks/P1-T05-TASK-0005/
- **Dependencies:** P1-T01-TASK-0001, P1-T02-TASK-0002
- **Primary Adapter:** code_adapter
- **Secondary Adapters:** frontend_adapter

## Objective
Set up all developer tooling for the Assay project: pre-commit hooks (ruff lint, ruff format, mypy) and a Makefile with `test`, `lint`, and `typecheck` targets covering both the Python backend and the TypeScript SDK.

## Why This Task Exists
P1-T01 and P1-T02 created the scaffolds. This task wires up the quality gates so all future contributors run the same checks locally that CI will enforce.

## Scope
- `.pre-commit-config.yaml` with ruff (lint + format) and mypy hooks
- `Makefile` with `test`, `lint`, `typecheck` targets (Python + TS)
- `make test` runs pytest + vitest together
- `make lint` runs ruff check + ruff format --check
- `make typecheck` runs mypy + tsc --noEmit
- pre-commit installed into .venv
- Full `make test` passes green

## Constraints
- Python tooling uses the existing `.venv` (`python -m venv .venv` pattern from P1-T01)
- TypeScript tooling uses `npm` in `sdk/`
- No new runtime dependencies — dev tools only
- ruff config already in pyproject.toml; mypy config already in pyproject.toml

## Escalation Conditions
- pre-commit install fails due to environment issue
- mypy strict mode flags errors in existing code that need schema changes
