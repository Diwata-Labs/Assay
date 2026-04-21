# Plan: P3-T05-TASK-0015

## Approach

Manual verification sequence: build the Docker image, run `assay run` against a live URL, inspect the output directory. No code changes required — this task exercises the stack assembled in P3-T01 through P3-T04.

---

## Step 1 — Build the Docker image

```
docker build -t assay-playwright runner/
```

Confirm: exit 0, no layer errors, `npm install` completes.

---

## Step 2 — Run assay against a test URL

```
assay run --target https://example.com --output /tmp/assay-integration
```

Confirm: exit 0, stdout shows `outcome: pass`.

---

## Step 3 — Inspect output files

```
ls /tmp/assay-integration/
cat /tmp/assay-integration/result.json
```

Confirm: `result.json` and `screenshot.png` present; `result.json` has `outcome: "pass"`.

---

## Verification

All three steps succeed without error. Document exact command output in results.md.

## Blocker Note

Docker is not installed in the current dev environment. This task is blocked until Docker is available. When Docker becomes available, execute steps 1–3 above and close the task.
