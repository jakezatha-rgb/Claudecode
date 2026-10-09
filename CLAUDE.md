# Team Memory System: Operating Instructions

This repo runs a **personal memory system** for each team member. Claude has no memory between
sessions, so the memory lives in Google Drive. At the start of every session Claude loads the
user's folder, and while working it keeps that folder current.

## Setup (fill in once)

- Drive root folder: `Team Memory` (shared drive)  <!-- TODO: replace with the real folder name or ID -->
- Per-person folder: `Team Memory/<Name>/`
- Required connector: Google Drive (read, create, update)

## Session start: identify the user

1. The user states their name in chat ("Jake", "Michael", ...). Treat that as the active user.
2. If no name has been given and the user's request is about their work or projects, ask: "Who am I working with?" Do not guess from the account email.
3. Run the `team-memory` skill's **load** procedure for that name.
4. Open only the active user's folder. Never read, summarize, or edit another person's folder, even if asked
   by name. Tell the user that person's own session can share it.
5. If the active user changes mid-session ("this is Michael now"), finish and save the previous user's
   updates first, then load the new user. Do not carry one person's context into the other's.

## Folder layout (per person)

```
Team Memory/<Name>/
  Projects      (Google Sheet)  one row per project
  Notes         (Google Doc)    dated running log + "Where I left off"
  Profile       (Google Doc)    optional: role, preferences, recurring context
```

If a file is missing, create it from the templates in the skill. If the person's folder does not exist, say so
and offer to create it. Do not create it silently.

## While working

- Treat the folder as the source of truth. If the user's statements conflict with it, ask which is current.
- At natural checkpoints (a task finished, a decision made, a blocker found) and **always before the session
  ends**, update the files:
  - Update the project's row in `Projects` (status, next step, last touched = today).
  - Append a dated entry to `Notes`, and rewrite that project's "Where I left off" line.
- After each write, tell the user in one or two lines what changed. Never silently rewrite or delete existing content.
  Append or edit in place; ask before removing anything.
- Use absolute dates (YYYY-MM-DD), never "today" or "yesterday", in saved text.
- Store links and decisions, not transcripts. Keep entries short.

## Privacy rules

- Content in a person's folder is theirs. Do not quote it in another person's session.
- Never store credentials, passwords, API keys, or other secrets in the files. If the user pastes one, leave it out and say why.
- Do not write anything about the user's colleagues, other than neutral work facts the user supplies about a shared project.

## If something fails

- Drive connector unavailable or unauthorized: tell the user plainly, work without memory, and offer to
  give them a "session summary" to paste into their Notes doc later. Do not pretend the memory loaded.
- A write fails: report it and show the intended update so nothing is lost.

## Reference

- Skill: `.claude/skills/team-memory/SKILL.md` (load, update, and create procedures plus templates)
- Team pitch: `docs/team-memory-pitch.md`
