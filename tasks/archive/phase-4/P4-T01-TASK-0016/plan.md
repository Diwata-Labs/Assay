# Plan: P4-T01-TASK-0016

## Approach

`format_packet(bundle, task_id=None)` reads the ArtifactBundle fields and returns a plain dict matching the Grain Sentinel payload schema. UUID and datetime generation use stdlib only. Severity and issue_type are derived from `bundle.outcome`. Tests cover all outcome paths and the optional task_id field.

---

## Step 1 — Create formatter package

Create `src/assay/formatter/__init__.py` (empty, marks as package) and `formatter.py` with `format_packet()`.

---

## Step 2 — Implement format_packet

Build the dict:
- `verification_id`: `str(uuid.uuid4())`
- `task_id`: passed-through or None
- `issue_type`: fail/inconclusive → `"test_failure"`; pass → `"bug_finding"` if error, else `"test_failure"` (runner always produces test_failure; bug_finding is SDK path)
- `severity`: fail → `"error"`; pass → `"info"`; inconclusive → `"warning"`
- `outcome`: from bundle.outcome
- `summary`: e.g. `"pass: https://example.com"` or `"fail: navigation timeout"`
- `artifact_refs`: `[bundle.screenshot_path]` if non-None, else `[]`
- `verified_at`: `bundle.timestamp` if non-empty, else `datetime.utcnow().isoformat() + "Z"`
- `followup_candidates`: `[]`

---

## Step 3 — Write tests

- Pass outcome → correct issue_type/severity/summary
- Fail outcome with error → correct fields
- Inconclusive → warning severity
- Screenshot present → in artifact_refs
- task_id passed → present in output
- verified_at falls back to current time when bundle.timestamp empty

---

## Verification

`make test` 62+ passing. `make lint` and `make typecheck` clean.
