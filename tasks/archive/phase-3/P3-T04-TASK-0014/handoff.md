---
task_id: P3-T04-TASK-0014
---

# Handoff: P3-T04-TASK-0014

## What was built

`src/assay/cli/main.py` `run()` command is now fully wired:
1. Validates `--target` required (exit 2 if missing)
2. Reads config from `ctx.obj` for `docker_image` and output directory
3. Calls `_runner.run(target, suite=suite, output_dir=output_dir, image=image)`
4. Calls `_artifacts.collect_artifacts(runner_result.output_dir, runner_result)` — catches `ArtifactError` → exit 1
5. Prints `outcome: <value>`; on error also prints error message to stderr
6. Exits: 0=pass, 3=fail, 1=all other

## For P3-T05 (integration test)

The integration test should invoke `assay run --target <url>` after `docker build`. The test should:
- Verify exit code 0 for a known-good URL
- Verify exit code 3 for a URL that returns a test failure
- Check `result.json` and `screenshot.png` are written to the output directory
