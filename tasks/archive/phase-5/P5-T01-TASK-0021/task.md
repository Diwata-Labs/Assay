# Task: Implement assay key commands

## Metadata
- **ID:** P5-T01-TASK-0021
- **Status:** review
- **Phase:** Phase 5 — FastAPI Ingest Layer + Auth
- **Backlog:** P5-T01
- **Packet Path:** tasks/P5-T01-TASK-0021/
- **Dependencies:** P2-T01-TASK-0006
- **Primary Adapter:** code_adapter
- **Secondary Adapters:** none

## Objective
Implement `src/assay/keys/store.py` (key store read/write with bcrypt) and wire the `assay key create`, `assay key list`, and `assay key revoke` CLI commands to real implementations replacing the stubs.

## Why This Task Exists
API key auth gates all ingest requests. This task builds the key lifecycle management layer that P5-T03 (middleware) depends on for validation.

## Scope
- `src/assay/keys/__init__.py` — package init
- `src/assay/keys/store.py` — `create_key()`, `list_keys()`, `revoke_key()`, `verify_key()`
- Update `src/assay/cli/main.py` `key_create`, `key_list`, `key_revoke` commands
- `tests/test_keys.py` — unit tests (tmp_path for key store file)

## Constraints
- Key store path: `config.keys.store` (default `~/.assay/keys.json`), expanded with `Path.expanduser()`
- Raw key: `secrets.token_urlsafe(32)` — printed once at create time, never stored
- Hash: `bcrypt.hashpw(key.encode(), bcrypt.gensalt())`
- Verify: `bcrypt.checkpw(raw.encode(), stored_hash.encode())`
- Revoked entries preserved (not deleted) with `revoked: true` and `revoked_at` timestamp
- Key store created if absent; parent dirs created with `mkdir(parents=True, exist_ok=True)`
- Schema: `docs/canonical/data_contracts.md §3`

## Escalation Conditions
- None
