# Example: Customer Implementation Delivery Skill

A filled-in per-workstream skill, stamped from the template. This is the track the deep worked example runs on (see `examples/northwind-apparel.md`). GIDs are placeholders.

---

```
name: customer-implementation-tracker
description: >
  Reads and updates the Customer Implementation Delivery track in the
  Workstream Tracker. Loads when the user says "update the implementation
  tracker", "end of session for delivery", "export status" while working on a
  customer go-live, or is reviewing implementation status and asks to record it.

## Context

Customer Implementation Delivery covers active customer go-lives: requirements
through hypercare. Owned by the engineering delivery lead. "Done" is a stable
production go-live past hypercare. Source of truth for delivery detail is the
ticket system, NOT self-reported status in email or standups. Self-reported
status and ticket status drift; this skill exists partly to catch that drift.

## Target

- Project: Workstream Tracker (GID: 0000000000000000)
- Task: Customer Implementation Delivery (GID: 1111111111111111)

## Update procedure

When triggered:

1. READ the current task description first. Do not write blind.
2. PRESERVE the Session Log. Append, never replace.
3. Update the description using the standard task template:
   - Status: Priority, Category=Customer Delivery, % Complete, Last Session
     (today), Depends On
   - Completed: add newly landed milestones (cumulative)
   - Next Actions: current next steps
   - Blockers: current blockers, or "(none)"
   - Notes: update context, including the per-customer go-live dates and the
     two-tier risk picture (visible blockers vs. the real long-pole)
   - Session Log: prepend one dated line, citing the source of each reconciled
     fact (ticket ID, standup doc, customer email)
4. SUBTASKS: the standard delivery deliverables are Requirements sign-off,
   Integration build, Data migration, UAT, Go-live readiness, Hypercare. Mark
   done as they land; add customer-specific items as needed.
5. SECTIONS: Active=2222..., Blocked=3333..., Queued=4444..., Stale=5555...,
   Completed=6666...
6. CONFIRM the update in one line.

## Workstream-specific rules

- RECONCILE AGAINST TICKETS. Never record "on track" from a self-reported
  status alone. Pull the linked tickets and check their real state. If a ticket
  is blocked while the narrative says on-track, flag the discrepancy in the
  report and draft a follow-up. Reconciliation is the point of this track.
- DISTINGUISH THE LONG-POLE. A go-live often has a visible blocker everyone is
  watching and a real long-pole that is quieter and lands later. Track both in
  Notes. The visible one is rarely the one that slips the date.
- CUSTOMER PII STAYS OUT. Do not transcribe customer data, contacts, or account
  details into the task. Reference the source document instead.
```

---

This skill carries one rule that defines the whole track: **reconcile against the ticket system, never trust self-reported status alone.** That single rule is what surfaced the blocked ticket in the worked example, and it is the kind of thing that belongs in a per-workstream skill rather than a generic one, because it is true for delivery and not for, say, a content workstream.
