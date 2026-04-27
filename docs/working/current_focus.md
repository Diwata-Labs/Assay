# Current Focus

## Current Phase
Phase 14 — v0.2.0 start (HTML report, watch mode, SQLite store)

---

## Active Focus

v0.1.0 shipped to PyPI as `assay-kit` (Phases 1–13 complete). Starting v0.2.0 — three phases planned:
- Phase 14: `assay report --format html` (single-file, inline screenshots)
- Phase 15: `assay run --watch` (file watcher, debounce, re-run on change)
- Phase 16: SQLite output store (replace flat JSON, `assay store import`)

v0.3.0 planned:
- Phase 17: Web UI / Dashboard (served by `assay serve`, powered by SQLite)

---

## Immediate Priorities

1. P14-T01: `assay report --format html`
2. P14-T02: `--open` flag
3. → Phase 15: watch mode
4. → Phase 16: SQLite store

---

## Active Constraints

- Canonical docs require human approval before direct edits
- `assay schedule start` uses `os.fork()` — POSIX only (no Windows support)
- Phase 17 (web UI) depends on Phase 16 (SQLite) being complete first
- Grain has no `grain verify ingest` command yet — submitted packets sit unread (logged in tooling_notes.md)
