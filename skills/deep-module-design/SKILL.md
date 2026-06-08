---
name: deep-module-design
description: Design or adjust a module so a small interface hides meaningful behavior and improves locality/testability.
---

# Deep Module Design

Use only when current slice friction suggests architecture should change.

## Inputs

Read task files from `<ORCHESTRATION_ROOT>/tasks/<task-id>/` plus `CONTEXT.md` and `docs/adr/`.

## Trigger signs

- One slice touches too many unrelated files.
- Logic is duplicated across callers.
- Interface is as complex as implementation.
- New service/helper/manager only passes through calls.
- Tests require excessive mocks.
- Error handling or invariants leak across layers.
- Next slice would spread the same knowledge further.

## Vocabulary

```text
Module: interface + implementation
Interface: everything callers must know
Depth: meaningful behavior behind small interface
Seam: boundary where behavior can vary
Adapter: concrete implementation behind seam
Locality: change concentrated in one place
Leverage: small interface enables many behaviors
```

## Process

Identify friction, callers, leaked knowledge, smallest useful seam, smallest public interface, hidden behavior, interface tests, and deletion test result.

## Output

```md
# Deep Module Candidate

## Current friction
...

## Proposed interface
...

## Hidden implementation
...

## Callers simplified
...

## Tests at interface
...

## Deletion test result
...

## Recommendation
Apply now | defer | reject
```

Do not refactor beyond what current/next slice needs.
