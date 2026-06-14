# Workstream Skill Template

Stamp one of these per workstream. Replace every `[BRACKETED]` token. Keep the structure.

---

```
name: [workstream-slug]-tracker
description: >
  Reads and updates the [WORKSTREAM NAME] track in the Workstream Tracker.
  Loads when the user says "update the [WORKSTREAM] tracker", "end of session
  for [WORKSTREAM]", "export status" while working on [WORKSTREAM], or is
  otherwise working on [WORKSTREAM] and asks to record status.

## Context

[WORKSTREAM NAME] is [one or two lines: what this workstream is, who owns it,
what "done" looks like]. Source of truth for delivery detail is [e.g. the
ticket system / the standup baseline doc / the compliance evidence folder].

## Target

- Project: Workstream Tracker (GID: [PROJECT_GID])
- Task: [WORKSTREAM NAME] (GID: [TASK_GID])

## Update procedure

When triggered:

1. READ the current task description first. Do not write blind.
2. PRESERVE the Session Log. You will append, never replace.
3. Update the description using the standard task template:
   - Status block: Priority, Category, % Complete, Last Session (today), Depends On
   - Completed: add anything newly done (cumulative list)
   - Next Actions: replace with current next steps
   - Blockers: current blockers, or "(none)"
   - Notes: update context worth keeping
   - Session Log: prepend one dated line describing this session, citing the
     source of any reconciled fact
4. SUBTASKS: mark completed deliverables done; add new deliverables as subtasks
   if they emerged. Do not duplicate existing subtasks.
5. SECTIONS: move the task if status warrants:
   Active=[SECTION_ACTIVE], Blocked=[SECTION_BLOCKED], Queued=[SECTION_QUEUED],
   Stale=[SECTION_STALE], Completed=[SECTION_COMPLETED]
6. CONFIRM the update back to the user in one line.

## Workstream-specific rules

[Optional. Add any rules unique to this track. Examples:
- "Always reconcile against the ticket system; do not record self-reported
  status without checking the source of truth."
- "Never transcribe customer PII into the task; reference the source document."
- "This track depends on [OTHER WORKSTREAM]; note slippage there as a blocker
  here."]
```

---

## How to fill it

- **Slug and name** — lowercase-hyphenated slug for the skill name; human name in the body.
- **Context** — keep it to two or three lines. Its job is to make the skill fire on the actual work, not just the literal trigger phrase.
- **GIDs** — the project GID is shared; the task GID is unique to this workstream. Get them from Asana once the task exists.
- **Workstream-specific rules** — this is where a track earns its own skill rather than sharing a generic one. A delivery track wants the "reconcile against tickets" rule. A compliance track wants the evidence rule. Put the thing that is true for *this* track and no other here.
