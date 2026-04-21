# Implementation Plan

**Project:** Assay
**Status:** Active — v0.2.0 in planning (Phase 10)
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

## Phase 5 — FastAPI Ingest Layer + Auth — CLOSED 2026-04-20

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

## Phase 6 — TypeScript Browser SDK — CLOSED 2026-04-20

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

## Phase 7 — Scheduler Implementation — CLOSED 2026-04-18

**Goal:** Implement the scheduler for recurring test runs.

**Deliverables:**
- `assay schedule add/list/remove` fully implemented
- Schedule state persisted to `~/.assay/schedules.json`
- Cron expression parsing (APScheduler or equivalent)
- Scheduler loop runs when `assay schedule run` or equivalent is invoked
- Integration with runner

**Exit criteria:** Scheduled run executes automatically at specified time; state persists across CLI invocations.

---

## Phase 8 — Integration + End-to-End Testing — CLOSED 2026-04-21

**Goal:** Validate the full system end-to-end across both primary paths.

**Deliverables:**
- E2E test: `assay run` → subprocess-mocked Docker → schema-valid packet ✓
- E2E test: SDK `capture()` → POST → ingest → schema-valid packet ✓
- Auth rejection E2E tests ✓
- Config precedence tests ✓
- Cross-phase regression sweep: 209 pytest passing ✓

**Exit criteria:** All E2E and integration tests pass; no regressions across phases. ✓ MET

---

## Phase 9 — Packaging + Distribution — CLOSED 2026-04-21

**Goal:** Make Assay installable and distributable for v1 release.

**Deliverables:**
- Python package metadata complete (pyproject.toml: readme, license, authors, classifiers) ✓
- npm package metadata complete (package.json: author, license, keywords) ✓
- Docker image build documented in README ✓
- README.md with install + first-run walkthrough ✓

**Exit criteria:** `pip install assay` installs cleanly; CLI, SDK, and Docker runner all documented. ✓ MET

**Exit criteria:** Fresh install on a clean machine completes successfully; `assay run --target <url>` and SDK `capture()` both work on first run.

---

---

## v0.2.0 — Cross-Project Usability + Grain Integration

Goal: make Assay installable in any project with `pip install assay`, integrate deeply with Grain workflows (task tagging, auto-detection, submit), implement `assay report`, screenshot persistence, background scheduling, and CI.

---

## Phase 10 — Distribution + CI

**Goal:** Make Assay installable anywhere without cloning the repo, and automate test runs on every push.

**Deliverables:**
- `python -m build` + publish workflow to PyPI (via GitHub Actions release job)
- GitHub Actions CI: `pytest` + `ruff` + `mypy` on every push/PR; `vitest` on SDK changes
- `.github/workflows/ci.yml` and `.github/workflows/release.yml`
- Version sourced from package metadata (`importlib.metadata`) so `assay --version` always reflects the installed tag

**Exit criteria:** `pip install assay` works from PyPI; CI is green on main; a tagged release triggers the PyPI job.

---

## Phase 11 — Screenshot Persistence + `assay report`

**Goal:** Screenshots are saved as real files alongside every packet; results are readable without opening JSON.

**Deliverables:**
- **SDK screenshot persistence:** `POST /ingest` saves the base64 screenshot to `assay-output/<packet-id>.png` and sets `artifact_refs` in the packet to the saved file path
- **Runner screenshot:** verify `screenshot.png` from Docker output is copied into the packet output directory and referenced in `artifact_refs` (it currently records only the temp path)
- **`assay report` command:** reads all `assay-*.json` from output dir, renders a table (id, outcome, severity, summary, screenshot ✓/✗, verified_at)
- `assay report --format json` for machine-readable output
- `assay report --filter outcome=fail` for quick filtering
- Tests: screenshot file written on ingest; artifact_refs populated; report renders correct rows

**Exit criteria:** After `assay run` or SDK `capture()`, the output directory contains both the packet JSON and a `<packet-id>.png` screenshot; `assay report` lists it with a screenshot indicator.

---

## Phase 12 — Grain Task Tagging + `assay run --task-id`

**Goal:** Assay runs can be explicitly or automatically tagged with the active Grain task ID, and the resulting packet can be submitted back to Grain.

**Deliverables:**
- `assay run --task-id TASK-0070`: populates `task_id` field in the output packet
- Grain auto-detection: if `docs/working/current_task.md` exists in cwd (or `GRAIN_TASK_ID` env var is set), auto-populate `task_id` without requiring the flag
- `assay submit --packet <path>`: validates the packet, then copies it to a configurable Grain-visible location
- `[grain]` section in `assay.toml`: `project_root`, `output_path`
- `assay run --submit` flag: run + submit in one step
- SDK `capture()` accepts an optional `taskId` field passed through to the ingest payload
- Grain project quickstart section in README
- Tests covering auto-detect, submit, `--task-id` flag, and SDK taskId passthrough

**Exit criteria:** In a Grain project directory, `assay run --target <url>` auto-tags the packet with the current task ID; `assay run --submit` places the packet where Grain can pick it up.

---

## Phase 13 — Background Scheduler (Daemon Mode)

**Goal:** `assay schedule run` can operate as a background daemon — start, stop, and query status without occupying a terminal.

**Deliverables:**
- `assay schedule start`: launches scheduler as background process, writes PID to `~/.assay/scheduler.pid`
- `assay schedule stop`: sends SIGTERM to the PID, cleans up
- `assay schedule status`: running / stopped + next-run time per schedule
- PID file locking to prevent double-start
- Log file at `~/.assay/scheduler.log`
- Tests for start/stop/status lifecycle; daemon isolation via subprocess mock

**Exit criteria:** `assay schedule start` returns immediately; `assay schedule status` shows running; `assay schedule stop` terminates cleanly; double-start is rejected.

---

## Deferred (v0.3+ / v2)

- Web UI / dashboard
- Bug bounty portal (internal + external verification workflow)
- Multi-user accounts
- OAuth / SSO
- SaaS hosting / managed infrastructure
- Database-backed output store
- Advanced analytics and reporting
- `assay report` HTML view
