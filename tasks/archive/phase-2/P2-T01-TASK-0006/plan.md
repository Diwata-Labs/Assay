# Plan: P2-T01-TASK-0006

## Approach

Add Typer to pyproject.toml, then implement `src/assay/cli/main.py` with a top-level `app` and five command groups/stubs. `schedule` and `key` are Typer sub-apps (command groups). `run`, `serve`, and `report` are direct commands. All stubs raise `typer.Exit(1)` after printing a not-implemented message. `--version` and `--config` are global options on the root app.

---

## Step 1 — Add typer dependency

Add `typer>=0.12` to `pyproject.toml` dependencies and reinstall with `pip install -e .`.

---

## Step 2 — Implement cli/main.py

Create `src/assay/cli/main.py` with:
- Root `app = typer.Typer()`
- `--version` callback option
- `--config` option stored via `typer.Context`
- `schedule_app` and `key_app` as sub-Typer apps added to root with `app.add_typer()`
- `run`, `serve`, `report` as stub commands on root app
- `schedule add`, `schedule list`, `schedule remove` as stubs on `schedule_app`
- `key create`, `key list`, `key revoke` as stubs on `key_app`

---

## Step 3 — Update pyproject.toml entrypoint

Confirm `[project.scripts]` points to `assay.cli.main:app` (not `assay.cli:app` as currently set).

---

## Step 4 — Write CLI tests

Add `tests/test_cli.py` using Typer's `CliRunner`:
- `--version` exits 0 and prints version string
- `--help` exits 0
- Each stub command exits 1 and prints a message

---

## Verification

`pip install -e .` succeeds. `assay --version` prints version. `assay run` exits 1 with "not implemented" message. All new tests pass. Full suite (18 existing + new) passes. `make lint` and `make typecheck` clean.
