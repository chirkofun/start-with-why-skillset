---
name: codebase-research
description: Quickly map relevant codebase context before intent clarification, preferably via a bounded subagent.
---

# Codebase Research

Goal: create/update a concise, task-scoped brief:

```text
<ORCHESTRATION_ROOT>/tasks/<task-id>/CODEBASE_RESEARCH.md
```

Use before `align-intent` for non-trivial feature/fix requests. Skip or keep minimal only when the user names the exact file/change or the task is documentation-only.

## Preconditions

`using-skillset` must have determined `<ORCHESTRATION_ROOT>` and inspected project-local instructions.

If no matching task exists, create `<task-id>` as `YYYY-MM-DD-short-slug`, create `<ORCHESTRATION_ROOT>/tasks/<task-id>/`, update `TASKS.md` and `current-task.md`, and create `TASK.md` with canonical frontmatter:

```yaml
task_id: <task-id>
status: new
phase: research
current_slice: null
created: YYYY-MM-DD
updated: YYYY-MM-DD
base_branch: main
branch: ""
worktree: ""
archived: false
```

Follow project-local branch/worktree instructions when they differ from defaults.

## Hard boundaries

Do not implement.
Do not ask the user questions.
Do not create a vertical plan.
Do not choose product behavior.
Do not do broad architecture review.
Do not read the whole repository.

Research returns likely, cited facts to help the main agent clarify intent.

## Use a research subagent when available

Model hint: cheap/fast model, low reasoning, good enough context.

In Pi, use the `subagent` tool if available. If not available, do not pretend delegation happened; either perform the bounded research directly or output the prompt below for a separate session.

Provide only:

```text
- ORCHESTRATION_ROOT
- task-id
- raw user request
- applicable project-local instructions
- task path
- allowed output file: CODEBASE_RESEARCH.md
- search budget and stop conditions
```

## Search ladder

1. Read orientation files that exist: `AGENTS.md`, `CLAUDE.md`, `SYSTEM.md`, `CONTEXT.md`, `README.md`, `docs/adr/`.
2. Inspect repo shape cheaply with file listing/search metadata.
3. Extract request terms: domain nouns, actions, labels, APIs, errors, integrations, filenames.
4. Run targeted searches from those terms.
5. Follow only 1-2 likely flows far enough to identify entry point, domain/orchestration, persistence/external adapter, and tests.
6. Stop when the brief can identify likely files, architecture flow, test entry points, pitfalls, unknowns, and questions enabled.

Default budget: about 10-20 targeted reads, less for small tasks. Prefer paths and summaries over pasted code.

## Output format

```md
---
task_id: <task-id>
updated: YYYY-MM-DD
research_confidence: Low | Medium | High
---

# Codebase Research

## Request Signal
...

## Project Instructions Read
- ...

## Search Strategy
- Terms searched:
- Entry points inspected:

## Architecture Snapshot
...

## Likely Files / Areas
| File/Area | Why relevant | Confidence |
|---|---|---|

## Existing Similar Behavior
- ...

## Tests / Verification Entry Points
- ...

## Constraints / Invariants
- ...

## Pitfalls
- ...

## Unknowns
- ...

## Questions This Enables
- Question:
  Recommended answer:
  Why it matters:

## Research Boundary
...
```

Keep the brief compact: max 12 likely files/areas and max 5 enabled questions.

## Subagent prompt shape

```md
You are researching codebase context before intent clarification.

ORCHESTRATION_ROOT:
<ORCHESTRATION_ROOT>

Task ID:
<task-id>

Raw request:
<user request>

Write only:
<ORCHESTRATION_ROOT>/tasks/<task-id>/CODEBASE_RESEARCH.md

Rules:
- Obey project-local instructions.
- Do not implement, plan slices, or ask the user questions.
- Follow the search ladder and stop early.
- Cite paths; do not paste large code blocks.
- Mark uncertain findings as likely/unknown.
- Keep output compact.

Return:
- brief path
- confidence
- highest-risk unknown
- suggested next skill: align-intent
```

## Completion gate

Output:

```text
Task ID:
Research brief:
Research confidence:
Likely areas:
Highest-risk unknown:
Recommended next skill: align-intent
```
