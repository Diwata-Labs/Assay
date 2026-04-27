# Deliverable Spec: P1-T01-TASK-0001

## Required Output

### New Files

- `pyproject.toml` — project metadata, dependencies, ruff/mypy/pytest config
- `src/assay/__init__.py` — package init with `__version__ = "0.1.0"`
- `src/assay/config.py` — empty module placeholder
- `src/assay/cli/__init__.py` — empty package
- `src/assay/runner/__init__.py` — empty package
- `src/assay/ingest/__init__.py` — empty package
- `src/assay/formatter/__init__.py` — empty package
- `tests/__init__.py` — empty
- `tests/test_placeholder.py` — smoke test: import assay, assert `__version__` is set
- `.gitignore` — Python standard

### Modified Files

- None

## Acceptance Checklist

- [ ] `pip install -e ".[dev]"` exits 0
- [ ] `ruff check src/` exits 0 (no lint errors)
- [ ] `pytest tests/` exits 0 with at least 1 passed test
- [ ] Package layout matches subsystems in `docs/canonical/architecture.md`
- [ ] No implementation logic present — scaffold only
- [ ] No silent stubs — placeholders are empty `__init__.py`, not success-returning stubs
- [ ] Results recorded in `results.md`

## Not Required

- Any CLI command implementation
- TypeScript SDK scaffold (P1-T02)
- Data contract schema definitions (P1-T03, P1-T04)
- Developer tooling beyond ruff, mypy, pytest
- Makefile or justfile (optional, not required for acceptance)
