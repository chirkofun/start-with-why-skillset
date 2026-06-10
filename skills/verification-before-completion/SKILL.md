---
name: verification-before-completion
description: Verify all slices and intent before claiming the feature/fix is complete.
---

# Verification Before Completion

Use before saying done.

Prefer a verification subagent when available to audit task state and evidence. Model hint: moderate/fast model; use strong reasoning for high-risk releases or complex acceptance criteria.

If no `subagent` tool is available, perform verification directly or output the prompt below for a separate session. The main agent owns final completion lifecycle updates.

## Read

From `<ORCHESTRATION_ROOT>/tasks/<task-id>/`:

```text
TASK.md
CODEBASE_RESEARCH.md if present
FEATURE_INTENT.md
VERTICAL_PLAN.md
PROGRESS.md
VERIFICATION.md
```

Also inspect test output / CI status if available.

## Verify

1. `TASK.md` frontmatter is canonical; `TASKS.md`, `current-task.md`, and `PROGRESS.md` agree.
2. Every planned slice is listed and complete or explicitly deferred.
3. Every done slice has evidence, checks, and review verdict.
4. Every deferred slice has reason, impact, follow-up decision/task, and approval/source.
5. Acceptance checks are covered; non-goals were not violated.
6. Communication across touched layers was verified.
7. Regression checks pass or gaps are explicit.
8. Research assumptions that changed are reflected in progress/handoff.
9. Architecture notes and handoff/progress are current.

## Verification subagent prompt

```md
You are auditing completion readiness.

ORCHESTRATION_ROOT: <ORCHESTRATION_ROOT>
Task ID: <task-id>

Read the task files and available test/CI evidence.

Rules:
- Do not implement fixes.
- Do not mark the task complete.
- Check state consistency, slice evidence, deferred slices, acceptance checks, non-goals, communication checks, and known gaps.
- Draft/update VERIFICATION.md only if instructed by the main agent.
- Return compact evidence and a completion verdict.

Return:
- verdict: Complete | Partial | Blocked
- missing evidence
- failing/stale checks
- lifecycle inconsistencies
- risks/gaps
- recommended next action
```

## Output

Write/update `<ORCHESTRATION_ROOT>/tasks/<task-id>/VERIFICATION.md`.

If complete, the main agent updates:
- `TASK.md` frontmatter to `status: completed`, `phase: complete`, and `updated: YYYY-MM-DD`,
- `<ORCHESTRATION_ROOT>/TASKS.md`,
- `<ORCHESTRATION_ROOT>/current-task.md` to no active task and last completed task.

Completion with deferred slices is allowed only when they are explicitly non-blocking and acceptance checks still pass.

Archiving is separate. Archive only completed, superseded, abandoned, or obsolete tasks, and record `archived: true`, `archived_at`, and `archive_reason` in `TASK.md`.

Do not claim completion if evidence is missing.
