# Plan: P2-T05-TASK-0010

## Approach

Add a --verbose test to test_cli.py after P2-T04 adds the flag. Audit existing tests against cli_spec.md §3/§4/§6 to confirm no other gaps. No new files needed.

---

## Step 1 — Add --verbose test

Add `test_verbose_flag()` to `tests/test_cli.py`: invoke `app` with `["--verbose", "--version"]` and assert exit 0.

---

## Step 2 — Coverage audit

Verify tests exist for: --version (✓), --help (✓), --config valid (✓), --config missing→exit 2 (✓), all 10 stubs→exit 1 (✓), --verbose (new). Exit codes 3/4 deferred.

---

## Verification

`make test` 37+ passing. All four global flags tested.
