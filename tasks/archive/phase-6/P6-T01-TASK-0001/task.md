# Task: Implement SDK init — new AssaySDK({ apiKey, endpoint })

## Metadata
- **ID:** P6-T01-TASK-0001
- **Status:** done
- **Phase:** Phase 6 — TypeScript Browser SDK
- **Backlog:** P6-T01
- **Packet Path:** tasks/P6-T01-TASK-0001/
- **Dependencies:** none (scaffold from Phase 1 exists)
- **Primary Adapter:** code_adapter
- **Secondary Adapters:** none

## Objective
Replace the `AssaySDK` stub in `sdk/src/sdk.ts` with a real implementation that accepts `{ apiKey, endpoint }` at construction time, validates both fields are non-empty strings, and stores them for use by later methods. Export the class cleanly from `sdk/src/index.ts`. Write unit tests covering construction, validation errors, and field storage.

## Why This Task Exists
All subsequent SDK tasks (screenshot capture, metadata collection, `capture()` POST) depend on a correctly initialised SDK instance with a stored API key and endpoint URL.

## Scope
- `sdk/src/sdk.ts` — replace stub with real constructor + config validation
- `sdk/src/index.ts` — already exports `AssaySDK`; no change expected
- `sdk/tests/sdk.test.ts` — expand with init tests

## Constraints
- `apiKey`: required, non-empty string — printed once at `assay key create` time
- `endpoint`: required, non-empty string — URL of the ingest server
- Both stored as private readonly fields for use by `capture()` in P6-T04
- Framework-agnostic — no DOM or browser APIs used in this task
- No external runtime dependencies added in this task

## Escalation Conditions
- None

## Closure Requirements
- `results.md` and `handoff.md` complete before moving to review

## Reviewer Focus
- Validation errors thrown on empty/missing apiKey or endpoint
- Fields accessible internally for later tasks (private readonly)
- Existing vitest scaffold still passes
