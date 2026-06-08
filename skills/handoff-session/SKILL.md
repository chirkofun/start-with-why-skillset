---
name: handoff-session
description: Create compact handoff for a fresh session or subagent with only durable, high-signal state.
---

# Handoff Session

Use at end of planning session, before implementation session, or before spawning subagents.

## Read

From `<ORCHESTRATION_ROOT>/tasks/<task-id>/`:

```text
TASK.md
FEATURE_INTENT.md
VERTICAL_PLAN.md
PROGRESS.md
ARCHITECTURE_RADAR.md
```

## Write

```text
<ORCHESTRATION_ROOT>/tasks/<task-id>/HANDOFF.md
```

## Handoff format

```md
---
task_id: <task-id>
status: <status>
phase: <phase>
current_slice: <slice-or-null>
updated: YYYY-MM-DD
---

# Handoff

## ORCHESTRATION_ROOT
...

## Task ID
...

## Status
new | planned | active | paused | blocked | deferred | completed | archived | superseded

## Current phase
intent | planning | implementation | review | verification | complete

## Intent
...

## Destination
...

## Branch / worktree
...

## Current slice
...

## Slice Progress

| Slice | Status | Evidence | Checks | Review Verdict |
|---|---|---|---|---|

## Next slice
...

## Files/areas of interest
- ...

## Invariants / non-goals
- ...

## Verification commands
- ...

## Architecture notes
- ...

## Risks / assumptions
- ...

## Exact next instruction
...
```

Prefer terse facts over narrative.
