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
Do not ask questions before inspecting obvious code/docs.

## Preconditions

`using-skillset` must have determined `<ORCHESTRATION_ROOT>` and `<task-id>`.

If no matching task exists, create:

```text
<ORCHESTRATION_ROOT>/tasks/<task-id>/
```

where `<task-id>` is:

```text
YYYY-MM-DD-short-slug
```

Also create/update:

```text
<ORCHESTRATION_ROOT>/tasks/<task-id>/TASK.md
<ORCHESTRATION_ROOT>/TASKS.md
<ORCHESTRATION_ROOT>/current-task.md
```

## Process

1. Restate the request as intent, destination, and observable behaviors.
2. Inspect relevant repo/docs first.
3. Ask only blocking questions.
4. Ask max 5 questions by default.
5. For each question, include your recommended answer.
6. Capture facts, not guesses.
7. Write/update task-scoped `FEATURE_INTENT.md`.

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
