# Plan: P1-T01-TASK-0001

## Approach

Create a minimal but correctly structured Python project scaffold that matches the four subsystems defined in `architecture.md` (cli, runner, ingest, formatter). No implementation logic — only package layout, tooling config, and a passing smoke test.

---

## Step 1 — Create `pyproject.toml`

- `[project]` metadata: `name = "assay"`, `version = "0.1.0"`, `requires-python = ">=3.11"`
- `[project.scripts]`: `assay = "assay.cli:app"` (placeholder entrypoint)
- `[project.optional-dependencies]` dev group: `ruff`, `mypy`, `pytest`
- `[tool.ruff]`: lint target = `src/`
- `[tool.mypy]`: strict = true, packages = `["assay"]`
- `[tool.pytest.ini_options]`: `testpaths = ["tests"]`

---

## Step 2 — Create `src/assay/` package structure

Matches subsystems from `architecture.md`:

```
src/assay/
  __init__.py        # __version__ = "0.1.0"
  config.py          # empty module (no implementation)
  cli/
    __init__.py      # empty
  runner/
    __init__.py      # empty
  ingest/
    __init__.py      # empty
  formatter/
    __init__.py      # empty
```

No implementation logic. No stubs that return success. Empty `__init__.py` only.

---

## Step 3 — Create `tests/`

```
tests/
  __init__.py
  test_placeholder.py   # one passing smoke test
```

`test_placeholder.py` content: import assay, assert `assay.__version__` is a non-empty string.

---

## Step 4 — Create `.gitignore`

Python standard entries: `__pycache__/`, `*.pyc`, `.venv/`, `dist/`, `build/`, `.mypy_cache/`, `.pytest_cache/`, `*.egg-info/`, `.env`.

---

## Verification

- `pip install -e ".[dev]"` exits 0
- `ruff check src/` exits 0
- `pytest tests/` exits 0 with ≥1 passing test
- Package layout matches `architecture.md` subsystems
