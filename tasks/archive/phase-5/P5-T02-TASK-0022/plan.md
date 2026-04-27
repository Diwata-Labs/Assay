# Plan: P5-T02-TASK-0022

## Approach

Create `src/assay/ingest/app.py` with a FastAPI app and a Pydantic `IngestPayload` model mirroring `data_contracts.md §2`. The `POST /ingest` handler accepts a validated payload and returns `{"status": "accepted"}`. Auth and formatter wiring are deferred. Tests use FastAPI's `TestClient` via `httpx`.

---

## Step 1 — Define IngestPayload Pydantic model

Model fields per `data_contracts.md §2`:
- `captured_at: str` — required, non-empty; validate ISO 8601 format
- `url: str` — required, non-empty
- `viewport: Viewport` — nested model with `width: int` and `height: int`, both > 0
- `user_agent: str` — required, non-empty
- `screenshot: str` — required, non-empty; validate as valid base64
- `user_comment: str | None = None`
- `metadata: dict[str, object] = {}`

---

## Step 2 — Implement FastAPI app and POST /ingest

Create `app = FastAPI()`. Define `POST /ingest` route that accepts `IngestPayload` and returns `{"status": "accepted"}`.

Export `app` from `src/assay/ingest/__init__.py`.

---

## Step 3 — Write tests

Use `from fastapi.testclient import TestClient`. Test:
- Valid payload → 200 `{"status": "accepted"}`
- Missing required field → 422
- Empty `url` → 422
- Non-positive viewport dimension → 422
- Invalid base64 `screenshot` → 422
- `user_comment` omitted → 200 (optional field)
- `metadata` omitted → 200 (optional field)

---

## Verification

Run `uv run pytest tests/test_ingest.py -v` and full suite. Confirm all pass.
