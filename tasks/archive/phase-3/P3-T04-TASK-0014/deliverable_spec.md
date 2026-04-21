# Deliverable Spec: P3-T04-TASK-0014

## Required Output

### New Files
- `tests/test_run_command.py` — unit tests for `assay run` wiring

### Modified Files
- `src/assay/cli/main.py` — `run()` command: replace stub with real runner + artifact collection call

## Acceptance Checklist
- [ ] `assay run --target <url>` calls `runner.run()` and `collect_artifacts()`
- [ ] Outcome "pass" → exit 0
- [ ] Outcome "fail" → exit 3
- [ ] Outcome other → exit 1
- [ ] Missing `--target` → error message, exit 2
- [ ] `ArtifactError` → error message, exit 1
- [ ] All new tests passing
- [ ] Full test suite passing with no regressions
- [ ] `make lint` and `make typecheck` clean
- [ ] review bundle complete in `results.md` and `handoff.md`

## Not Required
- Grain packet formatting — Phase 4
- Live Docker execution — tested with mocks; integration in P3-T05
