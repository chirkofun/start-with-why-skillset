---
name: improve-codebase-architecture
description: Explore architecture for deep-module opportunities without immediately refactoring.
---

# Improve Codebase Architecture

Goal: find high-leverage architecture improvements that make future slices easier.

Do not implement by default. Do not invent abstractions before observing friction.

## Read

Project-wide:

```text
CONTEXT.md
docs/adr/
```

Task-specific, if relevant:

```text
<ORCHESTRATION_ROOT>/tasks/<task-id>/FEATURE_INTENT.md
<ORCHESTRATION_ROOT>/tasks/<task-id>/VERTICAL_PLAN.md
<ORCHESTRATION_ROOT>/tasks/<task-id>/PROGRESS.md
```

## Look for

Shallow modules, pass-through abstractions, duplicated behavior, scattered invariants, excessive mocking, poor locality, APIs exposing too much process knowledge, and missing seams around external systems.

## Output

Update task-specific `<ORCHESTRATION_ROOT>/tasks/<task-id>/ARCHITECTURE_RADAR.md` or project-wide `<ORCHESTRATION_ROOT>/architecture-radar.md`.

Propose candidates first. Implement only after user/main-agent approval or when required to finish the current vertical slice.
