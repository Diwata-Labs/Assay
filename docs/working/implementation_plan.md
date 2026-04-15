# Implementation Plan

**Project:** Assay
**Status:** Active — Phase 3
**Last updated:** 2026-04-15

---

## Overview

9 phases, sequenced to build a shippable v1 end-to-end. Phases 1–6 are the critical path. Phases 7–9 are polish and distribution.

No phase should be started before its predecessor's exit criteria are satisfied.

---

## Phase 1 — Foundation (Scaffold + Contracts) — CLOSED 2026-04-15

**Goal:** Establish project structure, tooling, and data contracts before any implementation begins.

**Deliverables:**
- Python project scaffold: `pyproject.toml`, `src/assay/`, `tests/`
- TypeScript SDK scaffold: `sdk/`, `package.json`, `tsconfig.json`
- Grain task packet schema confirmed or proposed (resolve Q1 in open questions)
- SDK ingest payload schema
- API key store schema
- Schedule state schema
- Developer tooling: linting (ruff/mypy), formatting, pytest, vitest

**Exit criteria:** Project installs cleanly (`pip install -e .`); all schemas are defined and validated; no placeholder stubs; CI lint passes.

---

## Phase 2 — CLI Skeleton — CLOSED 2026-04-15

**Goal:** Implement the `assay` CLI entrypoint with all v1 commands wired up per stub policy (§5.1 of CLI spec).

**Deliverables:**
- `assay run` — wired (may delegate to not-implemented runner)
- `assay schedule add/list/remove` — wired
- `assay report` — wired
- `assay key create/list/revoke` — wired
- `assay serve` — wired
- `assay.toml` config parsing (with validation)
- All exit codes per CLI spec §3
- `--help` and `--version` working

**Exit criteria:** All commands exit with correct codes; no silent stubs; config parsing tested.

---

## Phase 3 — Playwright + Docker Runner

**Goal:** Implement the isolated test runner using Playwright inside Docker.

**Deliverables:**
- `Dockerfile` for Playwright runner image (Playwright + browsers)
- Python runner module: starts container, passes parameters, collects artifacts
- Artifact handling: screenshots, logs, pass/fail result extracted from container
- `assay run` fully functional end-to-end

**Exit criteria:** `assay run --target <url>` completes a real browser test inside Docker and writes at least one artifact to the output directory.

---

## Phase 4 — Task Packet Formatter

**Goal:** Implement the shared module that converts runner artifacts into Grain-compatible task packets.

**Deliverables:**
- `assay.formatter` Python module
- Schema-valid JSON packet output
- File naming: `assay-<ISO-timestamp>-<uuid>.json`
- Severity assignment logic (from test results)
- Integration with runner output

**Exit criteria:** `assay run` produces a schema-valid Grain task packet JSON file.

---

## Phase 5 — FastAPI Ingest Layer + Auth

**Goal:** Implement the ingest endpoint with API key authentication.

**Deliverables:**
- FastAPI app with `POST /ingest` endpoint
- API key validation middleware (`X-Assay-Key` header check)
- `assay key create/list/revoke` fully implemented (bcrypt, key store)
- `assay serve` starts the FastAPI server
- Ingest path: validate → parse → format → write packet
- HTTP 401 on invalid/missing key

**Exit criteria:** Valid key → 200 + packet written; invalid key → 401; `assay key` commands round-trip correctly.

---

## Phase 6 — TypeScript Browser SDK

**Goal:** Implement the browser SDK as a TypeScript npm package.

**Deliverables:**
- SDK init: `new AssaySDK({ apiKey, endpoint })`
- `sdk.capture({ comment? })` method
- Screenshot capture (canvas API or html2canvas)
- Metadata collection: URL, viewport, user agent, timestamp
- POST to ingest endpoint with `X-Assay-Key`
- npm package build (ESM + CJS outputs)
- Basic integration test (SDK → ingest → packet)

**Exit criteria:** Browser script initializes, calls `capture()`, ingest accepts it, a schema-valid packet is written to output.

---

## Phase 7 — Scheduler Implementation

**Goal:** Implement the scheduler for recurring test runs.

**Deliverables:**
- `assay schedule add/list/remove` fully implemented
- Schedule state persisted to `~/.assay/schedules.json`
- Cron expression parsing (APScheduler or equivalent)
- Scheduler loop runs when `assay schedule run` or equivalent is invoked
- Integration with runner

**Exit criteria:** Scheduled run executes automatically at specified time; state persists across CLI invocations.

---

## Phase 8 — Integration + End-to-End Testing

**Goal:** Validate the full system end-to-end across both primary paths.

**Deliverables:**
- E2E test: `assay run` → Docker → Playwright → packet (schema-valid)
- E2E test: SDK `capture()` → POST → ingest → packet (schema-valid)
- Auth rejection tests (401 on invalid key, all ingest endpoints)
- Config precedence tests
- Schema validation tests (all data contract schemas)

**Exit criteria:** All E2E and integration tests pass; no regressions across phases.

---

## Phase 9 — Packaging + Distribution

**Goal:** Make Assay installable and distributable for v1 release.

**Deliverables:**
- Python package published to PyPI (or install script documented)
- npm package published to npm registry
- Docker image build documented (or published to Docker Hub)
- `INSTALL.md` or equivalent — fresh install + first run walkthrough
- Version pinned in `pyproject.toml` and `package.json`

**Exit criteria:** Fresh install on a clean machine completes successfully; `assay run --target <url>` and SDK `capture()` both work on first run.

---

## Deferred (v2)

- Web UI / dashboard
- Bug bounty portal (internal + external verification workflow)
- Multi-user accounts
- OAuth / SSO
- SaaS hosting / managed infrastructure
- Database-backed output store
- Advanced analytics and reporting
