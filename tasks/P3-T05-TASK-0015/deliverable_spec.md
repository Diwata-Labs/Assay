# Deliverable Spec: P3-T05-TASK-0015

## Required Output

### New Files
- none

### Modified Files
- none (verification only)

## Acceptance Checklist
- [ ] `docker build -t assay-playwright runner/` exits 0
- [ ] `assay run --target https://example.com` exits 0
- [ ] Output directory contains `result.json` and `screenshot.png`
- [ ] `result.json` has `outcome: "pass"`
- [ ] review bundle complete in `results.md` and `handoff.md`

## Not Required
- Any code changes — this is a live integration verification
- CI configuration — deferred to Phase 5
