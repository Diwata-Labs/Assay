# Handoff: P1-T01-TASK-0001

## Final State
Python project scaffold created, installed cleanly, lint passes, and smoke test passes.

## Review Bundle

### Packet Identity
- **Task ID:** P1-T01-TASK-0001
- **Phase:** Phase 1 — Foundation
- **Status:** review

### Outcome
- **Review Readiness:** ready
- **Recommended Next Status:** done
- **User Review State:** approved
- **Short Summary:** Scaffold installs, ruff passes, pytest passes — all acceptance criteria met.

## What Was Built
- `pyproject.toml` — project metadata, dev deps, `setuptools.build_meta` backend, ruff/mypy/pytest config
- `src/assay/` package with four subsystem packages: `cli/`, `runner/`, `ingest/`, `formatter/`
- `src/assay/__init__.py` with `__version__ = "0.1.0"`
- `src/assay/config.py` empty module placeholder
- `tests/test_placeholder.py` smoke test — imports assay, asserts `__version__` is set
- `.gitignore` Python standard + `.venv*/`

## What Review Should Check
- Package layout matches the four subsystems in `docs/canonical/architecture.md` (cli, runner, ingest, formatter)
- No implementation logic present in any module
- `pyproject.toml` script entrypoint `assay = "assay.cli:app"` is a placeholder — `assay.cli` has no `app` object yet; this is expected and intentional for Phase 2
- Build backend is `setuptools.build_meta` (not `setuptools.backends.legacy:build`) — note this in review; both are correct, the change was for venv compatibility

## What Was Not Done
- TypeScript SDK scaffold (P1-T02 — separate task)
- Grain/data contract schema definition (P1-T03, P1-T04 — separate tasks)
- Any CLI implementation (Phase 2)
- Makefile / justfile (optional per deliverable spec, deferred)

## Known Issues or Follow-ups
- `assay` CLI entrypoint will fail if invoked (`assay.cli` has no `app`) — this is intentional; Phase 2 will implement it. Stub policy compliance: entrypoint is absent from working command surface, not a silent success.

## Files Changed
- `pyproject.toml` — new
- `src/assay/__init__.py` — new
- `src/assay/config.py` — new
- `src/assay/cli/__init__.py` — new
- `src/assay/runner/__init__.py` — new
- `src/assay/ingest/__init__.py` — new
- `src/assay/formatter/__init__.py` — new
- `tests/__init__.py` — new
- `tests/test_placeholder.py` — new
- `.gitignore` — new

## Reviewer Notes
Verify the three checks independently: `pip install -e ".[dev]"`, `ruff check src/`, `pytest tests/`. All should exit 0. The `.venv/` directory at project root is the local dev environment — not committed.

## Closeout Intake

### Open Questions To Log
- None

### Proposal Candidates To Log
- None

### Follow-ups To Log
- P1-T02: TypeScript SDK scaffold — can begin now, no dependency on this task
- P1-T03: Confirm Grain task packet schema (resolves open question Q1)
