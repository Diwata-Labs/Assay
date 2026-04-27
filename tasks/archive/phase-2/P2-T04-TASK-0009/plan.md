# Plan: P2-T04-TASK-0009

## Approach

Add `--verbose` as a boolean flag to the root app callback in `cli/main.py`. Store it alongside the config on `ctx.obj` so subcommands can read it. No verbose output in stubs — just accept and store.

---

## Step 1 — Add --verbose to main callback

Add `verbose: bool = typer.Option(False, "--verbose", help="Enable verbose output.")` to the `main` callback. Store as `ctx.ensure_object(dict)` pattern or expand ctx.obj to carry both config and verbose.

---

## Step 2 — Verify all four flags present

Confirm: `--help` (auto), `--version` (done), `--config` (done), `--verbose` (new). Run `assay --help` and verify all appear.

---

## Verification

`assay --verbose --version` exits 0. `assay --help` shows `--verbose` in output. Tests pass.
