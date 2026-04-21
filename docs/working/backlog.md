# Backlog

**Project:** Assay
**Last updated:** 2026-04-21

Status values: `pending` | `ready` | `in_progress` | `blocked` | `done`

---

## Phase 1 — Foundation ✓ CLOSED (5 tasks — archived to tasks/archive/phase-1/)

## Phase 2 — CLI Skeleton ✓ CLOSED (5 tasks — archived to tasks/archive/phase-2/)

## Phase 3 — Playwright + Docker Runner ✓ CLOSED (5 tasks — archived to tasks/archive/phase-3/)

## Phase 4 — Task Packet Formatter ✓ CLOSED (5 tasks — archived to tasks/archive/phase-4/)

## Phase 5 — FastAPI Ingest Layer + Auth ✓ CLOSED (6 tasks — archived to tasks/archive/phase-5/)

---

## Phase 6 — TypeScript Browser SDK ✓ CLOSED (6 tasks — archived to tasks/archive/phase-6/)

---

## Phase 7 — Scheduler ✓ CLOSED (5 tasks)

| ID | Task | Status | Dependencies | Notes |
|----|------|--------|--------------|-------|
| P7-T01 | Implement schedule state persistence (`~/.assay/schedules.json`) | done | P1-T04 | 15 tests |
| P7-T02 | Implement `assay schedule add/list/remove` fully | done | P7-T01, P2-T03 | 12 tests; ScheduleConfig added to config |
| P7-T03 | Integrate cron expression parser (APScheduler) | done | P7-T01 | implemented in P7-T02; cron.py |
| P7-T04 | Implement scheduler loop (invoke runner at scheduled times) | done | P7-T02, P7-T03, P3-T04 | 8 tests; CP-003 filed |
| P7-T05 | Scheduler integration test | done | P7-T04 | 5 tests |

---

## Phase 8 — Integration + E2E Testing ✓ CLOSED (5 tasks)

| ID | Task | Status | Dependencies | Notes |
|----|------|--------|--------------|-------|
| P8-T01 | E2E: `assay run` → subprocess mock → schema-valid packet | done | P4-T05, P3-T05 | 5 tests |
| P8-T02 | E2E: SDK capture → ingest → schema-valid packet | done | P6-T06 | 7 tests |
| P8-T03 | Auth rejection E2E | done | P5-T06 | covered in P8-T02 (test_e2e_sdk.py) |
| P8-T04 | Config precedence tests | done | P2-T05 | 10 tests |
| P8-T05 | Cross-phase regression sweep | done | all phases | 209 pytest passing |

---

## Phase 9 — Packaging + Distribution ✓ CLOSED (4 tasks)

| ID | Task | Status | Dependencies | Notes |
|----|------|--------|--------------|-------|
| P9-T01 | Finalize Python package metadata | done | P8 complete | pyproject.toml: readme, license, authors, classifiers; README.md |
| P9-T02 | Finalize npm package metadata | done | P8 complete | package.json: author, license, keywords |
| P9-T03 | Document Docker runner image | done | P8 complete | Build instructions in README.md |
| P9-T04 | First-run installation guide | done | P9-T01–P9-T03 | README.md: requirements, quick start, SDK, dev setup |

---

## v0.2.0

---

## Phase 10 — Distribution + CI

| ID | Task | Status | Dependencies | Notes |
|----|------|--------|--------------|-------|
| P10-T01 | PyPI publish workflow (GitHub Actions release job) | pending | P9 complete | `python -m build` + twine; version from importlib.metadata |
| P10-T02 | GitHub Actions CI: pytest + ruff + mypy + vitest | pending | P9 complete | Runs on every push and PR |

---

## Phase 11 — Screenshot Persistence + `assay report`

| ID | Task | Status | Dependencies | Notes |
|----|------|--------|--------------|-------|
| P11-T01 | Save SDK screenshot to disk on ingest; populate artifact_refs | pending | P5 complete | `<packet-id>.png` in output dir |
| P11-T02 | Verify runner screenshot is copied + referenced in artifact_refs | pending | P3-T05 | Currently records temp path only |
| P11-T03 | Implement `assay report` command (table + json + filter) | pending | P4 complete | Reads assay-*.json; outcome table |

---

## Phase 12 — Grain Task Tagging + `assay submit`

| ID | Task | Status | Dependencies | Notes |
|----|------|--------|--------------|-------|
| P12-T01 | `assay run --task-id` flag; populate task_id in packet | pending | P4 complete | |
| P12-T02 | Grain auto-detection: read current_task.md / GRAIN_TASK_ID env | pending | P12-T01 | |
| P12-T03 | `assay submit --packet <path>` command + [grain] config section | pending | P12-T01 | |
| P12-T04 | `assay run --submit` one-step flag | pending | P12-T03 | |
| P12-T05 | SDK taskId passthrough to ingest payload | pending | P6 complete | Optional field in capture() |

---

## Phase 13 — Background Scheduler (Daemon Mode)

| ID | Task | Status | Dependencies | Notes |
|----|------|--------|--------------|-------|
| P13-T01 | `assay schedule start`: background process + PID file | pending | P7 complete | |
| P13-T02 | `assay schedule stop`: SIGTERM + PID cleanup | pending | P13-T01 | |
| P13-T03 | `assay schedule status`: running/stopped + next-run times | pending | P13-T01 | |
| P13-T04 | PID file locking; log file at ~/.assay/scheduler.log | pending | P13-T01 | |
