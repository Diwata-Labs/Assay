# Task: Implement FastAPI ingest app with POST /ingest endpoint

## Metadata
- **ID:** P5-T02-TASK-0022
- **Status:** done
- **Phase:** Phase 5 — FastAPI Ingest Layer + Auth
- **Backlog:** P5-T02
- **Packet Path:** tasks/P5-T02-TASK-0022/
- **Dependencies:** P4-T01-TASK-0016 (formatter), P5-T01-TASK-0021 (key store)
- **Primary Adapter:** code_adapter
- **Secondary Adapters:** none

## Objective
Implement `src/assay/ingest/app.py` — a FastAPI application exposing `POST /ingest`. The endpoint validates the SDK ingest payload per `data_contracts.md §2` using Pydantic and returns `{"status": "accepted"}`. Auth middleware (P5-T03) and formatter wiring (P5-T04) are deferred to their own tasks.

## Why This Task Exists
The ingest endpoint is the core of the FastAPI layer. P5-T03 (auth middleware) and P5-T04 (formatter wiring) both depend on this endpoint existing and accepting valid payloads.

## Scope
- `src/assay/ingest/app.py` — FastAPI app, Pydantic payload model, `POST /ingest` handler
- `src/assay/ingest/__init__.py` — export `app`
- `tests/test_ingest.py` — endpoint tests via `httpx` TestClient

## Constraints
- Payload schema from `data_contracts.md §2`
- `captured_at`: required, non-empty ISO 8601 string
- `url`: required, non-empty string
- `viewport.width` / `viewport.height`: required, positive integers
- `user_agent`: required, non-empty string
- `screenshot`: required, non-empty string (base64 PNG — validate as valid base64)
- `user_comment`: optional; null or omitted accepted
- `metadata`: optional object
- Invalid payloads → 422 (FastAPI default Pydantic validation error)
- No auth in this task — auth is P5-T03

## Escalation Conditions
- None

## Closure Requirements

Before the packet can move to review, the task artifacts must include:

- `results.md` with current task status, review readiness, recommended next status, files changed, summary, test results, efficiency metrics, review notes, deliverable checklist, and blockers
- `handoff.md` with packet identity, phase, status, review readiness, recommended next status, summary, what was built, what review should check, known issues or follow-ups, files changed, reviewer notes, and closeout intake

Before the packet can move from review to done, the review artifacts must include:

- explicit `open_questions_to_log`
- explicit `proposal_candidates_to_log`
- explicit `followups_to_log`

Use `None` when a category has no items.

## Reviewer Focus
- Pydantic model matches `data_contracts.md §2` field by field
- Base64 validation is present but not overly strict (PNG magic bytes not required at this stage)
- 422 on malformed payload; 200 on valid payload
