# Grain Bug Log

Bugs and workflow gaps discovered while building Assay with Grain.

---

## GB-001 — `grain task prepare` does not detect stub packet files

**Status:** open
**Discovered:** 2026-04-15 during P1-T04 and P1-T05 execution

### Description

`grain task prepare` reports `ok` with `missing_inputs: 0` even when `context.md`, `plan.md`, and `deliverable_spec.md` are all unedited template stubs. These files are created by `grain task create` with placeholder content (e.g. `[what is included]`, `[One clear paragraph.]`) and are intended to be filled in by the AI as part of the execute prompt (Steps 4 and 7 of `tasks.next_and_implement.md`). When the execute prompt is not followed — for example, when a user asks the AI to execute a task directly in an ongoing conversation — the planning files are never populated and remain as stubs indefinitely.

### Why it matters

- Stub planning files are silent — there's no warning at execution time that they were skipped
- Reviewing or auditing a completed task is harder when context/plan/deliverable_spec contain only placeholder text
- `grain task prepare` is the natural pre-execution gate and should catch this

### Reproduction

1. Run `grain task create --phase N --task-num N --title "any"`
2. Run `grain task prepare --id <new-id>`
3. Observe: `ok`, `missing_inputs: 0` despite all three planning files being stub templates

### Suggested Fix

Add stub detection to `grain task prepare`. A file is a stub if it contains any unresolved placeholder tokens (e.g. `[`, `####`). Flag detected stubs as `missing_inputs` and block the `ok` status until they are populated.

Alternatively, support a `--simple` mode that skips these files entirely for small mechanical tasks (see GB-002).

---

## GB-002 — No lightweight packet mode for small tasks

**Status:** open
**Discovered:** 2026-04-15 during P1-T05 execution

### Description

`grain task create` always generates a full 7-file packet: `task_packet.md`, `task.md`, `context.md`, `plan.md`, `deliverable_spec.md`, `results.md`, `handoff.md`. For small, mechanical tasks (e.g. "create a Makefile", "add a dependency"), `context.md`, `plan.md`, and `deliverable_spec.md` add overhead without proportional value. Their content is often self-evident from the task description.

### Why it matters

- The overhead discourages proper packet usage for small tasks
- It creates pressure to skip the planning files (leading to GB-001 above)
- A minimal packet (`task.md` + `results.md`) would be sufficient for many Phase 1-type foundation tasks

### Suggested Fix

Add a `--simple` flag to `grain task create` that generates only `task.md` + `results.md`. The full packet remains default for larger/complex tasks. Optionally, `grain task prepare` could recommend `--simple` when it detects a task that doesn't warrant full planning files.

---

## GB-003 — Execute prompt is fragile when AI session is already in progress

**Status:** open
**Discovered:** 2026-04-15 during multiple task executions

### Description

The execute workflow (`prompts/task.execute.md` → `prompts/tasks.next_and_implement.md`) is designed as a cold-start AI prompt — the user pastes it into a fresh conversation. When a user instead asks an already-running AI assistant to "execute the next task," the assistant naturally jumps to implementation without reading the execute prompt, skipping packet generation steps (context, plan, deliverable_spec) and efficiency tracking fields in results.md.

There is no mechanism that enforces the execute prompt is followed before implementation proceeds.

### Why it matters

- All packet planning files end up as stubs (GB-001 downstream)
- Efficiency metrics in results.md are inconsistently filled
- The workflow depends on a convention the user must manually enforce

### Suggested Fix

Two options:
1. `grain task prepare` outputs the path to the relevant prompt and warns if the active task has stub planning files — nudging the user to restart with the correct prompt
2. Document the intended session boundary more prominently: "always start a new conversation for task execution using prompts/task.execute.md"

