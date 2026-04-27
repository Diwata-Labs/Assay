# Results: P3-T04-TASK-0014

## Packet State
- **Current Task Status:** review
- **Review Readiness:** ready
- **Recommended Next Status:** done

## Files Changed
- `src/assay/cli/main.py` — `run()` command: replaced stub with real runner + artifact collection call; added `ctx` parameter to read config
- `tests/test_run_command.py` — new; 6 unit tests mocking runner and artifact collection
- `tests/test_cli.py` — updated `test_run_stub` → `test_run_requires_target` to match new behaviour

## Summary

`assay run` is now wired end-to-end. The command validates `--target`, reads Docker image and output config from `ctx.obj`, calls `runner.run()`, then `collect_artifacts()`, prints `outcome: <value>`, and exits with the correct code (0=pass, 3=fail, 1=inconclusive/error). `ArtifactError` is caught and reports exit 1. All 6 new tests pass with mocked runner; no regressions in the 56-test suite.

## Test Results
- 56/56 pytest passing (6 new in test_run_command.py)
- 1/1 vitest passing
- `make lint`: clean
- `make typecheck`: clean (mypy 0 issues in 10 source files)

## Efficiency

### Execute
- **Prompt Runs:** 1
- **Conversation Restarts:** 1
- **Files Read (estimated):** 3
- **Notes:** One ruff format fix needed (long `with` statements reformatted to parenthesised form)

### Review
- **Prompt Runs:** 0
- **Conversation Restarts:** 0
- **Notes:** None until reviewer fills this in

### Close
- **Prompt Runs:** 0
- **Conversation Restarts:** 0
- **Notes:** None until closer fills this in

## Review Notes
- `assay run` CLI patches against `assay.runner.runner.run` and `assay.runner.artifacts.collect_artifacts` — tests are unit-level; real Docker execution deferred to P3-T05
- `output` CLI param defaults to `config.output.directory` when not supplied — consistent with config-first design

## User Review
- **State:** approved
- **Summary:** assay run wired to runner + artifact collection with full mock test coverage.
- **Resolution Mode:** close_task

### Required Fixes
- None

### Open Questions To Log
- None

### Proposal Candidates To Log
- None

### Follow-Ups To Log
- P3-T05: integration test requiring live Docker

### Residual Risks
- None at this layer

## Verification Review
- **State:** passed

## Closure Decision
- **Decision:** closed
- **Reason:** Closed via grain task close.

## Deliverable Checklist
- [x] `assay run --target <url>` calls `runner.run()` and `collect_artifacts()`
- [x] Outcome "pass" → exit 0
- [x] Outcome "fail" → exit 3
- [x] Outcome other → exit 1
- [x] Missing `--target` → error message, exit 2
- [x] `ArtifactError` → error message, exit 1
- [x] All new tests passing
- [x] Full test suite passing with no regressions
- [x] `make lint` clean
- [x] `make typecheck` clean

## Blockers
None.
