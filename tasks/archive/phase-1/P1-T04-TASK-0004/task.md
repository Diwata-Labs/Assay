# Task: Define and validate all data contract schemas

## Metadata
- **ID:** P1-T04-TASK-0004
- **Status:** done
- **Phase:** Phase 1 — Foundation
- **Backlog:** P1-T04
- **Packet Path:** tasks/P1-T04-TASK-0004/
- **Dependencies:** P1-T03-TASK-0003 (done)
- **Primary Adapter:** code_adapter
- **Secondary Adapters:** none

## Objective

Produce JSON Schema files for all data contracts defined in `docs/canonical/data_contracts.md`: the Grain Sentinel result payload, the SDK ingest payload, the API key store, and the schedule state. Each schema must validate a correct example and reject a malformed one via a test.

## Why This Task Exists

All downstream implementation tasks (formatter, ingest layer, CLI key management, scheduler) depend on stable, validated schemas. Writing them now as JSON Schema files with tests locks the contracts in machine-checkable form before any implementation begins.

See: `docs/canonical/data_contracts.md`, `docs/working/backlog.md` P1-T04.

## Scope

- `src/assay/schemas/` package with one JSON Schema file per contract:
  - `sentinel_payload.schema.json` — Grain Sentinel result payload (§1)
  - `sdk_ingest.schema.json` — SDK ingest payload (§2)
  - `key_store.schema.json` — API key store (§3)
  - `schedule_state.schema.json` — schedule state (§4)
- `src/assay/schemas/__init__.py` — loads and exposes schemas
- `tests/test_schemas.py` — one valid + one invalid example per schema (≥8 tests)
- Add `jsonschema` to `pyproject.toml` dependencies

## Constraints

- Schemas must reflect the approved contracts in `data_contracts.md` exactly
- `task_id` in `sentinel_payload.schema.json` must be nullable (Q10: optional, `null` for standalone)
- No implementation logic — schemas and validation tests only

## Escalation Conditions

- If a contract in `data_contracts.md` is ambiguous during schema authoring — surface as a change proposal, do not invent a resolution
