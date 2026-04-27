---
task_id: P4-T01-TASK-0016
---

# Handoff: P4-T01-TASK-0016

## Interface for downstream tasks

```python
from assay.formatter.formatter import format_packet
from assay.runner.artifacts import ArtifactBundle

packet: dict[str, object] = format_packet(bundle, task_id="TASK-0042")
# or
packet = format_packet(bundle)  # task_id=None for standalone
```

## For P4-T02 (packet file writer)
Serialize `packet` as JSON to `assay-<ISO-timestamp>-<uuid>.json` in the configured output directory.

## For P4-T04 (runner integration)
Call `format_packet(bundle)` after `collect_artifacts()` in `assay run`.
