---
name: remind-me
description: Handles personal reminders between the user and Claude. Use whenever the user says "remind me", "remind me to...", "remind me when I get home", "don't let me forget", "bring this up next time", or similar, even without a date. ALSO use at the start of every new conversation, before other work, to check reminders.md for open reminders and mention them. Reminders are private and stay in the chat and in reminders.md in the repo; never put them in shared tools like Trello, Slack or email.
---

# remind-me

Claude does not remember earlier conversations. A reminder only survives into the next conversation if it is written down somewhere the next conversation can read. The user wants reminders to stay private, between them and Claude, so the only places used are the chat itself and a small `reminders.md` file in the repo. Do not use Trello, Calendar, Gmail or any shared tool: the user's Trello board is shared with teammates.

Only save things the user explicitly asks to be reminded of.

## When the user asks for a reminder

1. Answer whatever else they wrote, as normal.
2. Add the reminder to `reminders.md` at the repo root, as a line under "Open":
   `- [ ] <reminder in the user's words> (set YYYY-MM-DD; when: <trigger, e.g. "when I get home" or "next conversation">)`
   Include enough context that a fresh conversation can act on it (which file, which step).
3. End the reply with the reminder as the last lines of the message, in this form:

   **Reminder:** <the reminder> (<trigger>)

   Putting it last keeps it visible and makes clear that it was saved.
4. Commit and push `reminders.md` only if the user has asked for commits in this session or a hook asks for it. If it cannot be saved (no repo, push fails), say so plainly; a reminder that was not written down will not come up next time.

## Start of a new conversation

1. Read `reminders.md` if it exists. Look only at the "Open" section.
2. If there are open reminders, mention them at the very start of the first reply, one line each, then continue with what the user asked. If a reminder's trigger is a condition ("when I get home"), opening a new conversation is the cue: mention it and ask if it is done.
3. When the user says one is done, move it to a "Done" section. If they want it again later, update the line rather than adding a duplicate.
4. If there are no open reminders, say nothing about reminders.

## Keep it private

Keep reminder text short and non-sensitive. No passwords, tokens or other people's private details.
