---
name: grill-me
description: One-question-at-a-time interview for stress-testing a plan, running discovery on a client or idea, or pulling something out of your head that isn't written down anywhere. Every answer gets written to disk immediately, so a long interview never loses ground to a context reset or a dropped session. Trigger on "/grill-me", "grill me on this", "stress test this idea", "interview me about X", "help me think through X out loud".
---

## What this skill does

A standing interview skill, not a one-time onboarding step (that's `/setup`). Use it any time you have something half-formed in your head — a new offer, a client situation, a pricing call, a build decision — and need it pulled out through questions rather than a blank page.

Two things make this different from just asking questions in chat:

1. **Every answer is written to disk the moment it's given**, before the next question is asked. A 20-question interview interrupted at question 12 has 12 real answers saved, not zero.
2. **Every question comes with a best guess attached.** Don't ask an open question and wait — offer a specific guess based on what's already known (CLAUDE.md, memory, this conversation, the topic itself), and let the user confirm or correct it. Confirming is faster than writing from scratch, and a wrong guess is corrected exactly, which is often more information than a right one.

## When NOT to run this

- First day setup of this folder — that's `/setup`, not this.
- A quick factual question with an obvious single answer — just ask it directly, don't wrap it in this skill.

## Execution

### Step 1: Name the topic and open the file

Ask what we're grilling on if it isn't already obvious from context (a plan to stress-test, a client to run discovery on, an idea to flesh out). Create `brainstorms/<slug>-<YYYY-MM-DD>.md` immediately, before the first question, with a one-line header naming the topic and today's date.

### Step 2: One question at a time, each with a guess

For each question:

1. Ask it plainly, one at a time, never a batch.
2. Attach a best-guess answer in the same message — pull from CLAUDE.md, memory, `decisions/log.md`, or the conversation so far. If there's truly nothing to guess from, say so instead of inventing one.
3. Wait for confirm or correct.
4. The moment an answer lands (confirmed or corrected), append it to the brainstorm file before asking the next question. Format: the question, the guess that was offered, and the actual answer.

No fixed question count. Keep going while there's real ground left to cover; stop when the topic is actually exhausted, not at an arbitrary number. If it's dragging past ~15 questions with no end in sight, stop and ask the user if they want to keep going or wrap up with what's there.

### Step 3: Close it out

Summarize what was captured in a few lines. Ask if anything here should become a `decisions/log.md` entry, a memory, or feed straight into whatever the interview was actually for (a proposal, a build, a pricing call). Don't auto-file it — The user decides where it lands.

## Why this exists

Half of what you know about a deal, a client, or a decision never makes it into a file — it's in your head, and pulling it out by asking "so what's the plan?" produces a paragraph, not the structured detail that's actually useful later. Guessing first and asking you to correct is faster than a blank prompt, and checkpointing every answer means an interrupted session isn't a lost one.
