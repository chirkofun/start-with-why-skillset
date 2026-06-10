---
active_task: ""
active_task_path: ""
last_completed_task: ""
updated: ""
---

# Current Task

Routing pointer only. `TASK.md` owns lifecycle state.

No active task.

## Rules

- Only one active task is allowed per worktree/session.
- If switching tasks, update the previous task's `TASK.md` status before changing `active_task`.
- Do not resume a completed task silently; create a follow-up task unless the user explicitly asks to reopen it.
