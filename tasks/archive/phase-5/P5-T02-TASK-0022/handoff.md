# Handoff: P5-T02-TASK-0022

## Final State
FastAPI app with `POST /ingest` endpoint is implemented and tested; payload validation matches `data_contracts.md §2`.

## Review Bundle

### Packet Identity
- **Task ID:** P5-T02-TASK-0022
- **Phase:** Phase 5 — FastAPI Ingest Layer + Auth
- **Status:** review

### Outcome
- **Review Readiness:** ready
- **User Review State:** pending
- **Verification State:** not_run
- **Recommended Next Status:** review
- **Short Summary:** Ingest endpoint accepts and validates SDK payloads; auth and formatter wiring deferred to P5-T03 and P5-T04.

## What Was Built
- `src/assay/ingest/app.py` — FastAPI app, `IngestPayload` Pydantic model, `POST /ingest` handler returning `{"status": "accepted"}`
- `src/assay/ingest/__init__.py` — exports `app`
- `tests/test_ingest.py` — 18 tests covering valid payloads, missing fields, empty fields, invalid base64, non-positive viewport dimensions

## What Review Should Check
- Pydantic model field coverage against `data_contracts.md §2` (all required fields present, optional fields have correct defaults)
- `screenshot` base64 validation: uses `base64.b64decode(v, validate=True)` — PNG magic bytes not checked
- `captured_at` is a non-empty string check only, not strict ISO 8601 parsing

## What Was Not Done
- Auth middleware (`X-Assay-Key` header validation) — P5-T03
- Formatter wiring (ingest → format_packet → write_packet) — P5-T04
- `assay serve` wiring — P5-T05

## Known Issues or Follow-ups
- None

## Files Changed
- `src/assay/ingest/app.py` — new
- `src/assay/ingest/__init__.py` — updated
- `tests/test_ingest.py` — new

## Reviewer Notes
None.

## Closeout Intake

### Open Questions To Log
- None

### Proposal Candidates To Log
- None

### Follow-Ups To Log
- None
