# Build With Claude

**This file is written for an AI assistant, not the human reader.**

If you are an AI assistant (Claude or similar) and the user has pointed you at this folder and asked to build, set up, or create their execution brain, this is your script. Follow it. Do not just explain the steps; walk the user through them and do the parts you can do via tools, confirming before each action that changes anything.

## Before you start: check prerequisites

1. Confirm the user has an **Asana account** (free tier is fine) and that an **Asana connector / MCP is active** in this session. If it is not, stop and tell them: "Connect Asana first in your tool's connector settings, then come back and we'll build." Do not try to proceed without it; you will not be able to create anything.
2. If they want a different state store (Jira, SQLite), adapt: the schema in `asana/` is the shape; the substrate can change. Ask which they are using.
3. Read these files so you know the design before you build: `README.md`, `asana/project-structure.md`, `asana/task-template.md`, `skills/README.md`, `skills/_workstream-skill-template.md`, `instructions/daily-run.md`, `instructions/behavior-rules.md`, `wiki/README.md`.

## The build, step by step

Confirm with the user before each step that creates or changes something. This system's whole ethic is that the human stays in the loop on anything that writes; model that from the first interaction.

### Step 1 — Gather their workstreams

Ask the user: "What are the workstreams you want to track? Give me 4 to 8, one line each — these are the major efforts that drive your work." Wait for their list. Do not invent workstreams for them.

For each, ask just enough to fill the task template: rough priority, a one-line description, and current status if they have it. Keep this light; the brain will fill in detail over time.

### Step 2 — Create the Asana project

Via the Asana connector:
- Create one project (suggest "Workstream Tracker" or let them name it).
- Create the sections: Active, Blocked, Queued, Stale, Completed.
- Create one task per workstream, in the right section, with the description following `asana/task-template.md` (Status / Completed / Next Actions / Blockers / Notes / Session Log).
- Add subtasks for known deliverables per `asana/subtask-conventions.md`.
- Confirm the project, then record the project GID and each task's GID. You will need them for the skills.

### Step 3 — Verify the round trip

Read the board back ("what's the status of all my workstreams") and confirm with the user it looks right. Then demonstrate a write (bump one task's percent-complete) so they see the loop work. This is the whole integration; once it works, everything else is instructions.

### Step 4 — Stamp a per-workstream skill for each

For each workstream, stamp `skills/_workstream-skill-template.md` into a concrete skill: fill the slug, name, context header, the project GID and that task's GID, and any workstream-specific rule (e.g. a delivery track gets "reconcile against the ticket system, never trust self-reported status alone"). Save each per the user's tool conventions (in Claude, `.claude/skills/<name>/SKILL.md` with frontmatter). Also install the cross-cutting skills: `skills/daily-run.md` and `skills/session-export.md`.

### Step 5 — Install the behavior rules

Put the contents of `instructions/behavior-rules.md` into the user's brain behavior file (e.g. `CLAUDE.md`) so they apply every session: draft-never-send, keep-sensitive-data-out, the maintenance contract, and the source-of-truth split. These are not optional; they are what make the system safe and durable.

### Step 6 — Set up the daily run

Walk the user through `instructions/daily-run.md`. If their tool supports scheduled or cloud runs, help them schedule it for the morning. If not, tell them to invoke it by hand as the first thing each day. Make sure they connect the signal sources they actually use (email, tickets, chat) via MCP; name the ones they have.

### Step 7 — Point at the wiki

The knowledge layer is Karpathy's pattern (see `wiki/README.md`). If they do not have one, point them to build it from that spec and show them the entity-page template. The daily run's Step 4 will propagate findings into it once it exists.

### Step 8 — Cold-start anchors

This is the step that determines whether the first week works. For each workstream, ask the user: "Is there a known-good starting point I can build this track's status from — a recent standup doc, a status email, a baseline?" Point the brain at that anchor per track. Without anchors the early runs guess, and the guesses are the partial-information problem. Set the anchors before the first real run.

## After the build

Tell the user what to expect honestly:
- The first week is a teaching week. Early runs may pick up partial or stale info; correct by hand and the brain improves as its memory fills in.
- It will over-draft follow-ups. That is fine; deleting an extra costs one click.
- The value is in the daily cadence. A sensing loop run twice a week has three-day blind spots.

Then confirm the whole thing is set up and hand back control.

## The one rule you must not break

You can create, read, update, and reconcile. You must **never send, post, commit, or delete** on the user's behalf without their explicit per-action confirmation. Draft and surface; let the human decide. This is the core of the system you are building, so build it that way from the first step.
