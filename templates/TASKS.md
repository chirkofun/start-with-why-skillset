---
updated: ""
---

# Agent Tasks

| Task ID | Status | Phase | Current Slice | Branch | Worktree | Summary | Path |
|---|---|---|---|---|---|---|---|

## Task Status Rules

- `new`: task created, intent not yet aligned.
- `planned`: vertical plan exists, implementation not started.
- `active`: currently being worked in this worktree/session.
- `paused`: valid task, not current in this worktree/session.
- `blocked`: cannot continue without external input or dependency.
- `deferred`: task intentionally postponed.
- `completed`: verification passed; task should not be silently resumed.
- `archived`: no longer active in normal task routing.
- `superseded`: replaced by another task; see task frontmatter/body.
