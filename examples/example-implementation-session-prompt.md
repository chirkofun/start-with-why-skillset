# Example: Implementation Session Prompt

Use the intent + vertical slice skillset.

This is an implementation session.

Determine ORCHESTRATION_ROOT from the project. Use `.pi` unless another project-local root is configured.

Start with `using-skillset`.
Respect project-local instructions, task frontmatter, and branch/worktree lifecycle state.

Read:
- `<ORCHESTRATION_ROOT>/current-task.md`
- `<ORCHESTRATION_ROOT>/tasks/<task-id>/TASK.md`
- `<ORCHESTRATION_ROOT>/tasks/<task-id>/FEATURE_INTENT.md`
- `<ORCHESTRATION_ROOT>/tasks/<task-id>/VERTICAL_PLAN.md`
- `<ORCHESTRATION_ROOT>/tasks/<task-id>/PROGRESS.md`
- `<ORCHESTRATION_ROOT>/tasks/<task-id>/HANDOFF.md`

Implement only the next vertical slice.
