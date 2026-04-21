# Task: Runner integration test

## Metadata
- **ID:** P3-T05-TASK-0015
- **Status:** done
- **Phase:** Phase 3 — Playwright + Docker Runner
- **Backlog:** P3-T05
- **Packet Path:** tasks/P3-T05-TASK-0015/
- **Dependencies:** P3-T02-TASK-0012, P3-T04-TASK-0014
- **Primary Adapter:** code_adapter
- **Secondary Adapters:** none

## Objective
Build and run the Playwright Docker image against a real URL to confirm end-to-end: `docker build` produces a working image, `assay run --target <url>` calls it, the container writes result.json and screenshot.png, and the CLI exits with the correct code.

## Why This Task Exists
Unit tests in P3-T02/T03/T04 mock the Docker layer. This task verifies that the Dockerfile, run.js, and Python runner wiring all work together with real Docker execution before Phase 3 is closed.

## Scope
- `docker build -t assay-playwright runner/` — confirm image builds cleanly
- `assay run --target https://example.com` — confirm exit 0 and output files written
- `assay run --target https://httpstat.us/404` (or similar) — confirm non-zero exit on navigation error (optional)
- Document results in results.md

## Constraints
- Docker must be installed and the Docker daemon running
- Internet access required (Playwright fetches page)
- No new Python files required — this is a manual/scripted verification step

## Escalation Conditions
- Docker not installed in dev environment → blocker; task deferred until Docker available
