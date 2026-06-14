# Skills

The procedure layer. A skill is a markdown file with a trigger and a set of steps the LLM follows. Skills are how the brain knows *how to do a kind of work*, not just what it knows or what the status is.

## Two kinds of skill

**Per-workstream skills.** One per workstream. Each knows how to read and update *its own* track: it carries that workstream's Asana task GID and its specific reconciliation rules. When you say "update the delivery tracker" or work inside that project, the matching skill loads and operates on the right task. You stamp one of these from the template for every workstream you track.

**Cross-cutting skills.** Shared procedures not tied to a single workstream. The daily run is one. The session-export rule is another. An ingest/convert routine is another. These operate across the whole portfolio.

The distinction matters because it is what makes the system scale. Add a workstream, stamp a per-workstream skill, and the brain knows how to run that track without you re-explaining it. The cross-cutting skills stay constant.

## The per-workstream pattern

Every per-workstream skill has the same shape:

1. **Trigger** — the phrases that load it ("update the [workstream] tracker", "end of session for [workstream]").
2. **Target** — the Asana project GID and the specific task GID it owns.
3. **Context header** — two or three lines on what the workstream is, so the skill fires on the actual work and not just the literal trigger phrase.
4. **The update procedure** — read the current task first, preserve the session log, update the fields, manage subtasks, move sections, confirm.
5. **Any workstream-specific rules** — e.g. a compliance track might carry an evidence-handling rule; a delivery track might carry a "always reconcile against the ticket system, not just self-reported status" rule.

Use `_workstream-skill-template.md` as the stamp. See `example-workstream-skill.md` for a filled-in one.

## Files in this folder

| File | Type | Purpose |
|------|------|---------|
| `_workstream-skill-template.md` | template | stamp one per workstream |
| `example-workstream-skill.md` | per-workstream | a filled-in Customer Implementation Delivery skill |
| `daily-run.md` | cross-cutting | the six-step morning engine |
| `session-export.md` | cross-cutting | the on-demand "update tracker" rule |

## A note on where skills live

In a Claude environment these go in `.claude/skills/<name>/SKILL.md`, each with frontmatter naming the skill so it can be discovered and loaded. In other tools the mechanism differs but the content is the same: a named, triggerable instruction the model loads for a class of task. This repo gives you the content; adapt the packaging to your tool.

If you already run separate projects in your LLM tool with custom instructions, you have per-workstream skills written already. Lift the instructions out and drop them in here as skills. That is exactly how this library was seeded.
