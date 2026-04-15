# Current Focus

## Current Phase
Phase 2 — CLI Skeleton

---

## Active Focus

Phase 1 closed. All foundation deliverables complete — scaffold, schemas, and developer tooling.

Phase 2 begins after Grain patches (GB-001, GB-003) are applied by the project owner.

First task: P2-T01 — Implement CLI entrypoint with Typer (Q2 resolved: Typer).

---

## Immediate Priorities

1. Wait for Grain patches before starting Phase 2 execution
2. P2-T01: Typer entrypoint, `assay` command, `--version` / `--help` / `--config` flags
3. P2-T02: `assay.toml` config parsing with validation
4. P2-T03 through P2-T05: stub commands, exit codes per spec §3/§5.1, CLI tests

---

## Active Constraints

- All CLI commands must enforce exit codes per CLI spec §3 and §5.1 — no silent stubs
- Docker must be available in all environments that run the Playwright runner
- Canonical docs require human approval before direct edits
