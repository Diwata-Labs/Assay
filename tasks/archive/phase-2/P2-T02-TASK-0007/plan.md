# Plan: P2-T02-TASK-0007

## Approach

Use `tomllib` (Python 3.11+ stdlib) to parse the config file. Define an `AssayConfig` dataclass with nested dataclasses per section, all fields optional with defaults matching cli_spec.md §5. Implement `load_config(path)` that resolves the file path (override → local → global → defaults), parses TOML, and returns a validated `AssayConfig`. Wire `--config` in `cli/main.py` to load config and store it in the Typer context object.

---

## Step 1 — Implement config.py

Define `ProjectConfig`, `RunnerConfig`, `OutputConfig`, `ServeConfig`, `KeysConfig` dataclasses with defaults. Define `AssayConfig` as the root container. Implement `load_config(path: str | None = None) -> AssayConfig` that:
1. Resolves path: explicit arg → `./assay.toml` → `~/.assay/config.toml` → empty (all defaults)
2. If file found, parses with `tomllib.load()`
3. Maps parsed dict onto dataclasses; raises `ConfigError` on unrecognised top-level keys
4. Returns `AssayConfig`

---

## Step 2 — Wire CLI

In `cli/main.py`, import `load_config` and `ConfigError`. In the `main` callback, if `config` arg is set, call `load_config(config)` and catch `ConfigError` → print message + `raise typer.Exit(2)`. Store result in `ctx.obj` for subcommands to access later.

---

## Step 3 — Write tests

`tests/test_config.py`:
- Valid full config loads correctly
- Missing file returns all defaults
- Invalid TOML raises `ConfigError`
- Unknown top-level key raises `ConfigError`
- `--config` flag in CLI with valid file exits 0 (via `--version` callback after config load)
- `--config` flag with nonexistent file exits 2

---

## Verification

`make test` 29+ passing. `make lint` and `make typecheck` clean. `assay --config ./assay.toml --version` works with a valid file.
