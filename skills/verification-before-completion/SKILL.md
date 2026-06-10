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

1. `TASK.md` frontmatter is canonical; `TASKS.md`, `current-task.md`, and `PROGRESS.md` point to the same task and do not contradict it.
2. Every planned slice appears in the `PROGRESS.md` slice table.
3. Every planned slice is complete or explicitly deferred.
4. Every completed slice has evidence, checks, and a review verdict.
5. Every deferred slice has reason, impact, follow-up decision/task, and approval/source.
6. Acceptance checks are covered.
7. Non-goals were not violated.
8. Communication across touched layers was verified.
9. Previous behavior/regression checks pass.
10. Architecture notes are captured.
11. Handoff/progress is current.

## Output

Write/update `<ORCHESTRATION_ROOT>/tasks/<task-id>/VERIFICATION.md`.

If complete:
- update `TASK.md` frontmatter to `status: completed`, `phase: complete`, and `updated: YYYY-MM-DD`,
- update `<ORCHESTRATION_ROOT>/TASKS.md`,
- update `<ORCHESTRATION_ROOT>/current-task.md` to no active task and record the last completed task,
- preserve branch/worktree fields for traceability.

Completion with deferred slices is allowed only when deferred slices are explicitly non-blocking and acceptance checks still pass.

Archiving is a separate lifecycle transition. Archive only completed, superseded, abandoned, or obsolete tasks, and record `archived: true`, `archived_at`, and `archive_reason` in `TASK.md`.

Do not claim completion if evidence is missing.
