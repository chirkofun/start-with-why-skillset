# Start-With-Why Skillset (Beta Version)

A compact, project-local AI-agent skillset for feature/fix work. Still in Beta.

## Inspired by:

- [Superpowers](https://github.com/obra/superpowers)
- [Skills by Matt Pocock](https://github.com/mattpocock/skills)

This version uses a configurable orchestration folder:

```text
<ORCHESTRATION_ROOT>
```

Examples:

```text
PI agent      -> .pi
Claude Code   -> .claude
Generic agent -> .agent
```

The orchestration root must be project-local, not global.

## Core philosophy

The agent may explore horizontally, but it must implement vertically.

```text
Understand intention
→ create task-scoped intent
→ plan vertical slices
→ implement one slice
→ verify communication between touched layers
→ review against intent
→ continue
```

## Project-local structure

Recommended PI layout:

```text
project/
  .pi/
    orchestration.md
    SYSTEM.md
    TASKS.md
    current-task.md
    skills/
    templates/
    tasks/
      <task-id>/
        TASK.md
        FEATURE_INTENT.md
        VERTICAL_PLAN.md
        PROGRESS.md
        HANDOFF.md
        VERIFICATION.md
        ARCHITECTURE_RADAR.md
  CONTEXT.md
  docs/adr/
```

For Claude Code, replace `.pi` with `.claude`.

## ORCHESTRATION_ROOT

Every skill must use task-specific state from:

```text
<ORCHESTRATION_ROOT>/tasks/<task-id>/
```

Do not hardcode `.agent`, `.pi`, or `.claude` inside reusable skills.

## Project instruction precedence

Always obey project-local instructions over generic skill instructions.

Before planning or implementation, inspect applicable project files such as:

```text
AGENTS.md
CLAUDE.md
SYSTEM.md
CONTEXT.md
docs/adr/
```

If project instructions conflict with this skillset, follow the project instructions. If project instructions conflict with the user request, ask before proceeding.

Examples: use required wrapper scripts, avoid direct Docker commands when prohibited, and follow local branch/base-branch rules.

Recommended precedence:

```text
system/developer instructions
→ project-local instructions
→ user request
→ skill instructions
→ generic defaults
```

Capture durable project constraints in task-scoped `FEATURE_INTENT.md`.

## Structured task state

Task-state Markdown files managed by this skillset should include YAML frontmatter. The frontmatter is the authoritative structured state; the Markdown body is for context, decisions, and evidence.

Minimum `TASK.md` frontmatter:

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

Task statuses:

```text
new, planned, active, paused, blocked, deferred, completed, archived, superseded
```

Task phases:

```text
intent, planning, implementation, review, verification, complete
```

## Task lifecycle rules

- Only one task may be current per worktree/session.
- New feature/fix requests create new tasks unless the user clearly says to continue the active task.
- If another task is already active in the same worktree/session, ask whether to switch, pause, or use a separate worktree.
- Completed tasks must not be silently resumed. Create a follow-up task unless the user explicitly asks to reopen.
- Reopening a completed task must record `reopened_at` and `reopen_reason` in `TASK.md`.
- Archive completed, superseded, abandoned, or intentionally obsolete tasks by setting `status: archived`, `archived: true`, and recording an archive reason.
- Map implementation tasks to a branch; use separate worktrees for parallel active tasks.
- Branch from `main` by default unless project-local instructions say otherwise.
- Deferred slices must be listed in `PROGRESS.md` with reason, impact, and follow-up decision.

## Slice-based progress

`PROGRESS.md` must make slice verification easy:

```md
| Slice | Status | Evidence | Checks | Review Verdict |
|---|---|---|---|---|
```

Allowed slice statuses:

```text
planned, in_progress, blocked, done, deferred, failed_review
```

Every completed slice needs evidence, checks, and a review verdict. Every deferred slice needs a reason, impact, and follow-up decision.

## Task identity rule

Before reading task-specific files, the agent must:

1. Determine `<ORCHESTRATION_ROOT>`.
2. Read `<ORCHESTRATION_ROOT>/current-task.md` if it exists.
3. Read the active task's `TASK.md`.
4. Compare current user request with the active task.
5. Continue only if the request clearly matches and the task is not completed or archived.
6. If the matching task is completed/archived, create a follow-up unless the user explicitly asks to reopen.
7. Otherwise create a new task folder.

Never reuse old task state just because files exist.

## Session split

Planning session:

```text
using-skillset
align-intent
plan-vertical-slices
handoff-session
```

Implementation session:

```text
using-skillset
subagent-slice-development
tdd-vertical-slice
intent-slice-review
repeat
verification-before-completion
```
