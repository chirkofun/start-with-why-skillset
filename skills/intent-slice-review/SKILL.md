---
name: intent-slice-review
description: Review a completed slice against feature intent, vertical plan, tests, and deep-module quality.
---

# Intent Slice Review

Use after each slice, before starting the next one.

## Inputs

Read from `<ORCHESTRATION_ROOT>/tasks/<task-id>/`:

```text
TASK.md
FEATURE_INTENT.md
VERTICAL_PLAN.md
PROGRESS.md
```

Also inspect current diff / changed files and test results.

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

## Deep module check

Ask whether this added pass-through wrappers, leaked implementation details, required excessive mocks, spread one concept across many files, or improved locality/leverage/testability.

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
- If verdict is `Proceed`, mark the reviewed slice `done`, include evidence and checks, and advance `current_slice` to the next planned slice.
- If verdict is `Fix current slice`, mark the slice `failed_review` or `in_progress` with required fixes.
- If verdict is `Re-plan`, update `TASK.md` frontmatter to `phase: planning` and do not start another slice.
- If a slice is intentionally postponed, mark it `deferred` with reason, impact, follow-up task/decision, and approval/source.
