# Daily Run Skill

Cross-cutting. The morning engine. This is the scheduled instruction that senses, reconciles, propagates, and drafts. Run it on a schedule (or invoke it by hand).

The full narrated version with rationale is in `instructions/daily-run.md`. This is the operational skill the model executes.

---

```
name: daily-run
description: >
  The daily operational run. Senses the last 24h of inbound, reconciles into
  the Workstream Tracker, propagates findings into the wiki, and drafts (never
  sends) follow-ups. Loads on schedule, or when the user says "run the daily",
  "morning run", or "do the daily update".

## Setup

Read these first for context: the brain's memory/identity file, the contacts
directory (to resolve follow-up recipients), and the per-workstream skills
(they are the playbook for each track).

## Step 1 — Pull the backbone

For each workstream task in the Workstream Tracker (project GID: [PROJECT_GID]),
get the open items with their current notes. This is the skeleton.

## Step 2 — Gather the signal

Read the last 24 hours of inbound. On Mondays widen to 72 to catch the weekend.
Sources: Outlook (new messages AND replies to prior follow-ups), Jira (items
updated in the window), Teams (status and blocker chatter). Read replies, not
just new arrivals. Treat empty channels as "no signal", not "nothing happened".

NOTE: Outlook, Jira, and Teams are what this example targets, but nothing is
specific to them. Any email, ticket, or chat system works the same way; you
just need an MCP connection into each. Substitute Gmail, Linear, Slack, or
whatever your work actually runs on.

## Step 3 — Reconcile into state

For each workstream with new signal:
- READ the current task first; PRESERVE the session log.
- Update status, completed, next actions, blockers, dates.
- Add a dated Session Log line citing the source.
- CHECK SELF-REPORTED STATUS AGAINST THE SOURCE OF TRUTH. If a status email or
  standup says on-track but the linked ticket is blocked, record the real state
  and flag the discrepancy for the report.
- If signal reveals untracked work, note it as a POSSIBLE new initiative. Do
  NOT auto-create tasks.
- Never modify a task in the wrong workstream.

## Step 4 — Propagate to the wiki

For each tracked entity touched this run, append a dated finding to its wiki
page's Key Findings section (newest first, confidence-tagged, never delete
priors). If a materially active entity has no page, CREATE one from the wiki
template. This is what makes the brain compound.

## Step 5 — Draft the actions

For anything overdue, at risk, blocked, awaiting a reply, or stale (no log
entry in 14+ days), draft a concise follow-up to the owner (resolve the address
from the contacts directory). Tone: direct, peer-to-peer, names the item, states
what is needed and by when.

Create these as DRAFTS only. NEVER send. Log each draft in the relevant task's
Session Log so the next run knows it is outstanding.

## Step 6 — Report and self-update

Produce a short report: counts updated by workstream, new flags and
discrepancies, wiki pages touched, and the list of drafts (recipient + subject)
for the user to review and send. Then update the brain's own memory and logs.
A run that ends without this leaves the brain stale.

## Hard rules

- Never send, post, commit, or delete. Draft and surface only.
- Asana is the source of truth for status. The wiki is the source of truth for
  understanding. Keep facts in the right one.
- No fabricated data. If a connector is unavailable, write one line to the log
  and stop without overwriting trackers.
```

---

Step 3's reconciliation rule and Step 5's draft-only rule are the two that matter most. The first is why the system catches drift between what people report and what the systems of record say. The second is the boundary that makes it safe to run unattended.
