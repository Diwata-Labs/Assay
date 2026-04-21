# Task: Integrate formatter with runner output path

## Metadata
- **ID:** P4-T04-TASK-0019
- **Status:** done
- **Phase:** Phase 4 — Task Packet Formatter
- **Backlog:** P4-T04
- **Packet Path:** tasks/P4-T04-TASK-0019/
- **Dependencies:** P4-T01-TASK-0016, P4-T02-TASK-0017, P3-T04-TASK-0014
- **Primary Adapter:** code_adapter
- **Secondary Adapters:** none

## Objective
Wire `format_packet()` and `write_packet()` into the `assay run` CLI command so that after every run a Grain Sentinel JSON file is written to the output directory.

## Why This Task Exists
P4-T01 and P4-T02 built the formatter and writer in isolation. This task connects them to the live run path so `assay run` produces an actionable output file on every execution.

## Scope
- Modify `src/assay/cli/main.py` `run()`: after `collect_artifacts()`, call `format_packet(bundle)` then `write_packet(packet, output_dir)`
- Print the packet file path on success: `f"packet: {packet_path}"`
- Update `tests/test_run_command.py`: add mock for writer and assert packet path printed

## Constraints
- No change to exit code logic
- `write_packet` failure should surface as exit 1 with error message
- `task_id` passed as None for all runner-path calls in v1

## Escalation Conditions
- None
