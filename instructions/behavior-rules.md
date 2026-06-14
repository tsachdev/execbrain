# Behavior Rules

The rules that make the system safe, durable, and honest. These belong in your brain's behavior file (e.g. `CLAUDE.md`) so they apply to every session, not just the daily run.

## Rule 1: Draft, never send

The system can read anything, reconcile anything, draft anything. It **cannot send, post, commit, merge, or delete.** Every irreversible action is gated on a human.

This is the most important rule in the system and it is deliberate. The whole field is moving toward more autonomy: hand the agent the keys, let it act on a schedule, close the loop end to end. For anything that touches the outside world on your behalf, that is a mistake. An assistant that reads everything and proposes is a force multiplier. An assistant that sends on your behalf is a liability waiting for its first bad inference, and they all have a bad inference eventually.

So: autonomy everywhere the action is reversible, a human gate at every door that only opens one way. You can let this run unattended precisely because it cannot do anything you cannot undo. When the run wants to follow up, it drafts and leaves it in your outbox. You read and send.

## Rule 2: Keep sensitive things out of the brain

The brain reads a lot, and not everything it reads belongs in a file that sits in plain text. Government identifiers, account numbers, customer PII, anything you would not want persisted in markdown, stays out by standing rule. When the brain encounters such a value, it references the **source document** instead of transcribing the value.

Write this into the behavior file from day one. It is far easier than scrubbing later, and it has saved more than one practitioner from themselves.

## Rule 3: The maintenance contract

Every note-taking system dies the same death: the upkeep falls to a human who eventually stops, and the system rots into a graveyard. The fix is to make the model the maintainer and yourself the schema author.

After every completed task, the brain updates its own memory, appends to its history log, and refreshes the relevant state. This is non-negotiable and it is written as a hard rule, not a suggestion. A session that ends without these updates leaves the brain stale. Enforce it the way you would enforce a test suite: the work is not done until the brain is updated.

## The source-of-truth split

State lives in the database. Understanding lives in the wiki. The same input often produces both, and they go to different places.

- "The review is done, ships Friday" → **state** (Asana task)
- "Their real blocker is a customer input nobody chased, not the thing everyone is watching" → **knowledge** (wiki page)

If you let status leak into the wiki, the wiki rots into a log. If you let narrative leak into the database, the database becomes unsortable prose. Keep the line clean.

## The honest friction

What the one-hour tutorials leave out, because you only hit it on day three.

**It picks up partial or stale information at first.** Early runs grab the wrong thing or an old thing and write it down confidently. You correct by hand more than you would like. This fades as the wiki fills in and the model has context for who and what matters, but the first week is a teaching week. Budget for it.

**Every track needs a cold-start anchor.** The biggest fix. The system cannot bootstrap a workstream's status from nothing. Give each track a known-good starting point the run can build from. For a track that runs on a weekly standup, point the run at the standup's baseline document and have it reconstruct forward from there. Without an anchor, the model guesses, and the guesses are where the partial-information problem comes from. Find the anchor for each track before you trust the run on it.

**It over-drafts, and that is fine.** It proposes more follow-ups than you need. You delete the extras. An unwanted draft costs one click; a missed follow-up costs a dropped ball. Take that trade and stop trying to tune it to zero.

**Treat the first week as training.** The system gets good as its memory and context fill in. The early friction is not a flaw in the design; it is the cost of a system that learns your world. Push through it and it smooths out.
