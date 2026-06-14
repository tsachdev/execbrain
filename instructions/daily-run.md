# The Daily Run, Narrated

The `skills/daily-run.md` file is the operational version the model executes. This is the same run with the reasoning attached, so you understand *why* each step is shaped the way it is before you adapt it.

The run does six things in order, and the order matters.

## Before anything: load context

The run reads the brain's own context first: the memory/identity file, the contacts directory (so it can resolve who a follow-up goes to), and the per-workstream skills (each track's playbook). This is the warm-up. Skipping it is how the run produces generic output that does not know your people or your priorities.

## Step 1 — Pull the backbone

Read every workstream's open items and current notes from Asana. This is the skeleton the run hangs everything on. You start from the state of record, not from a blank page, so the run is always reconciling against known truth rather than reconstructing from scratch.

## Step 2 — Gather the signal

Read the last 24 hours of inbound across your channels: Outlook, Jira, Teams (or your equivalents; you just need an MCP connection into each). Widen to 72 hours on Mondays to catch the weekend.

Two details that matter. Read **replies**, not just new messages, because the reply to a follow-up you sent last week is often the most important signal of the day. And treat an empty channel as *"no signal in the window"*, not *"nothing is happening"* — chat search in particular is not authoritative, so absence is not evidence.

This is the step that earns the system's keep. No human reliably reads everything across three channels every single morning. The brain does.

## Step 3 — Reconcile into state

This is the heart of the run. For each workstream with new signal: read the current task first, preserve the session log, then update status, next actions, blockers, and dates, and add a dated log line citing where the update came from.

The rule that makes this powerful: **check self-reported status against the source of truth.** A status email or a standup line that says "on track" is a claim. The ticket system is the fact. When they disagree, the ticket wins, and the disagreement itself is worth surfacing, because the gap between what people believe and what the systems show is where slippage hides. (The worked example in `examples/` is exactly this: a track reported on-track, a linked ticket actually blocked on a customer input, surfaced early enough to clear with a 15-minute call.)

Two guardrails. If the signal reveals work that is not tracked anywhere, note it as a *possible* new initiative but do not auto-create a task; creating is a decision, surfacing is safe. And never modify a task in the wrong workstream; when in doubt, leave it and flag it.

## Step 4 — Propagate to the wiki

After state is reconciled, push the material findings into the knowledge wiki. A new fact about an account goes on that account's page; a new wrinkle in an initiative goes on its page. Findings are dated, one or two lines, confidence-tagged, newest first, and never deleted. If something materially active has no page yet, create one from the template.

This is the step that makes the brain *compound* instead of merely refresh. State tells you where things stand today. The wiki accumulates understanding that pays off months later when you need the history of a relationship or a decision.

## Step 5 — Draft the actions

For anything overdue, at risk, blocked, awaiting a reply, or gone quiet (no log entry in 14+ days), draft a follow-up to the owner. Concise, peer-to-peer, names the item, states what is needed and by when.

Create these as **drafts only. Never send.** Log each draft in the relevant task so the next run knows it is outstanding and does not nag again. This is the boundary that makes the whole thing safe to run unattended; it has its own file, `behavior-rules.md`, because it is the most important rule in the system.

## Step 6 — Report and self-update

Produce a short report: counts updated by workstream, new flags and discrepancies, wiki pages touched, and the list of drafts for you to review and send. Then the run updates the brain's own memory and logs.

That last part is not optional. A run that ends without updating the brain leaves it stale, and a stale brain is worse than none, because you will trust it and it will be wrong.

## On scheduling

Run it every morning before you start. If your tool supports scheduled or cloud runs, automate it; if not, invoke it by hand as the first thing you do. The value is in the cadence. A sensing loop you run twice a week is a sensing loop with three-day blind spots.
