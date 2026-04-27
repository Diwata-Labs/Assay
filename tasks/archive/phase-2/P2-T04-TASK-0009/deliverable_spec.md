# Deliverable Spec: P2-T04-TASK-0009

## Required Output

### New Files
- none

### Modified Files
- `src/assay/cli/main.py` — add `--verbose` flag to main callback

## Acceptance Checklist
- [ ] `assay --verbose --version` exits 0
- [ ] `assay --help` shows `--verbose` option
- [ ] All existing tests still passing
- [ ] `make lint` and `make typecheck` clean
- [ ] review bundle complete in `results.md` and `handoff.md`

## Not Required
- Verbose output in stub commands
- Per-command verbose flags
