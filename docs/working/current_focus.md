# Current Focus

## Current Phase
Phase 3 — Playwright + Docker Runner

---

## Active Focus

Phase 2 closed. CLI skeleton complete — all commands on surface, config loader wired, stub policy enforced, 37 tests passing.

First task: P3-T01 — Write Dockerfile for the Playwright runner image.

---

## Immediate Priorities

1. P3-T01: Dockerfile (Playwright + browsers + deps)
2. P3-T02: Runner module (start container, pass params, stream output)
3. P3-T03: Artifact collection (screenshots, logs, pass/fail)
4. P3-T04: Wire `assay run` to runner module
5. P3-T05: Runner integration test (real Docker run against a test URL)

---

## Active Constraints

- Docker must be available in all environments that run the Playwright runner
- Every test run executes inside a fresh, ephemeral Docker container — no persistent container state
- `assay run` must exit 0 on success, 3 on test failure, 1 on runner error (cli_spec §3)
- Canonical docs require human approval before direct edits
