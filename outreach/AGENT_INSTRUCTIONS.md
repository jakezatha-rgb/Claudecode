# Task for a drafting agent (DRAFTS ONLY — NEVER SEND)

You are drafting sponsorship outreach emails for FRC team Mariners 8223. Your batch file is `/home/user/Claudecode/outreach/batch_N.json` (N given in your message). Each entry: seq, company, email, lang ("he" or "en"), day (1-10).

Template (Hebrew master): `/home/user/Claudecode/outreach/template_he.md` (first line is the SUBJECT, rest is the body). Read it fully.

For each entry:
1. If lang == "he": use the Hebrew template. Address it to the company: replace "שלום רב," with "שלום רב, צוות <company>," (company name in Latin script).
   If lang == "en": translate the whole template into natural, professional English (subject: "Sponsorship & partnership request – Mariners 8223 FRC Robotics Team"; greeting "Dear <company> team,"). Keep all facts, phone numbers, emails and both links exactly. Keep it warm and concise; don't invent facts. Hebrew team name can stay in Latin: "Mariners 8223, the robotics team of Ironi H High School, Tel Aviv".
   Do NOT otherwise change the facts. Do not add claims.
2. Load Gmail tools via ToolSearch (`select:mcp__Gmail__create_draft,mcp__Gmail__label_thread`). Call `create_draft` with `to` = the entry's email only, plain `body` (no markdown), `subject`. For Hebrew, ALSO pass `htmlBody` with `<div dir="rtl" style="text-align:right">…</div>` (use <br> for line breaks) so it renders right-to-left; for English plain body is enough.
3. Label the returned `threadId` with `label_thread` using the day's label ID: Day1=Label_3, Day2=Label_4, Day3=Label_5, Day4=Label_6, Day5=Label_7, Day6=Label_8, Day7=Label_9, Day8=Label_10, Day9=Label_11, Day10=Label_12. Use the entry's `day` field. If labelling fails, retry once, then report it.
4. NEVER call send_message or any send/forward tool. Drafts only. Create each draft exactly once (no duplicates; if you retry, first check list_drafts).

Final report (short): a table of seq | company | lang | day | draftId | labelled yes/no, plus any problems.
