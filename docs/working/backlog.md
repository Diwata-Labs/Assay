# Backlog

**Project:** Assay
**Last updated:** 2026-04-15

Status values: `pending` | `ready` | `in_progress` | `blocked` | `done`

---

## Phase 1 — Foundation

| ID | Task | Status | Dependencies | Notes |
|----|------|--------|--------------|-------|
| P1-T01 | Initialize Python project scaffold (`pyproject.toml`, `src/assay/`, `tests/`) | done | none | First task — unblock everything else |
| P1-T02 | Initialize TypeScript SDK scaffold (`sdk/`, `package.json`, `tsconfig.json`) | done | none | Can run parallel to P1-T03 |
| P1-T03 | Confirm or draft Grain task packet schema | done | none | Resolves open question Q1 |
| P1-T04 | Define and validate all data contract schemas (key store, schedule state, ingest payload) | done | P1-T03 | Q1 resolved, Q10 decided |
| P1-T05 | Set up developer tooling (ruff, mypy, pytest, vitest, pre-commit) | done | P1-T01, P1-T02 | |

---

## Phase 2 — CLI Skeleton

| ID | Task | Status | Dependencies | Notes |
|----|------|--------|--------------|-------|
| P2-T01 | Implement CLI entrypoint with Click or Typer | pending | P1-T01 | Choose framework (see Q2) |
| P2-T02 | Implement `assay.toml` config parsing with validation | pending | P2-T01 | |
| P2-T03 | Wire all commands with stub policy enforcement (exit codes per spec §3, §5.1) | pending | P2-T01 | No silent stubs |
| P2-T04 | Implement `--help`, `--version`, `--config` global flags | pending | P2-T01 | |
| P2-T05 | CLI unit tests (config parsing, flag handling, exit codes) | pending | P2-T01–P2-T04 | |

---

## Phase 3 — Playwright + Docker Runner

| ID | Task | Status | Dependencies | Notes |
|----|------|--------|--------------|-------|
| P3-T01 | Write `Dockerfile` for Playwright runner image | pending | P1-T01 | Playwright + browsers + deps |
| P3-T02 | Implement runner module (start container, pass params, stream output) | pending | P3-T01 | |
| P3-T03 | Implement artifact collection (screenshots, logs, pass/fail from container) | pending | P3-T02 | |
| P3-T04 | Wire `assay run` to runner module | pending | P3-T02, P2-T03 | |
| P3-T05 | Runner integration test (real Docker run against a test URL) | pending | P3-T04 | Requires Docker in CI |

---

## Phase 4 — Task Packet Formatter

| ID | Task | Status | Dependencies | Notes |
|----|------|--------|--------------|-------|
| P4-T01 | Implement `assay.formatter` module (runner artifacts → Grain packet) | pending | P1-T03, P1-T04 | Core shared module |
| P4-T02 | Implement packet file writer (naming, output dir, JSON serialization) | pending | P4-T01 | |
| P4-T03 | Implement severity assignment logic | pending | P4-T01 | Simple rules initially |
| P4-T04 | Integrate formatter with runner output path | pending | P4-T01, P3-T03 | |
| P4-T05 | Schema validation tests for packet output | pending | P4-T02 | |

---

## Phase 5 — FastAPI Ingest Layer + Auth

| ID | Task | Status | Dependencies | Notes |
|----|------|--------|--------------|-------|
| P5-T01 | Implement `assay key create/list/revoke` commands (bcrypt, key store) | pending | P2-T01, P1-T04 | Key store on filesystem |
| P5-T02 | Implement FastAPI app with `POST /ingest` endpoint | pending | P4-T01 | |
| P5-T03 | Implement API key validation middleware (`X-Assay-Key`) | pending | P5-T01, P5-T02 | 401 on invalid/missing |
| P5-T04 | Wire ingest → formatter → packet write | pending | P5-T02, P4-T01 | |
| P5-T05 | Wire `assay serve` to start FastAPI server | pending | P5-T02, P2-T03 | |
| P5-T06 | Auth integration tests (valid key → 200, invalid → 401, missing → 401) | pending | P5-T03 | |

---

## Phase 6 — TypeScript Browser SDK

| ID | Task | Status | Dependencies | Notes |
|----|------|--------|--------------|-------|
| P6-T01 | Implement SDK init: `new AssaySDK({ apiKey, endpoint })` | pending | P1-T02, P1-T04 | |
| P6-T02 | Implement screenshot capture (canvas API or html2canvas) | pending | P6-T01 | Resolve Q3 |
| P6-T03 | Implement metadata collection (URL, viewport, user agent, timestamp) | pending | P6-T01 | |
| P6-T04 | Implement `capture({ comment? })` method with POST to ingest | pending | P6-T01–P6-T03 | |
| P6-T05 | Build npm package (ESM + CJS outputs, tsconfig, package.json) | pending | P6-T04 | |
| P6-T06 | SDK → ingest integration test | pending | P6-T04, P5-T04 | |

---

## Phase 7 — Scheduler

| ID | Task | Status | Dependencies | Notes |
|----|------|--------|--------------|-------|
| P7-T01 | Implement schedule state persistence (`~/.assay/schedules.json`) | pending | P1-T04 | |
| P7-T02 | Implement `assay schedule add/list/remove` fully | pending | P7-T01, P2-T03 | |
| P7-T03 | Integrate cron expression parser (APScheduler or equivalent, resolve Q4) | pending | P7-T01 | |
| P7-T04 | Implement scheduler loop (invoke runner at scheduled times) | pending | P7-T02, P7-T03, P3-T04 | |
| P7-T05 | Scheduler integration test | pending | P7-T04 | |

---

## Phase 8 — Integration + E2E Testing

| ID | Task | Status | Dependencies | Notes |
|----|------|--------|--------------|-------|
| P8-T01 | E2E: `assay run` → Docker → Playwright → schema-valid packet | pending | P4-T05, P3-T05 | |
| P8-T02 | E2E: SDK capture → ingest → schema-valid packet | pending | P6-T06 | |
| P8-T03 | Auth rejection E2E (all ingest endpoints) | pending | P5-T06 | |
| P8-T04 | Config precedence tests | pending | P2-T05 | |
| P8-T05 | Cross-phase regression sweep | pending | all phases | |

---

## Phase 9 — Packaging + Distribution

| ID | Task | Status | Dependencies | Notes |
|----|------|--------|--------------|-------|
| P9-T01 | Finalize Python package metadata, publish to PyPI or document install | pending | P8 complete | |
| P9-T02 | Finalize npm package, publish to npm or document install | pending | P8 complete | |
| P9-T03 | Document or publish Docker runner image | pending | P8 complete | |
| P9-T04 | Write first-run installation guide | pending | P9-T01–P9-T03 | |
