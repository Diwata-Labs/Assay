# Task: Implement API key validation middleware (X-Assay-Key)

## Metadata
- **ID:** P5-T03-TASK-0023
- **Status:** done
- **Phase:** Phase 5 — FastAPI Ingest Layer + Auth
- **Backlog:** P5-T03
- **Packet Path:** tasks/P5-T03-TASK-0023/
- **Dependencies:** P5-T01-TASK-0021 (key store / verify_key), P5-T02-TASK-0022 (FastAPI app)
- **Primary Adapter:** code_adapter
- **Secondary Adapters:** none

## Objective
Add `X-Assay-Key` header validation to the FastAPI ingest app. Requests with a valid active key pass through; requests with a missing or invalid key receive HTTP 401. Uses `verify_key()` from the key store module. The key store path is injected via app state so tests can override it.

## Why This Task Exists
All ingest requests must be authenticated per architecture §4 and CLI spec §2.5. This task gates the `POST /ingest` endpoint so unauthorized SDKs are rejected before payload processing.

## Scope
- `src/assay/ingest/app.py` — FastAPI dependency for key validation; key store path via app state
- `tests/test_ingest.py` — auth tests (valid key → 200, invalid → 401, missing → 401, revoked → 401)

## Constraints
- Header: `X-Assay-Key`
- Missing header → 401
- Invalid/revoked key → 401
- Valid active key → 200
- Key store path from app.state.key_store (testable without touching ~/.assay/keys.json)

## Escalation Conditions
- None

## Closure Requirements
- `results.md` and `handoff.md` complete before moving to review

## Reviewer Focus
- 401 on missing header, invalid key, revoked key
- Key store path injection via app.state is testable
