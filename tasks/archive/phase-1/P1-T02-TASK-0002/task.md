# Task: Initialize TypeScript SDK scaffold

## Metadata
- **ID:** P1-T02-TASK-0002
- **Status:** done
- **Phase:** Phase 1 — Foundation
- **Backlog:** P1-T02
- **Packet Path:** tasks/P1-T02-TASK-0002/
- **Dependencies:** none
- **Primary Adapter:** frontend_adapter
- **Secondary Adapters:** none

## Objective

Create the TypeScript browser SDK scaffold: `sdk/` directory with `package.json`, `tsconfig.json`, source entry point, and a passing smoke test. No implementation logic — scaffold and tooling only.

## Why This Task Exists

Phase 1 requires both the Python and TypeScript scaffolds before any implementation begins. The SDK scaffold unblocks Phase 6 (TypeScript browser SDK implementation) and is required by P1-T05 (dev tooling setup). Can run in parallel with P1-T03.

See: `docs/working/implementation_plan.md` Phase 1, `docs/working/backlog.md` P1-T02.

## Scope

- `sdk/package.json` — name, version, scripts, dev deps (typescript, vitest)
- `sdk/tsconfig.json` — strict TypeScript config targeting ESNext/ESM
- `sdk/src/index.ts` — empty module placeholder (exports nothing yet)
- `sdk/src/sdk.ts` — empty placeholder for `AssaySDK` class
- `sdk/tests/sdk.test.ts` — one passing smoke test
- `.npmignore` or `files` field in package.json to exclude test files from publish

## Constraints

- Framework-agnostic: no React, Vue, or other framework dependency
- ESM primary output; CJS output deferred to Phase 6
- TypeScript strict mode required
- Minimal footprint: no runtime dependencies in v1 scaffold

## Escalation Conditions

- If TypeScript version or vitest configuration causes irresolvable conflicts
