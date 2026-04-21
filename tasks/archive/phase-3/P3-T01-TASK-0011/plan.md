# Plan: P3-T01-TASK-0011

## Approach

Use the official `mcr.microsoft.com/playwright` base image — it ships with Node.js and all browser binaries pre-installed, eliminating the fragile `npx playwright install` step. Add a minimal `run.js` entry script that reads env vars, navigates to the target URL, takes a screenshot, and writes `result.json`. The output dir is `/output` — the Python runner module mounts a host dir there.

---

## Step 1 — Create runner/ directory structure

Create `runner/Dockerfile`, `runner/run.js`, `runner/package.json`, `runner/.dockerignore`.

---

## Step 2 — Write Dockerfile

Base: `mcr.microsoft.com/playwright:v1.44.0-jammy`. Copy `package.json` and `run.js`. Set `WORKDIR /app`. Default `CMD ["node", "run.js"]`. Expose `ASSAY_TARGET_URL`, `ASSAY_SUITE`, `ASSAY_OUTPUT_DIR` as documented env vars (no defaults — runner module must supply them).

---

## Step 3 — Write run.js

Use `@playwright/test`-free approach: import `playwright` directly. Launch Chromium, navigate to `ASSAY_TARGET_URL`, screenshot to `$ASSAY_OUTPUT_DIR/screenshot.png`, write `$ASSAY_OUTPUT_DIR/result.json` with `{ outcome, url, timestamp, error }`. Exit 0 on pass, 1 on failure.

---

## Step 4 — Write package.json

Minimal: `{ "dependencies": { "playwright": "^1.44.0" } }`. No test runner needed — run.js is the entry point.

---

## Verification

`docker build -t assay-playwright:latest ./runner` succeeds. `docker run --rm -e ASSAY_TARGET_URL=https://example.com -e ASSAY_OUTPUT_DIR=/output -v /tmp/assay-test:/output assay-playwright:latest` produces `screenshot.png` and `result.json` in `/tmp/assay-test`. Manual verification only — no automated test at this stage (P3-T05 handles integration tests).
