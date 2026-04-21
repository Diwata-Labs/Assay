# Task: Wire assay serve to start FastAPI server

## Metadata
- **ID:** P5-T05-TASK-0025
- **Status:** in_progress
- **Phase:** Phase 5 — FastAPI Ingest Layer + Auth
- **Backlog:** P5-T05
- **Packet Path:** tasks/P5-T05-TASK-0025/
- **Dependencies:** P5-T02-TASK-0022 (FastAPI app), P2-T03-TASK-0008 (CLI stubs)
- **Primary Adapter:** code_adapter
- **Secondary Adapters:** none

## Objective
Replace the `assay serve` CLI stub with a real implementation that starts the FastAPI ingest server via uvicorn using host/port from config (or CLI flags). The key store and output dir from config must be propagated to `app.state` before uvicorn starts.

## Why This Task Exists
`assay serve` is currently a stub returning exit 1. This task makes it functional so the ingest endpoint is reachable.

## Scope
- `src/assay/cli/main.py` — replace serve stub with uvicorn.run call; propagate config to app.state

## Constraints
- Host default: `127.0.0.1`, port default: `8000` (from config or CLI flags per cli_spec.md §2.5)
- `app.state.key_store` = `config.keys.store`
- `app.state.output_dir` = `config.output.directory`
- Uses uvicorn (already in deps)
- `assay serve` runs until interrupted (Ctrl-C) — no background/daemon mode

## Escalation Conditions
- None

## Closure Requirements
- `results.md` complete before moving to review

## Reviewer Focus
- Config values propagated to app.state before server starts
- CLI flags override config (host/port)
- No import of uvicorn at module level (import inside function to keep CLI fast)
