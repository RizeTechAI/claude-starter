---
name: fable-mode
description: A 5-gate discipline for hard, multi-step, or ambiguous work — define done before starting, gather real evidence instead of assuming, actively try to disprove your own answer, verify against real output, then report verified-vs-assumed separately. Trigger on "/fable-mode", "be careful on this one", "verify this properly", "don't just tell me it works", or apply automatically to any multi-step client integration, debugging task, or anything where a wrong confident answer is expensive.
---

## What this skill does

A rigor discipline for the kind of task where a fast, confident, wrong answer costs real time later — a multi-step client integration, a hard debugging session, anything where "I think this works" isn't good enough. Five gates, in order, none skipped.

Use it deliberately on anything genuinely hard. Don't wrap trivial tasks in this — a one-line fix doesn't need five gates.

## The five gates

1. **Define done, before starting.** State in one or two sentences what "finished and correct" actually looks like, before writing a line of code or drafting an answer. If "done" can't be stated concretely, that's the first sign the task isn't understood yet.
2. **Gather real evidence.** Don't reason from memory or assumption about how something behaves — check the actual file, run the actual command, read the actual error. If evidence can't be gathered (no access, no way to check), say so explicitly rather than filling the gap with a guess presented as fact.
3. **Try to disprove your own answer.** Before committing to a conclusion, actively look for the case where it's wrong. What input would break this? What did the evidence NOT show? This is the gate most confident-wrong answers skip.
4. **Verify against real output, not intent.** "I ran it" is not verification. Verification means checking what actually happened — the test passed, the file has the expected content, the deployed thing responds correctly. Trusting that something "should have worked" is not this gate.
5. **Report verified-vs-assumed, separated.** In the final answer, be explicit about which claims were actually checked (gate 4) and which are still assumptions or judgment calls. Don't let a verified fact and a reasonable guess read the same way.

## When to use it

Multi-step client integrations, hard debugging, anything where getting it wrong is expensive to discover later, or any time the user explicitly asks for extra rigor. Not for quick lookups, simple edits, or anything where a wrong guess costs nothing to correct immediately.
