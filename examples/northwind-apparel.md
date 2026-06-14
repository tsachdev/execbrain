# Worked Example: Northwind Apparel

One CTO workstream, end to end, showing every layer working together. Northwind Apparel is a fictional mid-market apparel retailer; the names, tickets, and release numbers are illustrative. This is the story that proves why the sensing loop matters.

## The setup

**Workstream:** Customer Implementation Delivery
**Customer:** Northwind Apparel (multi-channel go-live)
**Engineering delivery lead:** Maria Chen
**The track's defining rule** (from its per-workstream skill): *reconcile against the ticket system, never trust self-reported status alone.*

## The Asana task, before the run

```
# Customer Implementation Delivery

## Status
Priority: High
Category: Customer Delivery
% Complete: 70
Last Session: 2026-06-12
Depends On: none

## Completed
- Requirements sign-off
- Integration build (in progress)
- Environments provisioned

## Next Actions
- Close out remaining integration tickets
- Schedule UAT

## Blockers
- (none reported)

## Notes
Northwind multi-channel go-live targeted for Release 260616.1.
Per-customer go-live date: late June.

## Session Log
- 2026-06-12: Status from weekly standup; lead reports on track.
```

Subtasks: Requirements sign-off (done), Integration build (in progress), Data migration (open), UAT (open), Go-live readiness (open), Hypercare (open).

## The morning run

**Step 1 — backbone.** The run pulls Customer Implementation Delivery and sees it at 70%, no blockers, last touched from a standup that reported on track.

**Step 2 — signal.** The run reads the window. In email, nothing material from the delivery lead. In Jira, it reads the linked tickets directly rather than trusting the standup summary. One ticket, INT-4821 (a customer-facing configuration the integration needs), is sitting in **Blocked**, waiting on information from the customer. It has not moved in days.

**Step 3 — reconcile, and the catch.** Here the track's defining rule fires. The self-reported status said on track. The ticket system says one of the work items is blocked. The ticket wins. The run records the real state and flags the discrepancy:

```
## Status
...
% Complete: 70
Last Session: 2026-06-14
...

## Blockers
- INT-4821 blocked, awaiting configuration input from Northwind. Reported
  on-track at standup, but ticket has been in Blocked for several days.
  Discrepancy surfaced 2026-06-14.

## Session Log
- 2026-06-14: Reconciled against Jira. Standup reported on-track, but INT-4821
  is Blocked awaiting customer config input. Flagged discrepancy. Drafted
  nudge to Maria Chen. Source: Jira INT-4821.
- 2026-06-12: Status from weekly standup; lead reports on track.
```

**Step 4 — propagate.** The run appends a finding to the Northwind account's wiki page:

```
## Key Findings
- [2026-06-14] Go-live config dependency (INT-4821) stalled waiting on customer
  input; not reflected in self-reported status. Pattern: Northwind slow on
  config returns. Source: Jira INT-4821. (c:100)
```

That finding is knowledge, not status. Months later, "Northwind is slow returning configuration inputs" is exactly the kind of thing you want on the dossier before the next project with them.

**Step 5 — draft, never send.** The run drafts a one-line nudge and leaves it in the outbox:

> **To:** Maria Chen
> **Subject:** Northwind INT-4821 looks blocked
>
> Maria, the run flagged INT-4821 in Blocked, waiting on a config input from Northwind, though standup had the track on schedule. Worth a nudge to close the gap before it touches the 260616.1 date? Tushar

It logs the draft in the task so tomorrow's run knows it is outstanding and does not nag again.

**Step 6 — report.** The morning summary includes one flagged discrepancy: *Customer Implementation Delivery reported on-track, but INT-4821 is blocked on customer input; nudge drafted to Maria Chen.*

## What happened next

I read the morning report and sent the drafted nudge. Maria checked with the devs. The devs said a quick call with Northwind would resolve the config question faster than waiting on the ticket thread. She set up a 15-minute call the next day. The item cleared.

Nobody did anything wrong. The work was simply sitting in a queue, waiting passively on a customer reply, with no urgency attached to it. The reported status was optimistic, the ticket system held the truth, and the gap between them was where a quiet delay was hiding.

The brain did not catch a person. It caught **latency**. It compressed the time between a thing being stuck and a human deciding to do something about it, from "whenever the customer happens to reply" to "a 15-minute call tomorrow." That compression, repeated across a whole portfolio every morning, is the entire argument for the sensing loop.

## The layers, in this one story

- **State** (Asana): the task moved from "70%, no blockers" to "blocked on INT-4821," reconciled from the source of truth.
- **Knowledge** (wiki): a durable finding about Northwind's config-return pattern, useful long after this ticket closes.
- **Procedure** (skill): the track's rule, *reconcile against the ticket system*, is what made the catch automatic rather than lucky.
- **The boundary**: the run drafted the nudge and stopped. A human read it and sent it. The system surfaced; the person decided.
