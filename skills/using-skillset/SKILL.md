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

## Respect project instructions

Before research, planning, or implementation, inspect applicable project-local instructions:

```text
AGENTS.md
CLAUDE.md
SYSTEM.md
CONTEXT.md
docs/adr/
```

Also check for nearer-scoped instruction files in directories you will touch.

Rules:
- Always obey project-local instructions over generic skill instructions.
- Capture durable constraints in task-scoped `FEATURE_INTENT.md`.
- If project instructions conflict with this skillset, follow the project instructions.
- If project instructions conflict with the user request, ask before proceeding.
- Examples: use required wrapper scripts, avoid direct Docker commands when prohibited, and follow local branch/base-branch rules.

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

## Structured state rule

New or modified task-state files managed by this skillset must include YAML frontmatter. Legacy files without frontmatter must be migrated before lifecycle routing depends on them.

`TASK.md` frontmatter is the canonical lifecycle source. Other task-state frontmatter is contextual metadata or a point-in-time snapshot; it must not override `TASK.md`.

Minimum task state:

```yaml
task_id: 2026-06-08-upload-retry
status: planned
phase: implementation
current_slice: 1
created: 2026-06-08
updated: 2026-06-08
base_branch: main
branch: feature/2026-06-08-upload-retry
worktree: ../worktrees/2026-06-08-upload-retry
archived: false
```

Allowed task statuses:

```text
new, planned, active, paused, blocked, deferred, completed, archived, superseded
```

Allowed phases:

```text
research, intent, planning, implementation, review, verification, complete
```

## Task identity check

Before reading task-specific files:

1. Read `<ORCHESTRATION_ROOT>/current-task.md` as a routing pointer.
2. If it points to a task, read `<ORCHESTRATION_ROOT>/tasks/<task-id>/TASK.md`.
3. Check the active task status and lifecycle state from `TASK.md` frontmatter.
4. If the active task is `completed` or `archived`, do not resume it silently; create a follow-up task unless the user explicitly asks to reopen it.
5. Compare active task to user's current request.
6. If the request clearly continues a non-completed active task, use that task.
7. If the request is a new feature/fix, create a new task.
8. If another task is active in this worktree/session, ask whether to switch, pause it, or use a separate worktree.
9. If uncertain, ask one short question with a recommended answer.

Default: new feature/fix request means new task unless user says continue.

## Task lifecycle rules

- Only one current task is allowed per worktree/session.
- When switching away from unfinished work, update the previous task's `TASK.md` status before changing `current-task.md`.
- When implementation starts, set task status to `active` and record branch/worktree when applicable.
- Branch from `main` by default unless project-local instructions say otherwise.
- If the current git branch does not match the task branch, warn before editing.
- Use separate worktrees for parallel active tasks.
- A task may be marked `completed` only after `verification-before-completion` passes.
- Archive completed, superseded, abandoned, or obsolete tasks by setting `status: archived`, `archived: true`, `archived_at`, and `archive_reason`.
- Reopen completed tasks only on explicit request; record `reopened_at` and `reopen_reason` and preserve prior verification evidence.
- Mark deferred slices in `PROGRESS.md` with reason, impact, follow-up task/decision, and approval/source.

## Task path rule

Task files live only here:

```text
<ORCHESTRATION_ROOT>/tasks/<task-id>/
```

Never read task-specific files from the root orchestration folder.

## Route

Feature/fix:

```text
no matching task     -> create task shell -> codebase-research
research missing     -> codebase-research for non-trivial requests
intent unclear       -> align-intent
intent clear/no plan -> plan-vertical-slices
plan exists/code     -> tdd-vertical-slice or subagent-slice-development
slice completed      -> intent-slice-review
before done          -> verification-before-completion
```

Bug:

```text
codebase-research -> align-intent -> systematic-debugging-slice -> plan-vertical-slices
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
- project instructions read,
- active lifecycle status,
- missing required state,
- next action.
