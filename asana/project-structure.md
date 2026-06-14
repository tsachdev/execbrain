# Asana Project Structure

The state layer. One project holds your entire portfolio. This file describes the structure to create.

## The project

Create one Asana project. Name it for your portfolio (e.g. "Workstream Tracker"). On the free tier this supports unlimited tasks and subtasks, which is all you need.

## Sections (the lifecycle)

Sections are the workflow states. A task moves between them as its status changes.

| Section | Meaning |
|---------|---------|
| **Active** | In progress, updated within the staleness window (default 7 days) |
| **Blocked** | Waiting on an external dependency (a person, a customer, another team, another workstream) |
| **Queued** | Defined but not started; may have a dependency |
| **Stale** | No update in 7+ days; needs attention or a deliberate decision to park |
| **Completed** | Done; archived here, not deleted |

The daily run moves tasks between sections when the status warrants it. A track that goes quiet for a week moves to Stale. A blocked track that clears moves back to Active.

## Custom fields (optional, premium)

If you are on a paid Asana plan, two dropdown fields make the board sortable in Asana's own UI:

- **Priority** — High / Medium / Low
- **Status** — On track / At risk / Off track

On the free tier these are not settable via the API. That is fine. The task description carries the same data (see `task-template.md`), and the LLM reads and writes the description regardless of plan. The custom fields are a convenience for the Asana UI, not a dependency.

## One task per workstream

Each workstream is one task. The task name is the workstream name. A realistic CTO/CPO portfolio might look like:

- AI Product Engineering Transformation
- Major Module Delivery
- Customer Implementation Delivery
- ISO 27001 Certification
- Release Delivery
- ERP / SAP Upgrade

Deliverables under a workstream become **subtasks** (see `subtask-conventions.md`).

## The append-only session log

Every task description ends with a Session Log: a dated, newest-first list of what happened each time the task was touched. It is **append-only**. The run adds a line and never deletes a prior one. This log is how the system remembers, and it is the single most important convention in the schema. Enforce it in the behavior rules.

## Record the GIDs

After you create the project, sections, and tasks, record their Asana GIDs. The daily run and the per-workstream skills reference them. Keep a small map:

```
PROJECT_GID:        <your project gid>
SECTION_ACTIVE:     <gid>
SECTION_BLOCKED:    <gid>
SECTION_QUEUED:     <gid>
SECTION_STALE:      <gid>
SECTION_COMPLETED:  <gid>

TASK_<WORKSTREAM>:  <gid>   # one line per workstream
```

You can get these by asking your LLM (with the Asana connector enabled) to list the project's sections and tasks with their GIDs, once the structure exists.
