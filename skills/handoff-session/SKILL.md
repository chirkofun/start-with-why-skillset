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
# Handoff

## ORCHESTRATION_ROOT
...

## Task ID
...

## Current phase
Planning | Implementation | Review | Verification

## Intent
...

## Destination
...

## Current slice
...

## Completed slices
- ...

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
