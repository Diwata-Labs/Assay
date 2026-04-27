# Deliverable Spec: P2-T02-TASK-0007

## Required Output

### New Files
- `src/assay/config.py` — AssayConfig dataclass + load_config() + ConfigError
- `tests/test_config.py` — config parsing tests

### Modified Files
- `src/assay/cli/main.py` — wire --config flag to load_config(); exit 2 on ConfigError

## Acceptance Checklist
- [ ] `load_config(None)` returns defaults when no file exists
- [ ] Valid TOML file parsed into `AssayConfig` correctly
- [ ] Unknown top-level key raises `ConfigError`
- [ ] Invalid TOML raises `ConfigError`
- [ ] `--config <missing-file>` exits 2 via CLI
- [ ] All new tests passing
- [ ] Full test suite passing with no regressions
- [ ] `make lint` and `make typecheck` clean
- [ ] review bundle complete in `results.md` and `handoff.md`

## Not Required
- Passing config values down into stub commands — stubs remain stubs
- Config file writing or creation
- Schema validation beyond section/key structure check
