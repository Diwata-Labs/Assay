# Agent Instructions — Assay

## Project Overview

Assay is an independent verification layer for software projects. It runs Playwright tests in Docker, captures browser screenshots via a TypeScript SDK, formats results into Grain-compatible task packets, and exposes a FastAPI ingest endpoint with API key auth.

- **PyPI package:** `assay-kit` (`uv tool install assay-kit`)
- **CLI entrypoint:** `assay` (via `src/assay/cli/main.py`)
- **Python source:** `src/assay/`
- **TypeScript SDK:** `sdk/`
- **Docker runner:** `runner/`
- **Tests:** `tests/` (pytest) + `sdk/` (vitest)

---

## Before Starting Any Task

1. Create a task packet directory: `tasks/P{phase}-T{n}-TASK-{id}/`
2. Populate `task.md`, `context.md`, `plan.md`, `deliverable_spec.md`, `results.md` from templates in `templates/`
3. Set task status to `ready` in `task.md`
4. Update `docs/working/current_task.md` with the task ID and path
5. Update `docs/working/backlog.md` to reflect `in_progress`

The current highest task ID is **TASK-0031**. Next is **TASK-0032**.

Never skip this step — even in resumed sessions or when the work seems straightforward.

---

## Commit Rules

- No `Co-Authored-By` lines of any kind
- Lowercase, concise commit messages
- Do not commit `.DS_Store`, `assay-output/`, or secrets

---

## Code Quality — Must Pass Before Every Commit

```bash
.venv/bin/ruff check .        # linting
.venv/bin/mypy src/assay      # type checking
.venv/bin/pytest              # 250 tests must pass
```

- Python 3.11+, strict mypy
- No inline comments unless the WHY is non-obvious
- Use `cast(list[dict[str, object]], ...)` over `# type: ignore[arg-type]` for mypy list issues
- Lazy-import APScheduler inside function bodies; patch `apscheduler.schedulers.blocking.BlockingScheduler` in tests

---

## Key Files

| File | Purpose |
|------|---------|
| `docs/working/current_focus.md` | Current phase and priorities |
| `docs/working/backlog.md` | All phases and task statuses |
| `docs/working/current_task.md` | Active task — keep updated |
| `docs/working/change_proposals.md` | Proposals pending human approval |
| `docs/working/tooling_notes.md` | Workflow friction log |
| `docs/canonical/data_contracts.md` | Authoritative schema + CLI spec |
| `src/assay/schemas/assay_payload.schema.json` | Output packet JSON schema |

---

## Canonical Docs Policy

`docs/canonical/` requires **human approval** before edits. File a change proposal in `docs/working/change_proposals.md` first.

---

## Output Packet Schema

Required fields: `verification_id`, `task_id`, `issue_type`, `severity`, `outcome`, `summary`
Optional fields: `artifact_refs`, `followup_candidates`, `verified_at`

`task_id` is optional for standalone runs; required for Grain-integrated runs.

---

## Current State

v0.2.0 complete and published to PyPI as `assay-kit`. 250 pytest passing. Next tasks are in `docs/working/backlog.md` under v0.3+.
