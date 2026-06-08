# Intent + Vertical Slice Skillset v2

A compact, project-local AI-agent skillset for feature/fix work.

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
    PI.md
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

## Task identity rule

Before reading task-specific files, the agent must:

1. Determine `<ORCHESTRATION_ROOT>`.
2. Read `<ORCHESTRATION_ROOT>/current-task.md` if it exists.
3. Read the active task's `TASK.md`.
4. Compare current user request with the active task.
5. Continue only if the request clearly matches.
6. Otherwise create a new task folder.

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
