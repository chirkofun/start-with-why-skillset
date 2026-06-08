---
name: tdd-vertical-slice
description: Implement one vertical slice using one failing check, minimal cross-layer implementation, and verification.
---

# TDD Vertical Slice

Use when implementing one slice from `<ORCHESTRATION_ROOT>/tasks/<task-id>/VERTICAL_PLAN.md`.

## Hard rules

Do not implement layer-by-layer.
Do not write all tests upfront.
Do not build future slices.
Do not create speculative interfaces.

## Loop

For the current slice:

1. Read `TASK.md`, `FEATURE_INTENT.md`, `VERTICAL_PLAN.md`, and `PROGRESS.md` from `<ORCHESTRATION_ROOT>/tasks/<task-id>/`.
2. Identify the slice stop condition.
3. Write or identify one failing check for the behavior.
4. Run it. Confirm it fails for the expected reason.
5. Implement the smallest change across required layers.
6. Run the slice check.
7. Run relevant regression checks.
8. Verify communication between touched layers.
9. Update task-scoped `PROGRESS.md`.

## Communication check

Explicitly confirm how data/control/error flows across touched boundaries.

Example:

```text
UI -> command handler -> domain service -> repository -> result -> UI state
```

## Completion output

```text
ORCHESTRATION_ROOT:
Task ID:
Slice:
Behavior:
Files changed:
Checks added:
Checks run:
Communication verified:
Intent match:
Ready for intent-slice-review: yes/no
```
