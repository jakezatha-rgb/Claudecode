---
name: team-memory
description: Load and update a team member's personal memory (projects, status, where they left off) stored as Google Docs and Sheets in their folder on the shared Drive. Use when the user says their name to start a session, asks "where did I leave off", or wants their project memory saved or updated.
---

# Team Memory

Claude has no memory between sessions. Each person's memory is a folder on Google Drive. This skill
loads it at the start of a session and keeps it current.

Operating rules (privacy, change reporting, failure handling) are in `CLAUDE.md`. Follow them.
Before the first Google file create or edit in a session, also read the `anthropic-skills:google-workspace` skill.

## Procedure: load

Input: the user's name.

1. Search Drive for the folder `Team Memory/<Name>` (use `search_files`, then confirm the parent is `Team Memory`).
   - Not found: say so, offer to create it (see **create**). Stop.
   - Several matches: ask which one.
2. List the folder, then read `Projects`, `Notes`, and `Profile` (`read_file_content`).
3. Give a recap of at most ~10 lines:
   - Active projects with their status.
   - For each, the **Where I left off** line and any blockers.
   - Anything stale (Last touched more than 14 days ago) or marked blocked.
4. End with: "Want to continue with <most recently touched project>, or something else?"

Do not dump the files back. Summarize.

## Procedure: update

Run at checkpoints and before the session ends.

1. Work out what changed: new or finished project, status change, new next step, decisions, blockers, links.
2. `Projects` sheet: update that project's row (Status, Next step, Last touched = today's date). Add a row for a new project.
3. `Notes` doc: append a dated entry under that project (see template) and replace its **Where I left off** line.
4. Report the changes in one or two lines. For anything that removes or overwrites existing content, ask first.
5. If a write fails, show the intended text so the user can paste it.

## Procedure: create

For a new person, with the user's confirmation:

1. Create folder `Team Memory/<Name>`.
2. Create the three files from the templates below.
3. Ask the user for their current projects and fill in the first rows. One question at a time is fine.

## Templates

### Projects (Google Sheet)

Header row, one project per row:

| Project | Status | Goal | Next step | Blockers | Links | Last touched |
|---|---|---|---|---|---|---|

Status is one of: `active`, `blocked`, `paused`, `done`. Dates are YYYY-MM-DD.

### Notes (Google Doc)

```
# <Name>: Notes

## Where I left off
- <Project A>: <the exact next step, specific enough to resume cold>
- <Project B>: ...

## Log
### 2026-01-01: <Project A>
- Did: ...
- Decided: ... (why)
- Next: ...
```

Newest log entries go at the top of the Log section.

### Profile (Google Doc, optional)

```
# <Name>: Profile
Role / focus:
How I like to work:
Recurring context (tools, clients, constraints):
```

## Quality bar

- "Where I left off" must be actionable cold: a stranger could resume from it. "Working on pricing" is bad;
  "Draft v2 of the pricing table is in the linked doc; next, compare tier 2 against the competitor sheet" is good.
- Keep entries short. Link to the real artifact (doc, repo, card) instead of copying content.
- No secrets, no gossip, no other people's data.
