# Task: Implement packet file writer

## Metadata
- **ID:** P4-T02-TASK-0017
- **Status:** done
- **Phase:** Phase 4 — Task Packet Formatter
- **Backlog:** P4-T02
- **Packet Path:** tasks/P4-T02-TASK-0017/
- **Dependencies:** P4-T01-TASK-0016
- **Primary Adapter:** code_adapter
- **Secondary Adapters:** none

## Objective
Implement `src/assay/formatter/writer.py` — takes a Grain Sentinel payload dict and writes it as a JSON file to the configured output directory. Filename: `assay-<ISO-timestamp>-<uuid>.json`.

## Why This Task Exists
`format_packet()` (P4-T01) produces the payload dict in memory. This module persists it to disk so operators can run `grain verify ingest --payload <path>`.

## Scope
- `src/assay/formatter/writer.py` — `write_packet(packet, output_dir) -> Path`
- Creates output directory if it does not exist
- Filename derived from `packet["verified_at"]` and `packet["verification_id"]`
- Writes minified JSON (no indent for machine consumption)
- Returns the Path of the written file
- Unit tests in `tests/test_writer.py`

## Constraints
- Filename format: `assay-<verified_at_safe>-<verification_id>.json` where `verified_at_safe` strips colons/dots (filename-safe)
- Output directory created with `Path.mkdir(parents=True, exist_ok=True)`
- JSON written with `json.dumps` — stdlib only

## Escalation Conditions
- None
