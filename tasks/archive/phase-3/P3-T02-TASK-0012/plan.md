# Plan: P3-T02-TASK-0012

## Approach

Implement `runner.py` using `subprocess.run` to invoke `docker run` with the correct flags. Mount a temp output directory as `/output` inside the container. Pass `ASSAY_TARGET_URL`, `ASSAY_SUITE`, `ASSAY_OUTPUT_DIR` as `-e` env vars. Capture stdout/stderr and stream to the caller. Return a `RunResult` dataclass. Unit tests patch `subprocess.run` to avoid needing Docker.

---

## Step 1 — Implement RunResult and run()

`RunResult(exit_code: int, output_dir: str, stdout: str, stderr: str)`. `run(target_url, suite, output_dir, image)` builds and executes the docker command, captures output, returns RunResult.

---

## Step 2 — Write unit tests

`tests/test_runner.py` — patch `subprocess.run`:
- Successful run returns exit_code 0
- Failed run returns exit_code 1
- Correct docker flags passed (image, env vars, volume mount)
- Output dir passed through correctly

---

## Verification

`make test` 40+ passing. `make lint` and `make typecheck` clean.
