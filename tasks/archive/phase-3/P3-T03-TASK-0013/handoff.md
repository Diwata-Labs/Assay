---
task_id: P3-T03-TASK-0013
---

# Handoff: P3-T03-TASK-0013

## What was built

`src/assay/runner/artifacts.py` — artifact collection module with:
- `ArtifactError`: raised when result.json is present but unparseable
- `ArtifactBundle`: dataclass holding outcome, url, suite, timestamp, error, screenshot_path, raw_result
- `collect_artifacts(output_dir, runner_result)`: reads runner output directory; falls back to exit-code-derived outcome when result.json is absent

`tests/test_artifacts.py` — 7 unit tests using tmp_path fixtures covering all acceptance criteria.

## Interface for next task

P3-T04 (`assay run` wiring) should call:

```python
from assay.runner.runner import run
from assay.runner.artifacts import collect_artifacts, ArtifactError

runner_result = run(target_url, suite=suite, image=config.runner.docker_image)
bundle = collect_artifacts(runner_result.output_dir, runner_result)
```

`bundle.outcome` → "pass" / "fail" / "inconclusive"  
Exit code mapping: pass → 0, fail → 3, inconclusive → 1  
`ArtifactError` should be caught and reported as exit code 1.
