# Current Focus

## Current Phase
Phase 10 — Distribution + CI (v0.2.0 start)

---

## Active Focus

v0.1.0 shipped (Phases 1–9 complete, pushed to main). Starting v0.2.0 — four phases planned:
- Phase 10: PyPI publish + GitHub Actions CI
- Phase 11: Screenshot persistence to disk + `assay report` command
- Phase 12: Grain task tagging (`--task-id`, auto-detect, `assay submit`)
- Phase 13: Background scheduler daemon (start/stop/status)

Grain integration (Phase 12) is the highest-priority new capability — allows Assay to be used inside any Grain project with zero manual wiring.

---

## Immediate Priorities

1. P10-T01: PyPI publish via GitHub Actions release workflow
2. P10-T02: CI workflow (pytest + ruff + mypy + vitest on every push/PR)
3. → Phase 11: screenshot persistence + assay report
4. → Phase 12: Grain task tagging + submit

---

## Active Constraints

- `assay report` is currently a stub (exit 1) — must be implemented before v0.2.0 ships
- SDK screenshot base64 from ingest is currently discarded — must be saved to disk (Phase 11)
- `assay run --task-id` does not exist yet — CP needed when implemented (Phase 12)
- Canonical docs require human approval before direct edits
