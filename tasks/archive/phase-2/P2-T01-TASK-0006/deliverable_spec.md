# Deliverable Spec: P2-T01-TASK-0006

## Required Output

### New Files
- `src/assay/cli/main.py` — Typer app with all commands
- `tests/test_cli.py` — CLI tests via CliRunner

### Modified Files
- `pyproject.toml` — add `typer>=0.12` dependency; fix entrypoint to `assay.cli.main:app`

## Acceptance Checklist
- [ ] `assay --version` exits 0 and prints version
- [ ] `assay --help` exits 0
- [ ] `assay run` exits 1 with not-implemented message
- [ ] `assay serve` exits 1 with not-implemented message
- [ ] `assay report` exits 1 with not-implemented message
- [ ] `assay schedule add` exits 1 with not-implemented message
- [ ] `assay schedule list` exits 1 with not-implemented message
- [ ] `assay schedule remove` exits 1 with not-implemented message
- [ ] `assay key create` exits 1 with not-implemented message
- [ ] `assay key list` exits 1 with not-implemented message
- [ ] `assay key revoke` exits 1 with not-implemented message
- [ ] All new tests passing
- [ ] Full test suite passing with no regressions
- [ ] `make lint` and `make typecheck` clean
- [ ] review bundle complete in `results.md` and `handoff.md`

## Not Required
- Any real command implementation — stubs only
- Config file parsing — that is P2-T02
- `--config` flag wiring to actual config loading — accept the flag, don't parse yet
