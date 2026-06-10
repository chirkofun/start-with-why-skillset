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
- Always obey project-local `AGENTS.md`, `CLAUDE.md`, `SYSTEM.md`, `CONTEXT.md`, and nearby instruction files over generic skill instructions.
- Only one task may be current per worktree/session.

Task lifecycle:
- New/modified task-state files must include YAML frontmatter; migrate legacy files before routing depends on them.
- `TASK.md` frontmatter is the canonical lifecycle source; other frontmatter is contextual metadata or a snapshot.
- Task statuses: `new`, `planned`, `active`, `paused`, `blocked`, `deferred`, `completed`, `archived`, `superseded`.
- Task phases: `research`, `intent`, `planning`, `implementation`, `review`, `verification`, `complete`.
- Completed tasks must not be silently resumed; create a follow-up task unless the user explicitly asks to reopen.
- Archive only completed, superseded, abandoned, or intentionally obsolete tasks, and record the reason.
- Map each implementation task to a branch and, for parallel active work, a separate worktree.
- Mark deferred slices explicitly in `PROGRESS.md` with reason, impact, and follow-up decision.
