# Personal AI Memory for Every Teammate

*A proposal: give Claude a memory, one folder per person, so every session picks up where the last one ended.*

## The problem

Claude is capable but starts every conversation cold. Every session, each of us re-explains what we are
working on, what we decided, and what comes next. That costs minutes each time, and the context that matters
(why we chose X, what was blocked) quietly gets lost.

## The idea

Give each person a small, private **memory folder** on our shared Google Drive. Claude reads it at the start of a session
and updates it as we work. The memory lives in ordinary Google Docs and Sheets that we can read and edit ourselves.

- Say your name. Claude opens your folder and recaps your projects and exactly where you left off.
- Work as normal. Claude records decisions, status changes, and the next step.
- Close the session. Your folder is current for next time, from any device.

## How it works

| Piece | What it is |
|---|---|
| **Memory store** | `Team Memory/<Name>/` on the shared Drive |
| **Projects sheet** | One row per project: status, goal, next step, blockers, links, last touched |
| **Notes doc** | "Where I left off" per project plus a short dated log of decisions |
| **Profile doc** (optional) | Role, preferences, recurring context |
| **Instructions** | A `CLAUDE.md` plus a `team-memory` skill that define how Claude loads and updates the folder |

Claude doesn't remember anything on its own. The files are the memory, so it is transparent and portable,
and you can fix it with a keyboard.

## Benefits

- **No more re-briefing.** Resume a project in seconds, even after weeks away.
- **Decisions are captured**, with the reason, while they are fresh.
- **Nothing hidden.** It's plain Docs and Sheets. You can read, correct, or delete any of it.
- **Cheap to start.** Folders, two templates, and one instruction file. No new software to buy.
- **Personal by design.** It supports *you*. It is not a reporting tool.

## Principles and guardrails

1. **Your memory belongs to you.** Each session only opens the active person's folder. It never reads or quotes someone else's.
2. **Not a monitoring tool.** There are no team dashboards, no cross-person summaries, and no activity scoring.
3. **Visible changes.** After each save Claude says what it changed, and it asks before deleting anything.
4. **No secrets.** Passwords, keys, and sensitive personal data stay out of the files.
5. **Fails safe.** If Drive isn't reachable, Claude says so and offers a summary to paste in later. It never pretends it remembers.

## What we need to decide

- **Access and privacy.** Ideal setup: each person has their own Claude seat and the Drive folder is shared only with them.
  A single shared login would work technically but cannot keep folders private, and consumer plans may not allow
  shared logins. We should check Anthropic's current terms and plan options (e.g. a team plan) before rollout.
- **Plan features.** Confirm that the chosen plan includes the Google Drive connector.
- **Update discipline.** Claude saves only while a session is running, so the instructions tell it to update at
  checkpoints and before closing.
- **Usage limits.** Heavy shared use on one account could hit limits.

## Rollout plan

1. **Pilot (1 week):** Jake runs it on his own folder. Tune the templates and instructions.
2. **Small group (2 weeks):** 2 to 3 teammates, each with their own folder. Collect what is useful and what is noise.
3. **Team:** Roll out with the settled templates and access setup.

**Success looks like:** people start a session and are working within a minute, and "where was I?" stops being a question.

## The ask

Approve a one-week pilot with a single folder and the files in this repo.
Cost: setup time and an existing Claude plan. Risk: low, since all memory is in files we own and can delete.
