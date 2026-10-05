---
name: session-handoff
description: Produce a structured end-of-session summary before context gets cleared or compacted, so the next session (or a fresh Claude instance) can resume cold with no lost ground. Trigger on "/session-handoff", "write a handoff", "wrap up this session", "before we clear context", or proactively suggest it when a long session is about to hit its limit.
---

## What this skill does

A chat-only summary, never written to a file by default, produced right before a session ends, gets compacted, or clears context. Long sessions (multi-hour research projects, multi-step builds) lose real work when a fresh session has to reconstruct "what were we even doing" from scratch. This skill exists to make that reconstruction instant instead of guessed.

## When to run it

- The user asks directly ("/session-handoff", "wrap up", "summarize before we clear").
- Proactively, when a session has been long and complex (many tool calls, multiple sub-tasks, background agents) and looks like it's wrapping up or about to compact.
- Before starting a `/compact` or ending a session that did meaningful multi-step work.

Don't run it for short, single-task sessions — a two-message exchange doesn't need a handoff.

## What to produce

Chat output, not a saved file (unless the user explicitly asks to save it). Cover, in order, only the sections that actually apply — skip any that are empty rather than padding them out:

1. **Where this session started from** — the one-sentence starting ask or problem, so the next session has the "why."
2. **What's locked / shipped** — decisions made and their actual absolute file paths (not "the config file," the real path). If something was committed or pushed, say so explicitly.
3. **Key files for next session** — the small set of files someone would need open to pick this back up, not every file touched.
4. **Running state** — anything that would otherwise be lost: background shell/agent IDs still running, dev servers left up, open git worktrees, scheduled wakeups pending. This is the category people forget and it's the most expensive to lose.
5. **Verification done** — what was actually run/tested to confirm the work, not what was claimed.
6. **Open questions / deferred work** — anything left unresolved, with enough context that a cold read understands why it's still open.

## Rules

- Never write this to disk automatically — it's for the current chat only, unless the user says to save it.
- No retrospective commentary ("this was a great session," "we learned a lot") — this is a resume point, not a narrative.
- If a section has nothing real to report, drop it rather than writing a filler line.
- Absolute paths, not vague references — "the file we changed" is useless to a fresh session with no memory of this conversation.
