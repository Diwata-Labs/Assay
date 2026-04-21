# Backlog

**Project:** Assay
**Last updated:** 2026-04-20

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
