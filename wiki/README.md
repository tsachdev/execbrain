# The Knowledge Wiki

This is the Karpathy layer. This repo does **not** reproduce it; it points to it and shows how the execution layer connects to it.

## Build the wiki from Karpathy's spec

Andrej Karpathy published a spec for an LLM-maintained personal wiki in April 2026: instead of re-reading raw documents at query time, the model builds and maintains a navigable knowledge base of markdown pages, and reads a compact index plus the few relevant pages on demand. It is not a product, it is a set of principles for structuring a knowledge base an LLM can actually navigate.

Build your knowledge layer from that spec, or from any of the good public adaptations of it. This repo assumes you have a wiki and focuses on the execution layer that feeds it.

The one principle worth restating because the whole system depends on it: **you own the schema, the model owns the content.** You decide what a page looks like and what earns a page. The model writes and maintains them. If a page is wrong, you do not hand-edit it into a fight with the model's next update; you feed it the correction and let it reconcile.

## How the execution layer connects

The daily run's Step 4 propagates findings into the wiki. After it reconciles state in Asana, it appends material findings to the relevant entity pages. State and knowledge stay in their own substrates, but the run keeps both current in one pass.

The split, restated:
- **Asana** holds status. "Where does this stand, what is next, what is blocked."
- **The wiki** holds understanding. "What do I know about this person, account, initiative, or concept, accumulated over time."

## Entity-page template

A minimal page the run can read and append to. Adapt freely.

```
tags: [reference, wiki-page, <folder>, <folder>-<slug>]
date: YYYY-MM-DD

# <Entity Name>

## Type
[person / account / initiative / concept]

## Relationship
[how this entity relates to you and your work]

## Summary
[a few sentences of current understanding, rewritten as it evolves]

## Key Findings
- [YYYY-MM-DD] finding, with the specific data point. Source: <where>. (c:100/80/70)
- [YYYY-MM-DD] earlier finding. Source: <where>. (c:80)

## Related Files
[links to source documents, deliverables, related pages]
```

## Conventions

- **Key Findings are append-only and newest-first.** Same discipline as the Asana session log. Never delete a prior finding.
- **Confidence-tag findings.** `c:100` for confirmed fact, `c:80` for reliable inference, `c:70` for soft signal. Later runs and your later self need to know how much to trust each line.
- **One entity per page.** Resist mega-pages. The model navigates better across many small pages than one large one, and small pages are what keep the index loadable.
- **Curate what gets a page.** Not everything deserves one. The human's job is picking what is worth thinking about; the model's job is everything after that.

## Folders

Organize by entity type. A working set for a CTO might be:

```
wiki/
├── people/         colleagues, customers, partners
├── accounts/       customers, prospects
├── initiatives/    programs and transformations
├── concepts/       frameworks, methods, recurring ideas
└── README.md
```
