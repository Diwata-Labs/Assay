# Workflow Metrics

---

## Phase 1 — Foundation — CLOSED 2026-04-15

### Task Summary
| Task | Status | Notes |
|------|--------|-------|
| P1-T01 Python scaffold | done | Clean first run |
| P1-T02 TypeScript SDK scaffold | done | Clean |
| P1-T03 Grain packet schema | done | CP-001 created and applied |
| P1-T04 Data contract schemas | done | 17 tests, all passing |
| P1-T05 Developer tooling | done | Makefile + pre-commit; all targets green |

### Phase Health
- **Blockers encountered:** 0
- **Open questions resolved:** Q1–Q10 (all)
- **Change proposals applied:** CP-001 (data_contracts.md §1 replaced with Grain Sentinel payload)
- **Tests at phase close:** 18 pytest / 1 vitest — all passing
- **Lint/typecheck at phase close:** clean

### System Improvements Identified

**Fix now (before Phase 2):**
- GB-001: `grain task prepare` does not detect stub packet files — project owner patching Grain
- GB-003: Execute prompt is fragile in live AI sessions — project owner patching Grain

**Batch next phase:**
- GB-002: No lightweight packet mode for small tasks — design decision for Grain v2

**Ignore:**
- None

---

## Phase 2 — CLI Skeleton — CLOSED 2026-04-15

### Task Summary
| Task | Status | Notes |
|------|--------|-------|
| P2-T01 CLI entrypoint (Typer) | done | All 5 command groups wired |
| P2-T02 assay.toml config loader | done | ConfigError → exit 2; tomllib stdlib |
| P2-T03 Stub policy enforcement | done | No-op — satisfied by P2-T01 |
| P2-T04 Global flags | done | `--verbose` added (was missing from P2-T01) |
| P2-T05 CLI unit tests | done | 37 pytest / 1 vitest passing |

### Phase Health
- **Blockers encountered:** 0
- **Open questions resolved:** none new
- **Change proposals:** none
- **Tests at phase close:** 37 pytest / 1 vitest — all passing
- **Lint/typecheck at phase close:** clean

### System Improvements Identified

**Fix now (before Phase 3):**
- GB-005: Phase review/close should be a hard gate in `grain workflow next` — not just a `stop_reason`. Currently bypassable by updating `current_focus.md` manually. Should require an explicit `grain phase close` command before routing to the next phase.

**Batch next phase:**
- None

**Ignore:**
- None

---

## Phase 3 — Playwright + Docker Runner — CLOSED 2026-04-16

### Task Summary
| Task | Status | Notes |
|------|--------|-------|
| P3-T01 Playwright Docker image | done | Dockerfile + run.js + package.json; `docker build` deferred |
| P3-T02 Python runner module | done | `runner.run()` wraps subprocess Docker call; fully mocked in tests |
| P3-T03 Artifact collection | done | `collect_artifacts()` + `ArtifactBundle`; 7 tests |
| P3-T04 Wire assay run command | done | CLI exits 0/3/1 per outcome; 6 mock tests |
| P3-T05 Runner integration test | done | `docker build` + `assay run --target https://example.com` → exit 0, result.json + screenshot.png written |

### Phase Health
- **Blockers encountered:** 1 (P3-T05: Docker PATH not set in Claude Code session — resolved by adding fallback path lookup in runner.py; package.json version pin fixed from `^1.44.0` to `1.44.0`)
- **Open questions resolved:** none new
- **Change proposals:** none
- **Tests at phase close:** 56 pytest / 1 vitest — all passing
- **Lint/typecheck at phase close:** clean

### System Improvements Identified

**Fix now (before Phase 4):**
- None

**Batch next phase:**
- None

**Ignore:**
- None

---
