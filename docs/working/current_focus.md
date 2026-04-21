# Current Focus

## Current Phase
Phase 13 — v0.2.0 complete

---

## Active Focus

v0.2.0 shipped (Phases 10–13 complete). All four v0.2.0 phases done:
- Phase 10: GitHub Actions CI + PyPI release workflow ✓
- Phase 11: Screenshot persistence + `assay report` ✓
- Phase 12: Grain task tagging + `assay submit` ✓
- Phase 13: Background scheduler daemon ✓

250 pytest passing, ruff + mypy clean.

---

## v0.2.0 Summary

**New commands:**
- `assay report` — renders packet table; `--format json`, `--filter outcome=fail`
- `assay submit --packet <path>` — validates schema, copies to `[grain].output_path`
- `assay schedule start/stop/status` — background daemon with PID + log file

**New flags:**
- `assay run --task-id TASK-XXXX` — explicit Grain task tagging
- `assay run --submit` — run + submit in one step
- Auto-detection: `GRAIN_TASK_ID` env or `docs/working/current_task.md`

**Screenshot persistence:**
- SDK: `/ingest` saves `{verification_id}.png`; `artifact_refs` populated
- Runner: `screenshot.png` copied to `{verification_id}.png` in output dir

---

## Active Constraints

- Canonical docs require human approval before direct edits
- `assay schedule start` uses `os.fork()` — POSIX only (no Windows support)
- PyPI publish not yet triggered (needs a tagged release + PyPI trusted publisher setup)
