# Deliverable Spec: P4-T01-TASK-0016

## Required Output

### New Files
- `src/assay/formatter/__init__.py` — package init
- `src/assay/formatter/formatter.py` — `format_packet()` function
- `tests/test_formatter.py` — unit tests

### Modified Files
- none

## Acceptance Checklist
- [ ] `format_packet(bundle)` returns dict with all required Grain Sentinel fields
- [ ] `verification_id` is a valid UUID v4 string
- [ ] `task_id` is None by default; accepts optional string
- [ ] `issue_type` correct for pass/fail/inconclusive outcomes
- [ ] `severity` correct for pass/fail/inconclusive outcomes
- [ ] `artifact_refs` contains screenshot_path when present
- [ ] `verified_at` uses bundle.timestamp when set, current UTC otherwise
- [ ] All new tests passing
- [ ] Full test suite passing with no regressions
- [ ] `make lint` and `make typecheck` clean
- [ ] review bundle complete in `results.md` and `handoff.md`

## Not Required
- File writing — P4-T02
- Integration with `assay run` — P4-T04
