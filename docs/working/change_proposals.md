# Change Proposals

---

## CP-001 — Replace Grain task packet schema in `data_contracts.md` §1

**Status:** applied (2026-04-15)
**Proposed by:** P1-T03-TASK-0003
**Affects:** `docs/canonical/data_contracts.md` §1
**Requires:** human approval per `PROJECT_RULES.md` §3

---

### Finding

Q1 is resolved. Grain has an existing, documented output contract that Assay must conform to.

Grain's `docs/working/v2_plan.md §11.2` defines the **Sentinel result payload schema** — the exact JSON structure Assay must produce and deliver to Grain via `grain verify ingest --payload <path>`. Assay was formerly called Sentinel; this contract was written for Assay.

The current schema in `data_contracts.md §1` is a freeform bug/test ticket format that does not match Grain's contract. It must be replaced.

---

### Current schema (data_contracts.md §1) — INCORRECT

```json
{
  "id": "<uuid-v4>",
  "schema_version": "1.0.0",
  "created_at": "<ISO 8601>",
  "source": "assay",
  "source_version": "<semver>",
  "project": "<project-name>",
  "type": "test_failure | bug_report | verification",
  "status": "ready",
  "title": "<short description>",
  "description": "<full description>",
  "severity": "low | medium | high | critical",
  "artifacts": [...],
  "metadata": {...},
  "user_comment": "<optional>"
}
```

---

### Proposed schema — Grain Sentinel result payload contract

**Required fields:**

```json
{
  "verification_id": "<string — stable ID assigned by Assay at submission>",
  "task_id": "<string — the Grain task packet ID being verified, e.g. TASK-0070>",
  "issue_type": "<enum: test_failure | bug_finding | screenshot_evidence | trace_capture | human_annotation>",
  "severity": "<enum: info | warning | error | critical>",
  "outcome": "<enum: pass | fail | inconclusive>",
  "summary": "<string — human-readable description of the finding>"
}
```

**Optional fields:**

```json
{
  "artifact_refs": ["<path or URI to captured artifact>"],
  "followup_candidates": [
    { "title": "<string>", "description": "<string>" }
  ],
  "verified_at": "<ISO 8601 datetime>"
}
```

---

### Delivery model

Assay writes the payload as a JSON file to a Grain-visible location (or a configured output directory). The Grain operator runs:

```
grain verify ingest --verification-id <id> --payload <path>
```

Assay does not push directly to Grain. Grain pulls via operator action.

---

### Implications for architecture

- The `task_id` field means Assay verifications are tied to specific Grain task packets — Assay is not a standalone bug tracker but a verification service for Grain workflows.
- `followup_candidates` are proposals for the operator, not auto-created packets. Assay should populate this when tests or captures identify likely follow-up work.
- The browser SDK captures (`screenshot_evidence`, `human_annotation`) and runner results (`test_failure`, `bug_finding`) map cleanly to `issue_type` values.
- Severity mapping: Playwright test failures → `error` or `critical`; SDK captures default to `info` unless user marks otherwise.

---

### Proposed update to data_contracts.md §1

Replace the current §1 content with the Grain-conformant schema above. Add a note that this schema is defined by Grain's bridge contract (`v2_plan.md §11`) and Assay must not deviate from required fields.

---

### Architectural open question surfaced by this finding

The `task_id` field assumes every Assay output references a specific Grain task packet. This works for the bug bounty / verification use case, but raises a question for standalone CLI use (e.g., `assay run` against a project that has no Grain workflow). Options:

- A) `task_id` is required — Assay only operates within Grain workflows
- B) `task_id` is optional — standalone mode produces payloads without it; Grain ingestion requires it
- C) Assay has two output modes: Grain payload (with `task_id`) and standalone summary (without)

**Recommendation:** Option B — `task_id` optional for standalone runs. Grain's contract requires it for ingestion, but Assay should support standalone use per its stated scope. Log as Q10 in open_questions.md.

---

### Decision needed from

Project owner — approve, reject, or amend before P1-T04 begins.

---

## CP-002 — Rename "Sentinel" references in `data_contracts.md` §1 and schema files

**Status:** applied (2026-04-16)
**Proposed by:** Phase 4 review
**Affects:** `docs/canonical/data_contracts.md` §1, `src/assay/schemas/sentinel_payload.schema.json`
**Requires:** human approval per `PROJECT_RULES.md` §3

---

### Finding

`data_contracts.md §1` is titled "Grain Sentinel Result Payload Schema" and describes a delivery model using `grain verify ingest --payload <path>`. Both are stale:

1. **"Sentinel" was Grain's internal name** for the verification layer feature before it was extracted into this standalone tool, Assay. The schema was written for Assay; the name should reflect that.
2. **`grain verify ingest` does not exist** in the current Grain CLI. The command was planned in `grain/docs/working/v2_plan.md §11.2` but never shipped — because the feature became Assay instead.
3. **`sentinel_payload.schema.json`** carries the same stale name.

---

### Proposed changes

**`docs/canonical/data_contracts.md` §1:**
- Rename heading: `"Grain Sentinel Result Payload Schema"` → `"Assay Result Payload Schema"`
- Remove the `grain verify ingest` command from the delivery model section
- Replace delivery model with: *"Assay writes the payload JSON to the configured output directory. The operator may inspect it directly or integrate it into their workflow via `assay report` or by reading the file."*
- Remove the reference to `grain/docs/working/v2_plan.md §11.2` as the defining authority (Assay itself is now the authority)

**`src/assay/schemas/sentinel_payload.schema.json`:**
- Rename file to `assay_payload.schema.json`
- Update `"$id"` from `"assay:sentinel_payload"` to `"assay:payload"`
- Update `"title"` from `"Sentinel Result Payload"` to `"Assay Result Payload"`

**`src/assay/schemas/__init__.py`:**
- Update `SENTINEL_PAYLOAD = _load("sentinel_payload.schema.json")` → `ASSAY_PAYLOAD = _load("assay_payload.schema.json")`

**All references in tests and source:**
- Update `SENTINEL_PAYLOAD` → `ASSAY_PAYLOAD` in `tests/test_schemas.py` and `tests/test_packet_schema.py`

---

### What does NOT change

- The payload JSON structure (required and optional fields) is unchanged
- The `$schema` draft version is unchanged
- No data format changes — only naming

---

### Decision needed from

Project owner — approve to apply in Phase 5 or as a standalone patch.

---

## CP-003 — Add `assay schedule run` to CLI spec in `data_contracts.md §5`

**Status:** applied (2026-04-21)
**Proposed by:** P7-T04-TASK-0004
**Affects:** `docs/canonical/data_contracts.md` §5 (Configuration File Schema / CLI surface)
**Requires:** human approval per `PROJECT_RULES.md` §3

---

### Finding

P7-T04 implemented `assay schedule run` — a foreground scheduler loop that fires registered schedules via APScheduler. This command was not present in the original CLI specification in `data_contracts.md`.

### Proposed addition to `data_contracts.md §5` CLI commands table

```
assay schedule run    Start the foreground scheduler loop (runs until Ctrl+C)
```

### What does NOT change

- Existing CLI commands and their signatures are unchanged
- Schedule store schema (§4) is unchanged
- No behavioral changes to add/list/remove

---

### Decision needed from

Project owner — approve to update `data_contracts.md §5` with the new command.
