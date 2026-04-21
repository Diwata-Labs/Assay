# Deliverable Spec: P5-T02-TASK-0022

## Required Output

### New Files
- `src/assay/ingest/app.py` — FastAPI app, IngestPayload Pydantic model, POST /ingest handler
- `tests/test_ingest.py` — endpoint tests

### Modified Files
- `src/assay/ingest/__init__.py` — export `app`

## Acceptance Checklist
- [ ] `POST /ingest` returns 200 on valid payload
- [ ] `POST /ingest` returns 422 on missing required fields
- [ ] `POST /ingest` returns 422 on invalid base64 screenshot
- [ ] `POST /ingest` returns 422 on non-positive viewport dimensions
- [ ] Pydantic model covers all fields from `data_contracts.md §2`
- [ ] All new tests passing
- [ ] Full test suite passing with no regressions
- [ ] review bundle complete in `results.md` and `handoff.md`

## Not Required
- Auth middleware (P5-T03)
- Formatter wiring (P5-T04)
- `assay serve` wiring (P5-T05)
