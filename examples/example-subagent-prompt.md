# Example: Subagent Prompt

You are implementing exactly one vertical slice.

ORCHESTRATION_ROOT:
<ORCHESTRATION_ROOT>

Task ID:
<task-id>

Slice:
<copy one slice from VERTICAL_PLAN.md>

Relevant intent:
<copy only relevant sections from FEATURE_INTENT.md>

Rules:
- Obey project-local instructions over generic skill instructions.
- Do not broaden scope.
- Do not implement future slices.
- Do not refactor unrelated code.
- Write or identify one failing check first.
- Implement the minimum cross-layer change.
- Verify communication between touched layers.
- Update only your slice row/evidence in `PROGRESS.md`.
- Do not mark the slice `done`; leave it ready for review.
- Return compact evidence.
