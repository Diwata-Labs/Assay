# Task: Auth integration tests (valid key → 200, invalid → 401, missing → 401)

## Metadata
- **ID:** P5-T06-TASK-0026
- **Status:** in_progress
- **Phase:** Phase 5 — FastAPI Ingest Layer + Auth
- **Backlog:** P5-T06
- **Packet Path:** tasks/P5-T06-TASK-0026/
- **Dependencies:** P5-T03-TASK-0023 (auth middleware)
- **Primary Adapter:** code_adapter
- **Secondary Adapters:** none

## Objective
Write a dedicated `tests/test_auth.py` covering the full auth round-trip: key create → use → 200; missing key → 401; invalid key → 401; revoked key → 401. Also confirm that a valid ingest request produces a schema-valid output packet file.

## Why This Task Exists
The backlog specifies explicit auth integration test coverage as a phase exit criterion. Concentrating auth tests in their own file makes the auth contract clear and reviewable independently of payload validation.

## Scope
- `tests/test_auth.py` — new dedicated auth integration test file

## Constraints
- Tests use TestClient against the real app with tmp_path key store and output dir
- No mocking of auth logic
- All three required cases: valid → 200, invalid → 401, missing → 401

## Escalation Conditions
- None

## Closure Requirements
- `results.md` complete before moving to review

## Reviewer Focus
- All three auth outcomes covered with no mocking of the key store
- Revoked key correctly yields 401
- Packet file written on valid authenticated request
