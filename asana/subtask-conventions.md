# Subtask Conventions

Subtasks are the deliverables under a workstream. They give you item-level progress tracking without a separate tool, and they are available on the Asana free tier.

## What becomes a subtask

A subtask is a discrete, checkable deliverable or work area within the workstream. Not every line in the Completed list needs to be a subtask; reserve subtasks for the things you want to track to done independently.

Examples for a **Customer Implementation Delivery** workstream:
- Requirements sign-off
- Integration build
- Data migration
- UAT
- Go-live readiness
- Hypercare

Examples for an **ISO 27001 Certification** workstream:
- Scope definition
- Gap assessment
- Statement of Applicability
- Internal audit
- Stage 1 audit
- Stage 2 audit

## How the run uses them

During reconciliation, the daily run marks subtasks complete as their deliverables land, and adds new subtasks when new deliverables emerge from the signal. A subtask completion is a clean, unambiguous progress signal, more reliable than a percent-complete estimate.

## Granularity

Keep it to the deliverables you would actually report on. Roughly 5 to 10 subtasks per workstream is the useful range. More than that and you are managing the tracker instead of the work; fewer and the subtasks are not telling you anything the percent-complete field does not.

## Optional detail in subtask notes

A subtask can carry its own short note if a deliverable has meaningful internal state (e.g. "UAT: 3 of 5 test cycles passed, blocked on environment access"). Keep these to a line or two. Deep narrative belongs in the parent task's Notes or in the wiki, not scattered across subtask fields.
