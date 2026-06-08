# Orchestration Config

ORCHESTRATION_ROOT=.pi

This folder is project-local.

Task state lives in:

```text
<ORCHESTRATION_ROOT>/tasks/<task-id>/
```

Reusable skills live in:

```text
<ORCHESTRATION_ROOT>/skills/
```

Rules:
- Never read task state from another project.
- Never use global task state.
- Never reuse old task state unless active task identity matches the user request.
- All task-specific files must live under `tasks/<task-id>/`.
