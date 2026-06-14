# Task Template

Every workstream task uses this exact structure in its **description**. The LLM reads and writes it as a structured document. Consistency is what lets the model parse and update it reliably across sessions.

## The format

```
## Status
Priority: [High/Medium/Low]
Category: [your categories, e.g. Transformation / Delivery / Compliance / Customer]
% Complete: [0-100]
Last Session: [YYYY-MM-DD]
Depends On: [workstream name or "none"]

## Completed
- [cumulative bullet list of everything done to date]

## Next Actions
- [immediate next steps]

## Blockers
- [list, or "(none)"]

## Notes
[context worth preserving: decisions, constraints, source-of-truth references]

## Session Log
- [YYYY-MM-DD]: [what happened this session, citing the source of any update]
- [YYYY-MM-DD]: [previous session]
```

## Rules

- **Completed is cumulative.** It grows; it is the full history of what is done, not just this session.
- **Session Log is append-only and newest-first.** Add today's line at the top. Never delete a prior line. This is non-negotiable.
- **Everything else is overwritten** on each update to reflect current state.
- **Cite sources in the log.** "Reconciled from ticket INT-4821" or "per the weekly standup doc" so a later run knows where a fact came from and how much to trust it.
- **Last Session drives staleness.** The run compares it to today to decide whether a task is going stale.

## Why the description, not just custom fields

Custom fields are great for sorting in Asana's UI, but they are flat. The description holds the *narrative*: what is done, what is next, why something is blocked, what happened when. The LLM works from the description as its primary read/write surface, and the description works on every plan including free. Treat the fields as a UI convenience and the description as the source of truth.
