# Deliverable Spec: P3-T03-TASK-0013

## Required Output

### New Files
- `src/assay/runner/artifacts.py` — ArtifactBundle dataclass + collect_artifacts() + ArtifactError
- `tests/test_artifacts.py` — unit tests with tmp_path fixtures

### Modified Files
- none

## Acceptance Checklist
- [ ] Valid result.json + screenshot → full ArtifactBundle
- [ ] Missing screenshot → screenshot_path is None
- [ ] Missing result.json + exit 0 → outcome "pass"
- [ ] Missing result.json + exit 1 → outcome "fail"
- [ ] Malformed result.json → ArtifactError raised
- [ ] All new tests passing
- [ ] Full test suite passing with no regressions
- [ ] `make lint` and `make typecheck` clean
- [ ] review bundle complete in `results.md` and `handoff.md`

## Not Required
- Grain packet formatting — Phase 4
- Any file copying or moving
