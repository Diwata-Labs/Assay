# Task: Implement runner module

## Metadata
- **ID:** P3-T02-TASK-0012
- **Status:** done
- **Phase:** Phase 3 — Playwright + Docker Runner
- **Backlog:** P3-T02
- **Packet Path:** tasks/P3-T02-TASK-0012/
- **Dependencies:** P3-T01-TASK-0011
- **Primary Adapter:** code_adapter
- **Secondary Adapters:** none

## Objective
Implement `src/assay/runner/runner.py` — the Python module that starts the Playwright Docker container, passes target URL and suite name as environment variables, streams container output to stdout, waits for completion, and returns a `RunResult` dataclass containing the exit code and output directory path. Unit tests mock `subprocess`/Docker so no live Docker daemon is needed.

## Why This Task Exists
The runner module is the Python-side orchestrator for every `assay run` invocation. P3-T03 (artifact collection) and P3-T04 (`assay run` wiring) both depend on it.

## Scope
- `src/assay/runner/runner.py` — `RunResult` dataclass + `run()` function
- `run()` calls `docker run` via `subprocess.run`, mounts a temp output dir, passes env vars, streams output
- Returns `RunResult(exit_code, output_dir)` — caller handles artifact reading
- `tests/test_runner.py` — unit tests with mocked subprocess; no live Docker needed

## Constraints
- Container is ephemeral — fresh run per invocation (architecture §2.3)
- Image name defaults to `assay-playwright:latest`; overridable via config
- Output dir is a `tempfile.mkdtemp()` unless caller specifies one
- Must not import Docker SDK — use `subprocess` only for simplicity in v1

## Escalation Conditions
- None anticipated
