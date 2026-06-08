---
name: using-skillset
description: Bootstrap and route this compact skillset. Use at session start and whenever the next workflow phase is unclear.
---

# Using Skillset

Load this first. Load other skills only when needed.

## Determine ORCHESTRATION_ROOT

Set `<ORCHESTRATION_ROOT>` before doing anything else.

Order:

1. If `.pi/orchestration.md` exists, use `.pi`.
2. Else if `.claude/orchestration.md` exists, use `.claude`.
3. Else if the user/tool configured another project-local root, use that.
4. Else create/use `.pi` for PI agent.
5. Never use a global folder for task state.

## Required root files

Check or create:

```text
<ORCHESTRATION_ROOT>/orchestration.md
<ORCHESTRATION_ROOT>/TASKS.md
<ORCHESTRATION_ROOT>/current-task.md
<ORCHESTRATION_ROOT>/tasks/
```

Project context may live outside orchestration root:

```text
CONTEXT.md
docs/adr/
```

## Task identity check

Before reading task-specific files:

1. Read `<ORCHESTRATION_ROOT>/current-task.md`.
2. If it points to a task, read `<ORCHESTRATION_ROOT>/tasks/<task-id>/TASK.md`.
3. Compare active task to user's current request.
4. If the request clearly continues the task, use that task.
5. If the request is a new feature/fix, create a new task.
6. If uncertain, ask one short question with a recommended answer.

Default: new feature/fix request means new task unless user says continue.

## Task path rule

Task files live only here:

```text
<ORCHESTRATION_ROOT>/tasks/<task-id>/
```

Never read task-specific files from the root orchestration folder.

## Route

Feature/fix:

```text
no matching task     -> create task -> align-intent
intent unclear       -> align-intent
intent clear/no plan -> plan-vertical-slices
plan exists/code     -> tdd-vertical-slice or subagent-slice-development
slice completed      -> intent-slice-review
before done          -> verification-before-completion
```

Bug:

```text
align-intent -> systematic-debugging-slice -> plan-vertical-slices
```

Architecture:

```text
improve-codebase-architecture -> deep-module-design
```

## Output

State:
- ORCHESTRATION_ROOT,
- task-id,
- current phase,
- loaded skill,
- missing required state,
- next action.
