# CLI Specification


---

## 1. Entrypoint

Command: `assay`

Installed as a CLI tool via pip (`pip install assay`) or local install script.

---

## 2. Commands

### 2.1 `assay run`

Execute a test run immediately using the Playwright + Docker runner.

```
assay run [--target <url>] [--suite <suite-name>] [--output <dir>]
```

| Flag | Required | Default | Description |
|------|----------|---------|-------------|
| `--target` | no | config default | URL or target identifier to test |
| `--suite` | no | `default` | Named test suite to run |
| `--output` | no | `./assay-output` | Directory to write task packets |

**Behavior:**
- Starts Docker container with Playwright runner image
- Executes the specified suite against the target
- Collects artifacts (screenshots, logs, pass/fail)
- Writes Grain-compatible task packets to output directory
- Exits 0 on success, 3 if tests fail, 1 on runner error

---

### 2.2 `assay schedule`

Manage scheduled test runs.

```
assay schedule add --cron "<expr>" [--suite <suite-name>]
assay schedule list
assay schedule remove <id>
```

**Subcommands:**

| Subcommand | Description |
|------------|-------------|
| `add` | Register a schedule with a cron expression |
| `list` | Display all active schedules with IDs and next run time |
| `remove <id>` | Remove a schedule by ID |

**Behavior:**
- Schedule state persisted to local filesystem (see `data_contracts.md`)
- Cron expressions follow standard 5-field format (minute hour day month weekday)
- `add` prints the assigned schedule ID on success

---

### 2.3 `assay report`

Display or export task packet summaries from the output directory.

```
assay report [--output <dir>] [--format json|text]
```

| Flag | Required | Default | Description |
|------|----------|---------|-------------|
| `--output` | no | `./assay-output` | Directory to read packets from |
| `--format` | no | `text` | Output format: `text` (human) or `json` (machine) |

---

### 2.4 `assay key`

Manage API keys for the ingest endpoint.

```
assay key create [--name <label>]
assay key list
assay key revoke <key-id>
```

**Subcommands:**

| Subcommand | Description |
|------------|-------------|
| `create` | Generate a new API key; prints raw key once — not stored |
| `list` | Show key IDs and labels (never raw key values) |
| `revoke <id>` | Invalidate a key by ID |

**Behavior:**
- Raw key is printed exactly once at creation time; not retrievable afterward
- Keys are stored as bcrypt hashes in `~/.assay/keys.json`
- Revoked keys are marked `revoked: true` and rejected on auth

---

### 2.5 `assay serve`

Start the FastAPI ingest server.

```
assay serve [--port <port>] [--host <host>]
```

| Flag | Required | Default | Description |
|------|----------|---------|-------------|
| `--port` | no | `8000` | Port to bind |
| `--host` | no | `127.0.0.1` | Host to bind |

**Behavior:**
- Starts FastAPI server
- All `/ingest` requests require valid `X-Assay-Key` header
- Runs until interrupted (Ctrl-C)

---

## 3. Exit Codes

| Code | Meaning |
|------|---------|
| 0 | Success |
| 1 | General / unexpected error |
| 2 | Configuration error (missing or invalid `assay.toml`) |
| 3 | Test failure (runner completed, but tests failed) |
| 4 | Auth error (invalid or missing API key in relevant context) |

---

## 4. Stub Policy (§5.1)

Unimplemented commands must not silently succeed.

Before a command is fully implemented, it must either:
- be absent from the command surface entirely, **or**
- return an explicit not-implemented error with a non-zero exit code

**Silent success (exit 0, no output) from a stub is not permitted.**

---

## 5. Configuration File

Config file locations (in priority order):
1. `./assay.toml` (project-local)
2. `~/.assay/config.toml` (global user config)

Minimal structure:

```toml
[project]
name = "my-project"

[runner]
docker_image = "assay-playwright:latest"
timeout_seconds = 300

[output]
directory = "./assay-output"

[serve]
host = "127.0.0.1"
port = 8000

[keys]
store = "~/.assay/keys.json"
```

CLI flags override config file values.

---

## 6. Global Flags

Available on all commands:

| Flag | Description |
|------|-------------|
| `--config <path>` | Override config file path |
| `--verbose` | Enable verbose output |
| `--help` | Show help |
| `--version` | Print version |
