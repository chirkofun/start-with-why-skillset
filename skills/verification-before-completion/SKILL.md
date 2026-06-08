---
name: verification-before-completion
description: Verify all slices and intent before claiming the feature/fix is complete.
---

# Verification Before Completion

Use before saying done.

## Read

From `<ORCHESTRATION_ROOT>/tasks/<task-id>/`:

```text
TASK.md
FEATURE_INTENT.md
VERTICAL_PLAN.md
PROGRESS.md
VERIFICATION.md
```

Also inspect test output / CI status if available.

## Verify

1. Every planned slice is complete or explicitly deferred.
2. Every completed slice has evidence.
3. Acceptance checks are covered.
4. Non-goals were not violated.
5. Communication across touched layers was verified.
6. Previous behavior/regression checks pass.
7. Architecture notes are captured.
8. Handoff/progress is current.

## Output

Write/update `<ORCHESTRATION_ROOT>/tasks/<task-id>/VERIFICATION.md`.

If complete:
- update task `TASK.md` status to `done`,
- update `<ORCHESTRATION_ROOT>/TASKS.md`,
- update `<ORCHESTRATION_ROOT>/current-task.md` to no active task or last completed task.

Do not claim completion if evidence is missing.
