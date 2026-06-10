---
name: subagent-slice-development
description: Delegate one vertical slice to a subagent with strict scope, stop conditions, and compact handoff.
---

# Subagent Slice Development

Use for implementation sessions where subagents develop slices. 
In Pi, use the `subagent` tool if available.
If the `subagent` tool is not available, do not pretend delegation happened.
Instead, produce a subagent prompt for the user to run in a separate Pi session or tmux pane.

## Main agent responsibilities

Before spawning a subagent, provide only:

```text
- ORCHESTRATION_ROOT
- task-id
- slice name and number
- relevant Feature Intent sections
- slice plan
- current progress, including the slice table row
- applicable project-local instructions and constraints
- files/areas already known
- allowed scope
- disallowed scope
- verification expectations
- handoff format
```

Do not pass entire chat history unless required.

## Subagent prompt shape

```md
You are implementing exactly one vertical slice.

ORCHESTRATION_ROOT:
<ORCHESTRATION_ROOT>

Task ID:
<task-id>

Read:
- <ORCHESTRATION_ROOT>/tasks/<task-id>/TASK.md
- <ORCHESTRATION_ROOT>/tasks/<task-id>/FEATURE_INTENT.md
- <ORCHESTRATION_ROOT>/tasks/<task-id>/VERTICAL_PLAN.md
- <ORCHESTRATION_ROOT>/tasks/<task-id>/PROGRESS.md

Your slice:
<slice>

Rules:
- Obey project-local instructions over this generic prompt.
- Do not broaden scope.
- Do not implement future slices.
- Do not refactor unrelated code.
- Write/identify one failing check first.
- Implement the minimum cross-layer change.
- Verify communication between touched layers.
- Update progress only for your slice row and related evidence sections.
- Do not mark the slice `done` without review; leave it ready for `intent-slice-review`.

Return:
- files changed
- checks added
- checks run
- result
- assumptions
- risks
- suggested next step
```

## Main agent after subagent returns

Review diff, inspect checks, use `intent-slice-review`, update task-scoped `PROGRESS.md`, and spawn next subagent only if current slice passes.
