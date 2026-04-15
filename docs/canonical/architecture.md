# Architecture


---

## 1. System Overview

Assay has three primary subsystems:

1. **CLI + Scheduler** — operator-facing control surface
2. **Runner** — isolated test execution environment
3. **Ingest API + Browser SDK** — passive collection surface for frontend bug reports

These subsystems share a common output module: the **Task Packet Formatter**, which converts all results into Grain-compatible task packets written to the local filesystem.

---

## 2. Components

### 2.1 CLI (`assay`)

- **Language:** Python
- **Entrypoint:** `assay` command (installed via pip or install script)
- **Responsibilities:**
  - Accept and dispatch `run`, `schedule`, `report`, `key`, `serve` commands
  - Invoke the runner for test execution
  - Manage API key lifecycle (`assay key`)
  - Start the ingest server (`assay serve`)
  - Write or display task packet summaries (`assay report`)
- **Config:** reads `assay.toml` from project root or `~/.assay/config.toml`

### 2.2 Scheduler

- **Embedded in the CLI process** — no separate daemon in v1
- **Trigger modes:** daily, weekly, on-demand (cron expression)
- **State:** persisted to local filesystem (schedule state schema defined in `data_contracts.md`)
- **Invokes:** runner via same path as `assay run`

### 2.3 Playwright + Docker Runner

- **Language:** Python (orchestration), Playwright (browser automation)
- **Docker required:** yes — every test run executes inside a fresh Docker container for isolation and reproducibility
- **Responsibilities:**
  - Pull / build the Playwright runner Docker image
  - Start container with configured target URL and test suite
  - Execute Playwright test suite inside container
  - Collect artifacts: screenshots, logs, pass/fail result
  - Return artifacts to CLI for packet formatting
- **No persistent container state** — containers are ephemeral per run

### 2.4 FastAPI Ingest Layer

- **Language:** Python
- **Framework:** FastAPI
- **Started via:** `assay serve`
- **Responsibilities:**
  - Expose `/ingest` endpoint (POST)
  - Validate `X-Assay-Key` header against local key store
  - Parse and normalize SDK payload
  - Invoke Task Packet Formatter
  - Write Grain task packet to output store
- **Auth:** API key, passed via `X-Assay-Key` HTTP header
- **Rejection:** HTTP 401 for invalid or missing key; payload not processed
- **Output store (v1):** local filesystem directory

### 2.5 TypeScript Browser SDK

- **Language:** TypeScript
- **Distribution:** npm package
- **Responsibilities:**
  - Initialize with API key + ingest endpoint URL
  - Capture screenshot (browser canvas or DOM-to-image)
  - Collect page metadata: URL, viewport dimensions, user agent, timestamp
  - Collect optional user comment
  - POST payload to Assay ingest endpoint with `X-Assay-Key` header
- **Design constraints:**
  - No framework dependency (framework-agnostic)
  - Minimal bundle footprint
  - API key is embedded at SDK init time (not stored in SDK source)

### 2.6 Task Packet Formatter

- **Language:** Python
- **Shared module** used by both runner and ingest paths
- **Responsibilities:**
  - Convert runner artifacts or SDK payloads into Grain-compatible task packets
  - Write JSON files to configured output directory
  - Assign stable IDs, timestamps, and schema-valid structure
- **Output:** `assay-<timestamp>-<uuid>.json` per packet
- **Schema:** defined in `docs/canonical/data_contracts.md`

---

## 3. Data Flow

```
[ assay run ]
     │
     ▼
[ Docker Container ]
     │
[ Playwright ] → screenshots, logs, pass/fail
     │
     ▼
[ Task Packet Formatter ] → Grain task packet JSON
     │
     ▼
[ Output Directory ]


[ Browser SDK ]
     │  POST /ingest  (X-Assay-Key)
     ▼
[ FastAPI Ingest Layer ]
     │  validate key
     ▼
[ Task Packet Formatter ] → Grain task packet JSON
     │
     ▼
[ Output Directory ]
```

---

## 4. Auth Model (v1)

- **Type:** API key
- **Key format:** opaque random string (min 32 chars)
- **Storage:** bcrypt-hashed entries in `~/.assay/keys.json` — raw key never stored
- **Transport:** HTTP header `X-Assay-Key` on all ingest requests
- **SDK usage:** key passed at SDK initialization, sent with every POST
- **CLI management:** `assay key create | list | revoke`
- **Invalid/missing key:** HTTP 401, payload rejected before processing

---

## 5. Deployment (v1)

- CLI and server run locally or on any single machine with Docker available
- FastAPI server is started manually via `assay serve` — no process manager required in v1
- No SaaS infrastructure, no database, no external dependencies beyond Docker

---

## 6. Modularity Principle

- CLI, Runner, Ingest API, SDK, and Packet Formatter are independently addressable subsystems
- No subsystem may introduce a hard dependency on another subsystem's internal state
- In v2, any subsystem may be extracted, replaced, or scaled independently

---

## 7. Deferred Architectural Items (v2)

- Database-backed output store (currently: local filesystem)
- Multi-tenant key management and user accounts
- Web UI and hosted dashboard
- SaaS deployment model
- Bug bounty verification workflow
