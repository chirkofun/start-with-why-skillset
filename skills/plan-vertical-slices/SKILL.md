---
name: plan-vertical-slices
description: Convert intent into independently verifiable vertical slices of observable behavior.
---

# Plan Vertical Slices

Goal: create/update:

```text
<ORCHESTRATION_ROOT>/tasks/<task-id>/VERTICAL_PLAN.md
<ORCHESTRATION_ROOT>/tasks/<task-id>/PROGRESS.md
```

Use task-scoped `FEATURE_INTENT.md` as source of truth.

## Preconditions

Read:

```text
<ORCHESTRATION_ROOT>/tasks/<task-id>/TASK.md
<ORCHESTRATION_ROOT>/tasks/<task-id>/FEATURE_INTENT.md
CONTEXT.md
docs/adr/
```

## Invalid plan

Reject horizontal plans:

```text
1. database
2. domain
3. API
4. UI
5. tests
```

## Valid plan

Plan by observable behavior:

```text
Slice 0: walking skeleton / tracer bullet
Slice 1: first valuable behavior
Slice 2: first failure or edge behavior
Slice 3: next behavior
```

Each slice must touch only the layers needed for that behavior.

## Slice template

```md
## Slice N: <observable behavior>

### Behavior
...

### User/System Value
...

### Layers touched
- UI:
- API:
- Domain:
- Persistence:
- External adapters:
- Tests:

### First failing check
...

### Minimal implementation
...

### Communication check
How this proves touched layers communicate.

### Verification
Commands/tests/manual checks.

### Stop condition
What must be true before next slice.

### Non-goals protected
...
```

## Planning rules

- Every slice must leave the system runnable.
- Every slice must be independently reviewable.
- Do not create future abstractions.
- Add seams only when the current or next slice needs them.
- Prefer deep modules over shallow glue.
- Keep slices small enough for subagents.

## Output

Write/update `VERTICAL_PLAN.md`, `PROGRESS.md`, and set `TASK.md` status to `planned`.
