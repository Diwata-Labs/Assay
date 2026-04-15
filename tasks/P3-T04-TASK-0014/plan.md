# Plan: P3-T04-TASK-0014

## Approach

Replace the stub in `assay run` with calls to `runner.run()` and `collect_artifacts()`. The CLI layer stays thin: it reads config from `ctx.obj`, validates `--target`, delegates to the runner, reads the bundle outcome, prints a summary, and maps outcome to the correct exit code. Tests mock both runner and artifact functions.

---

## Step 1 — Update assay run command in main.py

- Add `ctx: typer.Context` parameter to `run()`
- Require `--target` (error exit 2 if None)
- Read `config = ctx.obj` for `docker_image` and output directory
- Call `runner.run(target, suite=suite, output_dir=output, image=config.runner.docker_image)`
- Call `collect_artifacts(result.output_dir, result)` inside try/except ArtifactError
- Print outcome line: `f"outcome: {bundle.outcome}"`
- Exit 0 for "pass", 3 for "fail", 1 otherwise

---

## Step 2 — Write tests

- Mock `assay.runner.runner.run` and `assay.runner.artifacts.collect_artifacts`
- Tests: pass exit 0, fail exit 3, inconclusive exit 1, missing target exit 2, ArtifactError exit 1

---

## Verification

`make test` 55+ passing. `make lint` and `make typecheck` clean.
