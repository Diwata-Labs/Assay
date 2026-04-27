# Task: Wire ingest → formatter → packet write

## Metadata
- **ID:** P5-T04-TASK-0024
- **Status:** in_progress
- **Phase:** Phase 5 — FastAPI Ingest Layer + Auth
- **Backlog:** P5-T04
- **Packet Path:** tasks/P5-T04-TASK-0024/
- **Dependencies:** P5-T02-TASK-0022 (FastAPI app), P4-T01-TASK-0016 (formatter)
- **Primary Adapter:** code_adapter
- **Secondary Adapters:** none

## Objective
Add `format_sdk_packet()` to `assay.formatter.formatter` to convert an SDK `IngestPayload` into a Grain-compatible packet dict. Wire the `POST /ingest` handler to call `format_sdk_packet()` then `write_packet()` after auth passes, writing the packet to the configured output directory.

## Why This Task Exists
The ingest endpoint currently returns `{"status": "accepted"}` without writing any output. This task closes the ingest path so a valid SDK capture produces a Grain task packet file on disk.

## Scope
- `src/assay/formatter/formatter.py` — add `format_sdk_packet(payload: IngestPayload) -> dict`
- `src/assay/ingest/app.py` — call formatter and writer after auth; output dir from `app.state.output_dir`
- `tests/test_ingest.py` — add test confirming a packet file is written on valid request
- `tests/test_formatter.py` — add tests for `format_sdk_packet`

## Constraints
- `issue_type`: `screenshot_evidence` for SDK captures (per `data_contracts.md §1`)
- `severity`: `info` default (per spec)
- `outcome`: `inconclusive` (capture requires human review)
- `artifact_refs`: `[]`
- `task_id`: `null` (standalone capture)
- `verified_at`: use `payload.captured_at`
- Output dir from `app.state.output_dir` (default `./assay-output`)

## Escalation Conditions
- None

## Closure Requirements
- `results.md` and `handoff.md` complete before moving to review

## Reviewer Focus
- Packet file written to disk on valid ingest request
- `format_sdk_packet` field mapping matches `data_contracts.md §1`
- Output dir injected via app.state (testable)
