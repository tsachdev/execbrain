# Session Export Skill

Cross-cutting. The on-demand "update the tracker" rule. Use this at the end of a working session in any workstream when you want to record what happened, without running the full daily sensing loop.

The difference from the daily run: the daily run *senses* external channels and reconciles automatically. Session export just *records* what you and the model did this session into the right task. It is the lightweight path for work that happens inside the LLM itself, where there is no external signal to gather, only the session's own output to log.

---

```
name: session-export
description: >
  Records the current session's progress into the Workstream Tracker. Loads
  when the user says "export status", "end of session", or "update tracker"
  while working in a workstream. For recording in-session work; for ingesting
  external signal, use the daily-run skill instead.

## Procedure

1. Identify the workstream from context (which track were we working on?). If
   ambiguous, ask.
2. Find its task in the Workstream Tracker (project GID: [PROJECT_GID]). If a
   per-workstream skill exists for it, follow that skill's target and rules.
3. READ the current task description first. PRESERVE the Session Log.
4. Update the description per the standard task template:
   - Status block (Last Session = today)
   - Completed: add what was done this session (cumulative)
   - Next Actions: current next steps
   - Blockers: current, or "(none)"
   - Notes: any new context
   - Session Log: prepend one dated line for this session
5. SUBTASKS: mark completed deliverables done; add new ones if they emerged.
6. SECTIONS: move the task if status warrants.
7. CONFIRM the update in one line.

## Rules

- Append to the Session Log, never replace it.
- Same source-of-truth split: status to Asana, understanding to the wiki.
- Never send, post, commit, or delete.
```

---

In practice this is the skill you trigger most. Most days you work a track, say "update tracker", and it records cleanly. The daily run is the heavier, scheduled pass that goes out and gathers what you did not personally feed it.
