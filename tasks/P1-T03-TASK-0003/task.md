# Task: Confirm or draft Grain task packet schema

## Metadata
- **ID:** P1-T03-TASK-0003
- **Status:** done
- **Phase:** Phase 1 — Foundation
- **Backlog:** P1-T03
- **Packet Path:** tasks/P1-T03-TASK-0003/
- **Dependencies:** none
- **Primary Adapter:** docs_adapter
- **Secondary Adapters:** none

## Objective

Resolve open question Q1: does Grain have an existing, published task packet schema that Assay must conform to? If yes, obtain the schema and update `docs/canonical/data_contracts.md` to match. If no, confirm that the schema in `data_contracts.md` is Assay's authoritative definition and remove the draft caveat. Output is a confirmed, canonical data contract for the Grain task packet.

## Why This Task Exists

`docs/canonical/data_contracts.md` currently has a draft caveat on the Grain packet schema pending resolution of Q1. All downstream tasks (P1-T04, Phase 4 formatter, Phase 5 ingest) depend on a stable schema. This must be resolved before P1-T04 can begin.

See: `docs/working/open_questions.md` Q1, `docs/canonical/data_contracts.md` §1.

## Scope

- Check whether Grain exposes a machine-readable or documented task packet schema
- If Grain schema exists: compare to current `data_contracts.md` §1 and produce a change proposal or direct update
- If no Grain schema: confirm Assay's schema as authoritative, remove draft caveat from `data_contracts.md` §1
- Update `docs/working/open_questions.md` Q1 status to `decided`

## Constraints

- Changes to `docs/canonical/data_contracts.md` require human approval per `PROJECT_RULES.md` §3
- If Grain schema differs from Assay's current draft, produce a change proposal in `docs/working/change_proposals.md` — do not directly overwrite
- Minimal change: only touch `data_contracts.md` §1 (Grain packet schema) and Q1 in open questions

## Escalation Conditions

- If Grain's schema is incompatible with Assay's proposed schema in a way that requires architectural changes — escalate before editing any canonical doc
