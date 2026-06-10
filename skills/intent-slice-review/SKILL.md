---
name: intent-slice-review
description: Review a completed slice against feature intent, vertical plan, tests, and deep-module quality.
---

# Intent Slice Review

Use after each slice, before starting the next one.

Prefer a review subagent when available to keep implementation context out of the main agent. Model hint: strong reasoning model; fast/moderate is acceptable for tiny diffs.

If no `subagent` tool is available, perform the review directly or output the prompt below for a separate session. The main agent owns final `PROGRESS.md` and `TASK.md` lifecycle updates.

## Inputs

Read from `<ORCHESTRATION_ROOT>/tasks/<task-id>/`:

```text
TASK.md
CODEBASE_RESEARCH.md if present
FEATURE_INTENT.md
VERTICAL_PLAN.md
PROGRESS.md
```

Also inspect current diff, changed files, and test results.

## Review checklist

```text
Intent match: yes|partial|no
Destination progress: yes|partial|no
Slice stop condition met: yes|no
Communication verified: yes|partial|no
Acceptance checks covered: yes|partial|no
Non-goals violated: yes|no
Previous slices still valid: yes|unknown|no
Architecture quality: deepened|preserved|shallowed|unknown
```

Deep-module check: flag pass-through wrappers, leaked details, excessive mocks, scattered concepts, or improved locality/leverage/testability.

## Review subagent prompt

```md
You are reviewing exactly one completed vertical slice.

ORCHESTRATION_ROOT: <ORCHESTRATION_ROOT>
Task ID: <task-id>
Slice: <slice>

Read task files, inspect only the current diff/changed files and relevant test output.

Rules:
- Do not implement fixes.
- Do not broaden scope or review future slices.
- Check intent, stop condition, tests, communication, non-goals, and deep-module quality.
- Return a compact verdict with evidence and required fixes.

Return:
- verdict: Proceed | Fix current slice | Re-plan | Architecture review needed
- evidence
- required fixes
- risks
- recommended next skill
```

## Output

```md
# Slice Review

## Verdict
Proceed | Fix current slice | Re-plan | Architecture review needed

## Evidence
...

## Required fixes before next slice
- ...

## Next skill
...
```

Update task-scoped `PROGRESS.md` with the verdict in the slice table.

Rules:
- If verdict is `Proceed`, mark the reviewed slice `done`, include evidence/checks, and advance `TASK.md` frontmatter `current_slice`.
- If verdict is `Fix current slice`, mark the slice `failed_review` or `in_progress` with required fixes.
- If verdict is `Re-plan`, update `TASK.md` frontmatter to `phase: planning` and do not start another slice.
- If a slice is intentionally postponed, mark it `deferred` with reason, impact, follow-up task/decision, and approval/source.
