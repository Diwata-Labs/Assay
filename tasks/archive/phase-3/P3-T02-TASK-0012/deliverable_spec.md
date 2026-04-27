# Deliverable Spec: P3-T02-TASK-0012

## Required Output

### New Files
- `src/assay/runner/runner.py` — RunResult dataclass + run() function
- `tests/test_runner.py` — unit tests with mocked subprocess

### Modified Files
- none

## Acceptance Checklist
- [ ] `run()` invokes `docker run` with correct image, env vars, volume mount
- [ ] `RunResult` carries exit_code, output_dir, stdout, stderr
- [ ] Successful mock run returns exit_code 0
- [ ] Failed mock run returns exit_code 1
- [ ] Output dir defaults to tempfile.mkdtemp() when not supplied
- [ ] All new tests passing
- [ ] Full test suite passing with no regressions
- [ ] `make lint` and `make typecheck` clean
- [ ] review bundle complete in `results.md` and `handoff.md`

## Not Required
- Live Docker execution (deferred to P3-T05)
- Artifact parsing (deferred to P3-T03)
- CLI wiring (deferred to P3-T04)
