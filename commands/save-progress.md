---
description: Update CLAUDE.md, TODO.md, PROGRESS.md, and DECISIONS.md with current session work so the next session can pick up seamlessly
---

Update the project's session-handoff files so the next Claude Code session can pick up where this one left off.

Do the following in order. Create any file that doesn't exist yet.

1. **TODO.md**
   - Mark any completed items as done (`- [x]`)
   - Add any new tasks surfaced this session
   - Maintain a `## Blocked` section for items waiting on external input — note what each is blocked on
   - Keep the file scannable: group by area if it's getting long

2. **PROGRESS.md** (append-only session log)
   - Append a new entry headed `## Session YYYY-MM-DD`
   - Under it, in bullets:
     - **Shipped:** what was actually finished this session (be specific — file names, behaviors, not vague verbs)
     - **In progress:** anything partially done and the state it was left in
     - **Blocked:** what's waiting and on whom/what
     - **Next session should pick up:** the single most important thing to do first
   - Do NOT rewrite old entries — append only

3. **DECISIONS.md** (ADR-style architectural decision log)
   - If any architectural, dependency, library, API-design, data-model, or convention decisions were made this session, append a new entry:
     - `## YYYY-MM-DD — <short title>`
     - **Context:** what problem or question prompted the decision
     - **Decision:** what was chosen
     - **Alternatives considered:** what else was on the table and why it was rejected
     - **Consequences:** trade-offs accepted, follow-ups required, things to watch for
   - Skip this step entirely if no real decisions were made this session — do not pad it with trivial choices

4. **CLAUDE.md** (project root)
   - Update ONLY if stable project context changed: new dependencies, new build/test/deploy commands, new directory conventions, new code-style rules, changed architecture
   - Do NOT log session-specific work here — that's what PROGRESS.md is for
   - Keep it short and high-signal; if a section is getting noisy, prune it

5. **README.md**
   - Update only if user-facing behavior, install steps, configuration, or public API changed
   - Skip if the changes were internal

6. **Handoff summary**
   - Print a concise summary to the chat with three lines:
     - ✅ Shipped: ...
     - 🟡 Next: ...
     - 🔴 Blocked: ... (or "nothing blocked")

Be honest in the summary — if little was accomplished, say so. The point of these files is accurate handoff, not optimistic reporting.
