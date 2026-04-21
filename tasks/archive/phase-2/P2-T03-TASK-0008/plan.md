# Plan: P2-T03-TASK-0008

## Approach

P2-T01 already implemented all stubs with exit 1 and "not implemented" output. This task verifies the contract is met by running the existing test suite and confirming coverage matches §3/§4 requirements. No new code needed.

---

## Step 1 — Verify coverage

Confirm `tests/test_cli.py` covers all 10 stub commands and asserts exit_code == 1 and "not implemented" in output.

---

## Step 2 — Verify exit code mapping

Confirm exit code 2 (config error) is tested in `tests/test_config.py`. Exit codes 3 and 4 are not testable until Phase 3/5 implementations — document as deferred.

---

## Verification

`make test` passes. All 10 stub tests present in test_cli.py. Exit code 2 covered in test_config.py.
