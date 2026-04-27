# Plan: P3-T03-TASK-0013

## Approach

Define `ArtifactBundle` as a dataclass mirroring the result.json fields plus screenshot_path. `collect_artifacts()` reads result.json if present and parses it; falls back to deriving outcome from the RunResult exit code if the file is missing. Locates screenshot.png and sets path to None if absent. Tests use tmp_path to write fixture files.

---

## Step 1 — Implement ArtifactBundle and collect_artifacts

`ArtifactBundle(outcome, url, suite, timestamp, error, screenshot_path, raw_result)`. `collect_artifacts(output_dir, runner_result)` reads `output_dir/result.json` → populates bundle. If missing, sets outcome from exit_code. screenshot_path set if `output_dir/screenshot.png` exists.

---

## Step 2 — Write tests

- Valid result.json + screenshot → full bundle
- Valid result.json, no screenshot → screenshot_path is None
- Missing result.json, exit 0 → outcome "pass"
- Missing result.json, exit 1 → outcome "fail"
- Malformed result.json → raises ArtifactError

---

## Verification

`make test` 48+ passing. `make lint` and `make typecheck` clean.
