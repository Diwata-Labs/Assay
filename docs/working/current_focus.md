# Current Focus

## Current Phase
Phase 9 — Packaging + Distribution (complete)

---

## Active Focus

All 9 phases complete. Assay v0.1.0 is feature-complete:
- CLI: `assay run`, `assay serve`, `assay schedule add/list/remove/run`, `assay key create/list/revoke`
- FastAPI ingest endpoint with X-Assay-Key auth
- TypeScript browser SDK (ESM + CJS)
- APScheduler-based foreground scheduler
- 209 Python tests passing; 27 TypeScript tests passing
- pyproject.toml and package.json metadata complete; README.md with full install guide

---

## Active Constraints

- CP-003 pending: `assay schedule run` not yet in `data_contracts.md §5`
- Canonical docs require human approval before direct edits
