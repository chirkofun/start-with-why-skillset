---
name: systematic-debugging-slice
description: Debug by reproducing one failing behavior, finding cause, and fixing via a vertical slice.
---

# Systematic Debugging Slice

Use for bugs.

## Inputs

Use task-scoped files from `<ORCHESTRATION_ROOT>/tasks/<task-id>/`. If bug intent does not exist, create a minimal `FEATURE_INTENT.md`.

## Process

1. Read task intent or create minimal bug intent.
2. Reproduce the failure.
3. Capture expected vs actual behavior.
4. Find the smallest failing check.
5. Trace through layers only as needed.
6. Identify root cause.
7. Plan the fix as a vertical slice.
8. Implement minimal fix.
9. Verify regression check.
10. Review against intent.

## Do not

- patch symptoms without reproduction,
- change multiple layers speculatively,
- refactor while debugging unless required to expose the seam,
- claim fixed without a regression check or clear manual verification.

## Output

```text
ORCHESTRATION_ROOT:
Task ID:
Bug behavior:
Reproduction:
Root cause:
Slice fix:
Check added/run:
Regression risk:
Next skill:
```
