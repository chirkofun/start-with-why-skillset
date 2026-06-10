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

1. Read `TASK.md`, `CODEBASE_RESEARCH.md` if present, `FEATURE_INTENT.md`, `VERTICAL_PLAN.md`, and `PROGRESS.md` from `<ORCHESTRATION_ROOT>/tasks/<task-id>/`.
2. Confirm project-local instructions and task branch/worktree constraints still apply.
3. Identify the slice stop condition.
4. Set `TASK.md` frontmatter to `status: active`, `phase: implementation`, and the current slice.
5. Mark the slice `in_progress` in the `PROGRESS.md` slice table.
6. Write or identify one failing check for the behavior.
7. Run it. Confirm it fails for the expected reason.
8. Implement the smallest change across required layers.
9. Run the slice check.
10. Run relevant regression checks.
11. Verify communication between touched layers.
12. Update task-scoped `PROGRESS.md` with evidence, checks, files changed, and next action.

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

Do not mark the slice `done` until `intent-slice-review` records a `Proceed` verdict, unless the slice is explicitly deferred with reason, impact, and follow-up decision.
