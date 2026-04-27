# Task: Implement assay.formatter module

## Metadata
- **ID:** P4-T01-TASK-0016
- **Status:** done
- **Phase:** Phase 4 — Task Packet Formatter
- **Backlog:** P4-T01
- **Packet Path:** tasks/P4-T01-TASK-0016/
- **Dependencies:** P3-T03-TASK-0013
- **Primary Adapter:** code_adapter
- **Secondary Adapters:** none

## Objective
Implement `src/assay/formatter/formatter.py` — converts an `ArtifactBundle` into a Grain Sentinel payload dict conforming to `data_contracts.md §1`. This is the core shared module used by both the runner path and the ingest path.

## Why This Task Exists
The Grain Sentinel payload is the primary output format of Assay. This module is the boundary between Assay's internal representation (`ArtifactBundle`) and the external contract (Grain payload JSON). P4-T02 writes the file; P4-T04 wires it into `assay run`.

## Scope
- `src/assay/formatter/__init__.py` — package init
- `src/assay/formatter/formatter.py` — `format_packet(bundle, task_id=None) -> dict`
- Populates all required fields: `verification_id`, `task_id`, `issue_type`, `severity`, `outcome`, `summary`
- Populates optional fields: `artifact_refs`, `verified_at`
- `followup_candidates` left empty in v1
- Unit tests in `tests/test_formatter.py`

## Constraints
- `verification_id`: UUID v4 (uuid stdlib)
- `task_id`: optional string; defaults to None for standalone runs
- `issue_type`: outcome fail → `"test_failure"`; outcome pass → `"bug_finding"` if error present, else `"test_failure"`; inconclusive → `"test_failure"`
- `severity`: fail → `"error"`; pass → `"info"`; inconclusive → `"warning"`
- `artifact_refs`: `[bundle.screenshot_path]` if present, else `[]`
- `verified_at`: `bundle.timestamp` if non-empty, else current UTC time in ISO 8601
- `summary`: human-readable one-liner derived from outcome + url + error

## Escalation Conditions
- None
