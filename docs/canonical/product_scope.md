# Product Scope


---

## 1. Purpose

Assay is an independent verification layer for software projects. It runs automated tests on a schedule, verifies frontend bug reports via a browser SDK, and outputs structured task packets compatible with Grain.

Assay is built for any software team or individual developer who needs systematic, reproducible validation of their product — without tying their verification layer to a specific CI provider, framework, or issue tracker.

---

## 2. Goals

- Provide scheduled and on-demand test execution via CLI
- Capture and reproduce frontend bugs via a lightweight browser SDK (screenshot + metadata + user comment)
- Output structured, actionable task packets in Grain-compatible format
- Operate independently — no hard dependency on Grain or any specific CI system
- Support monetization through API key-based authentication on all ingest endpoints

---

## 3. Non-Goals (v1)

- Web UI or dashboard
- Bug bounty public portal or verification workflow
- Multi-user account management
- OAuth / SSO authentication
- SaaS deployment or hosted infrastructure
- Integration with specific CI/CD providers

---

## 4. Target Users

Any software team or individual developer who needs:
- Automated, scheduled validation of a software product
- Reproducible frontend bug capture with screenshot and metadata
- Structured output compatible with task/project management tools (Grain or otherwise)

No assumption is made about team size, stack, or deployment environment.

---

## 5. Key Capabilities (v1)

- `assay` CLI with `run`, `schedule`, `report`, `key`, and `serve` commands
- Scheduler: daily, weekly, on-demand test execution with cron expressions
- Playwright + Docker runner for isolated, reproducible frontend/browser testing
- FastAPI ingest layer to receive browser SDK payloads, auth-gated by API key
- TypeScript browser SDK: captures screenshot + metadata + user comment → POST to ingest
- API key issuance and validation (`assay key create/list/revoke`)
- Grain-compatible task packet output written to local filesystem

---

## 6. Scope Boundaries

### In scope for v1

- CLI service + scheduler
- Playwright runner in Docker (Docker required, not optional)
- FastAPI ingest layer with API key auth
- TypeScript browser SDK (npm package)
- Task packet output (Grain-compatible JSON)
- API key lifecycle management (create, list, revoke)

### Explicitly deferred to v2

- Web UI / dashboard
- Bug bounty portal (internal + external verification workflow)
- Multi-user accounts
- OAuth / SSO / advanced auth
- Advanced analytics or reporting
- SaaS hosting or managed infrastructure

---

## 7. Relationship to Grain

Assay outputs Grain-compatible task packets. There is no hard dependency on Grain being installed or available. Assay functions as a fully standalone verification layer; Grain compatibility is an output format choice, not an architectural dependency.

---

## 8. Monetization Model (v1 Foundation)

API key authentication is required on all ingest endpoints. In v1, keys are managed locally. This establishes the auth surface needed for future usage-based or subscription billing in v2. The specific monetization model is an open question (see `docs/working/open_questions.md`).
