# Tooling Notes

Lightweight inbox for workflow friction, tool bugs, or observations noticed mid-session.
Agents write here; user reviews and escalates to the appropriate tracker.


| Date       | Command                   | Observation                                                                                                                                                                                           | Severity |
| ---------- | ------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| 2026-04-15 | `grain task prepare`      | Does not detect stub packet files — reports `ok` with `missing_inputs: 0` even when context.md, plan.md, deliverable_spec.md are all unedited template stubs. **Fixed in patch.**                     | high     |
| 2026-04-15 | `grain task create`       | No lightweight packet mode — always generates a full 7-file packet even for small mechanical tasks. `--simple` flag (task.md + results.md only) would reduce overhead.                                | low      |
| 2026-04-15 | `prompts/task.execute.md` | Execute prompt is fragile in a live AI session — AI skips packet generation steps when asked to execute inline. `grain task prepare` now warns; partially addressed in patch.                         | medium   |
| 2026-04-15 | `grain upgrade`           | Does not seed new working docs defined in source manifest that are absent in the project (e.g. tooling_notes.md). Should detect and offer to seed missing working docs rather than silently skipping. | low      |
| 2026-04-15 | `grain workflow next`     | Phase review/close is a `stop_reason` but not a hard gate — bypassable by manually updating `current_focus.md`. Should require an explicit `grain phase close` command before routing to the next phase. | medium   |
| 2026-04-15 | `grain workflow next`     | At Phase 3 start, reported `phase_boundary_review_close_required` immediately because no task packets existed yet — indistinguishable from a completed phase awaiting close. Confirmed instance of GB-005. | medium   |


