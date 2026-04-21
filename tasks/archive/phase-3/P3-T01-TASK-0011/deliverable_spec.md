# Deliverable Spec: P3-T01-TASK-0011

## Required Output

### New Files
- `runner/Dockerfile` — Playwright runner image definition
- `runner/run.js` — entry script: navigate, screenshot, write result.json
- `runner/package.json` — playwright dependency
- `runner/.dockerignore` — exclude node_modules

### Modified Files
- none

## Acceptance Checklist
- [ ] `docker build -t assay-playwright:latest ./runner` succeeds
- [ ] Container reads `ASSAY_TARGET_URL`, `ASSAY_OUTPUT_DIR` env vars
- [ ] `screenshot.png` written to output dir on success
- [ ] `result.json` written with `outcome`, `url`, `timestamp` fields
- [ ] Container exits 0 on success, 1 on error
- [ ] Full existing test suite passing with no regressions (Dockerfile doesn't affect Python tests)
- [ ] review bundle complete in `results.md` and `handoff.md`

## Not Required
- Multi-browser support (Chromium only in v1)
- `@playwright/test` framework — direct `playwright` API only
- Python in the runner image
- Automated test (deferred to P3-T05)
