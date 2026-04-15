# Open Questions

**Project:** Assay
**Last updated:** 2026-04-13

Status values: `open` | `decided` | `deferred`

---

## Q1 — Grain task packet schema: conform or define?

**Status:** decided
**Decided by:** P1-T03-TASK-0003 (2026-04-15)

**Decision:** Option A — Grain has a strict schema. Assay must conform exactly.

**Finding:** Grain's `v2_plan.md §11.2` defines the **Sentinel result payload schema** — the exact JSON contract Assay produces and Grain ingests via `grain verify ingest`. The schema is: required fields `verification_id`, `task_id`, `issue_type`, `severity`, `outcome`, `summary`; optional fields `artifact_refs`, `followup_candidates`, `verified_at`.

**Action required:** Approve CP-001 in `docs/working/change_proposals.md` to update `data_contracts.md §1` to match this schema.

---

## Q2 — CLI framework: Click vs Typer

**Status:** decided
**Decision:** Typer

---

## Q3 — Browser SDK screenshot mechanism

**Status:** decided
**Decision:** html2canvas for v1. Revisit in v2.

---

## Q4 — Scheduler backend: APScheduler vs alternatives

**Status:** decided
**Decision:** APScheduler with JSON job store for v1.

---

## Q5 — Monetization model

**Status:** deferred
**Deferred to:** v2 planning. V1 API key infrastructure is sufficient as-is.

---

## Q6 — API key storage encryption (v1)

**Status:** decided
**Decision:** bcrypt hash only for v1; plaintext JSON file. Document the shared-machine risk. Keychain support deferred to v2.

---

## Q7 — SDK distribution: npm only or also CDN?

**Status:** decided
**Decision:** npm only for v1. Add CDN build in v2 if demand warrants it.

---

## Q8 — Missed scheduled runs: retry behavior

**Status:** decided
**Decision:** No retry in v1. Log missed runs only. Configurable retry deferred to v2.

---

## Q9 — Ingest server deployment in production

**Status:** decided
**Decision:** Manual `assay serve` on a VPS for v1. No daemon mode required. Managed hosting deferred to v2.

---

## Q10 — Standalone mode: is `task_id` required in output payloads?

**Status:** decided
**Decision:** `task_id` is optional. Standalone runs set it to `null`; Grain ingestion requires a non-null value at ingest time (enforced by Grain, not Assay).
