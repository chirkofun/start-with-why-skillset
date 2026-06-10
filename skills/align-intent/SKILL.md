---
name: align-intent
description: Establish compact shared understanding before planning a feature, fix, refactor, or behavior change.
---

# Align Intent

Goal: create or update:

```text
<ORCHESTRATION_ROOT>/tasks/<task-id>/FEATURE_INTENT.md
```

Do not implement.
Do not produce a full implementation plan.
Do not ask questions before reading `CODEBASE_RESEARCH.md` when present.

## Preconditions

`using-skillset` must have determined `<ORCHESTRATION_ROOT>`, resolved or requested a `<task-id>`, and inspected applicable project-local instructions (`AGENTS.md`, `CLAUDE.md`, `SYSTEM.md`, `CONTEXT.md`, `docs/adr/`, and nearer-scoped instruction files when relevant).

If no matching task exists, create the task shell, set `TASK.md` frontmatter to `status: new`, `phase: research`, `current_slice: null`, update `TASKS.md` and `current-task.md`, then route to `codebase-research` before continuing intent alignment.

Follow project-local branch/worktree instructions when they differ from defaults.

Read when available:

```text
<ORCHESTRATION_ROOT>/tasks/<task-id>/CODEBASE_RESEARCH.md
```

If `CODEBASE_RESEARCH.md` is missing for a non-trivial feature/fix, stop and recommend `codebase-research`. Skip only for trivial, exact-file, or documentation-only requests.

## Process

1. Restate the request as intent, destination, and observable behaviors.
2. Use `CODEBASE_RESEARCH.md` to ground questions; do not repeat broad research.
3. Do narrow inspection only to verify a blocking uncertainty.
4. Ask only blocking questions.
5. Ask max 5 questions by default.
6. For each question, include your recommended answer.
7. Capture facts, not guesses.
8. Capture durable project constraints in `FEATURE_INTENT.md`.
9. Write/update task-scoped `FEATURE_INTENT.md` and set `TASK.md` phase to `intent`.

## Feature Intent format

```md
# Feature Intent

## Intent
...

## Destination
...

## Observable Behaviors
- ...

## Non-Goals
- ...

## Constraints
- ...

## Research Used
- CODEBASE_RESEARCH.md:
- Research confidence:

## Existing System Facts
- ...

## Acceptance Checks
- ...

## Open Questions
- ...

## Riskiest Assumption
...
```

## Completion gate

Output:

```text
Task ID:
Task path:
Understanding confidence: High|Medium|Low
Destination:
Intention:
Riskiest assumption:
Recommended next skill: plan-vertical-slices
```
