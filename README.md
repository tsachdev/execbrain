# Execution Layer Brain

An LLM-maintained system for **execution state**, the half of a working life that a knowledge wiki cannot hold.

This is not a second brain. It is the layer that bolts onto one.

## What this is

In April 2026, Andrej Karpathy published a spec for an LLM-maintained personal wiki: have the model build and maintain a navigable knowledge base instead of re-reading raw documents at query time. The idea spread fast, and it is good. It answers the question *"what do I know about X."*

But most of a working day is a different question: *what is the status of this, what moved since yesterday, what is now stale, who owes me a reply, what is the one thing I should touch today.* A prose wiki is the wrong substrate for that. Status is structured. It wants a database.

This repo is the **execution layer**: a structured state store, a set of procedures the model follows, and a daily run that senses your real inbound, reconciles it into state, propagates findings into your knowledge wiki, and drafts the actions you owe. It senses everything. It acts on nothing irreversible without you.

## Credit where it is due

- **The knowledge wiki** is Andrej Karpathy's pattern. This repo does not reproduce it; it points to it. See `wiki/README.md`.
- **The trigger** was a conversation with Greg Buzek, founder of IHL Group, who is doing this work inside real industry. The researchers describe the mechanism; the practitioners prove it. Greg is the second kind.
- **The execution layer** — the Asana state schema, the skill format, the daily run, the human-gated action boundary — is the contribution here.

## The architecture

Three layers, three substrates. Do not collapse them.

| Layer | Substrate | Answers | Lives in |
|-------|-----------|---------|----------|
| **State** | A database | "What is the status?" | Asana (this repo's schema) |
| **Knowledge** | A markdown wiki | "What do I know about X?" | Karpathy-style wiki |
| **Procedure** | Skills | "How do I do this kind of work?" | `skills/` |

State is structured because status is structured: it sorts, it rolls up, it answers staleness. Knowledge is prose because understanding is prose: it compounds in dated, narrative findings. Procedure is the part most people skip: each kind of work gets a written workflow the model loads on demand, including one skill per workstream that knows how to read and update its own track.

The discipline is in the routing. A status fact ("the review is done, ships Friday") goes to the state database. An insight ("this account's real blocker is a customer input nobody has chased, not the thing everyone is watching") goes to the wiki. The same email can produce both. Keep the line clean or both substrates rot.

## The boundary that makes it safe

The daily run is autonomous. It reads your whole inbox and reconciles your entire portfolio without you. But it **cannot send, post, commit, or delete.** Those are gated on a human, every time. It drafts the follow-up and leaves it in your outbox.

This is deliberate, and it is the opposite of where most of the field is heading. Autonomy everywhere the action is reversible. A human gate at every door that only opens one way. You can let this run unattended every morning precisely because it cannot do anything you cannot undo.

## Why Asana (and what else works)

This repo uses **Asana** for the state layer because it has a clean API, a free tier with unlimited tasks and subtasks, a connector most LLM tools support, and a mobile app. None of that is load-bearing. The state layer is defined by its *shape*, not the tool:

- **Asana** — recommended; what these templates target.
- **Jira** — if your work already lives there.
- **SQLite** — if you want zero dependencies and to own the whole stack.

Any store that gives you structured, sortable, queryable status with an append-only log will do.

## Repo contents

```
execution-layer-brain/
├── README.md                      you are here
├── asana/
│   ├── project-structure.md       sections, custom fields, lifecycle
│   ├── task-template.md           the per-workstream status format
│   └── subtask-conventions.md     deliverables as checkable subtasks
├── skills/
│   ├── README.md                  the two kinds of skill, and the pattern
│   ├── _workstream-skill-template.md   stamp one per workstream
│   ├── example-workstream-skill.md     a filled-in example
│   ├── daily-run.md               the six-step engine
│   └── session-export.md          the "update tracker" rule
├── instructions/
│   ├── daily-run.md               the run, narrated step by step
│   └── behavior-rules.md          draft-never-send, sensitive-data, maintenance
├── wiki/
│   └── README.md                  pointer to Karpathy's spec + entity template
└── examples/
    └── northwind-apparel.md       one CTO workstream, end to end
```

## Quick start

Do not build all of it at once. Each layer is useful alone.

1. **Stand up the state database.** Create the project, sections, and one task per workstream from `asana/`. Live with just a queryable status board for a few days. It is already an upgrade.
2. **Connect your LLM to it.** Confirm the read path ("what's the status of all my workstreams") and the write path ("bump this to 60%"). That round trip is the whole integration.
3. **Add the daily run.** Drop in `instructions/daily-run.md` and `instructions/behavior-rules.md`. Schedule it.
4. **Add per-workstream skills.** Stamp `skills/_workstream-skill-template.md` once per track.
5. **Add the wiki.** Stand up the Karpathy layer and let the run propagate findings into it.

Read `examples/northwind-apparel.md` to see all of it working on a single real-shaped CTO workstream.

## A warning

This is not a weekend project you set up and admire. It is a system you run daily, and it compounds only if you run it. The honest friction — partial pickups early, the need for a cold-start anchor per track, the over-drafting you learn to live with, the non-negotiable maintenance contract — is documented in `instructions/behavior-rules.md` and in the companion essay. Budget for a teaching week.

---

*Companion essay: "The Execution Layer Brain" on the CTO Layer.*

*Built and maintained by Tushar Sachdev ([@tsachdev](https://github.com/tsachdev)). MIT licensed. Credit to Andrej Karpathy for the wiki architecture and Greg Buzek for the trigger.*
