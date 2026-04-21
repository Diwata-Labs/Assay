# Task: Write Dockerfile for Playwright runner image

## Metadata
- **ID:** P3-T01-TASK-0011
- **Status:** done
- **Phase:** Phase 3 — Playwright + Docker Runner
- **Backlog:** P3-T01
- **Packet Path:** tasks/P3-T01-TASK-0011/
- **Dependencies:** P1-T01-TASK-0001
- **Primary Adapter:** code_adapter
- **Secondary Adapters:** none

## Objective
Write a Dockerfile that produces an image containing Playwright, all required browsers (Chromium at minimum), and Node.js. The image receives a target URL and suite name as environment variables and runs a Playwright test script, writing screenshots and a JSON result file to a mounted output directory.

## Why This Task Exists
Every `assay run` execution spawns a fresh container from this image. The image must be self-contained — no host dependencies beyond Docker itself.

## Scope
- `runner/Dockerfile` — multi-stage or single-stage; Node.js + Playwright + browsers
- `runner/run.js` — minimal Playwright entry script: open target URL, take screenshot, write result JSON
- `runner/.dockerignore` — exclude node_modules and local artifacts
- Image accepts `ASSAY_TARGET_URL`, `ASSAY_SUITE`, `ASSAY_OUTPUT_DIR` env vars
- Output: `screenshot.png` + `result.json` written to `/output` inside the container

## Constraints
- Chromium only in v1 — full browser matrix deferred (architecture §2.3)
- Containers are ephemeral — no persistent state
- Output dir must be mountable as a Docker volume
- No Python in the runner image — it is Node.js only

## Escalation Conditions
- Playwright browser install fails in build context
