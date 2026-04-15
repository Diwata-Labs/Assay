# Task: Implement artifact collection

## Metadata
- **ID:** P3-T03-TASK-0013
- **Status:** done
- **Phase:** Phase 3 — Playwright + Docker Runner
- **Backlog:** P3-T03
- **Packet Path:** tasks/P3-T03-TASK-0013/
- **Dependencies:** P3-T02-TASK-0012
- **Primary Adapter:** code_adapter
- **Secondary Adapters:** none

## Objective
Implement `src/assay/runner/artifacts.py` — reads the output directory produced by the Docker container and returns a structured `ArtifactBundle` containing the parsed result.json, screenshot path, and raw stdout/stderr. This is the boundary layer between the runner and the formatter.

## Why This Task Exists
P3-T04 wires `assay run` end-to-end. It needs a clean interface for reading runner outputs without embedding file I/O logic in the CLI command.

## Scope
- `ArtifactBundle` dataclass: outcome, url, suite, timestamp, error, screenshot_path, raw_result
- `collect_artifacts(output_dir, runner_result)` — reads result.json, locates screenshot.png, returns ArtifactBundle
- Handles missing files gracefully (screenshot absent → None, result.json absent → derive from exit code)
- `tests/test_artifacts.py` — unit tests using tmp_path fixtures

## Constraints
- result.json schema per runner/run.js: `{ outcome, url, suite, timestamp, error }`
- Screenshot is optional — container may fail before writing it
- No Grain packet conversion here — that is Phase 4 (formatter)

## Escalation Conditions
- None
