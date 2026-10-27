# Project Brain

Claude reads this file first, every session. Keep it short and current.
Run `/setup` to fill it in.

## Who I am
(Your name, your role, what you do.)

## What I'm working on
(The ideas and projects this folder is for.)

## What matters right now
(Top 3 priorities, one line each.)

## How to work with me
- Be direct and concise.
- Ask before deleting anything. Move old stuff to `archives/` instead.
- When I make a decision, add it to `decisions/log.md`.
- When I'm doing the same task over and over, suggest turning it into a skill.

## Where things live
- `context/`: background on me, my work, my goals
- `projects/`: one folder per idea or build
- `brainstorms/`: rough thinking and interview notes
- `references/`: docs, notes, how tos, anything worth keeping
- `decisions/log.md`: what was decided and why
- `connections.md`: tools and accounts this folder can reach
- `archives/`: old stuff. Never delete, move here.

## Skills
- `/setup`: fill in this file by answering a few questions
- `/grill-me`: Claude interviews you one question at a time to pull an idea out of your head
- `/roast`: five critics tear apart an idea before you spend time on it
- `/storm`: research a topic from several expert angles
- `/fable-mode`: careful mode for hard, multi step work
- `/session-handoff`: end of session summary so the next one picks up where you left off
- `/skill-builder`: make a new skill
- `/excalidraw-diagram`: draw a diagram

## The framework (WAT)

This project runs on Nate Herk's WAT framework.

- **W, Workflows.** Markdown files that say what to do, step by step, in plain English. Here: the markdown in `projects/`, `references/`, and the skills under `.claude/skills/`.
- **A, Agent.** Claude Code. Reads the workflows, plans, picks the tools, runs the steps, fixes what breaks, then updates the workflow so the same thing does not break twice.
- **T, Tools.** The scripts and integrations that do the work. Here: the scripts and connected accounts listed in `connections.md`.

The loop every time: set up, describe the output wanted (not how to build it), plan mode, build, iterate on the output and let Claude update the workflow and the tools.

## Operating rules

- Look for an existing tool, script, skill, or workflow before writing a new one. Grep this repo and the AIOS first.
- When something fails, read the error, adapt, fix it, and update the workflow or tool so the next run does not fail the same way. Never retry the same call unchanged.
- Plan mode before any build. Let Claude ask its questions, read the plan, then build.
- Keep this file under 500 lines. If Claude ignores a rule, the file is too long. Specialized instructions live in `.claude/skills/`, not here.
- Project context is the sections above (who I am, what I'm working on, what matters right now).

## File structure

The WAT layout is `workflows/`, `tools/`, `temp/` (with `outputs/` and `resources/`), `.env`, `CLAUDE.md`. Mapped onto this repo:

| WAT | Here |
|---|---|
| Workflows | the markdown in `projects/`, `references/`, and the skills under `.claude/skills/`. |
| Tools | the scripts and connected accounts listed in `connections.md`. |
| Temp | `archives/` for old work. Scratch files go in Claude's own scratchpad, not here. |
| .env | `.env` at the root, gitignored, never printed. Every key also lives in the AIOS `.env`. |
| CLAUDE.md | This file. |
| Context | `context/`, `projects/`, `brainstorms/`, `decisions/log.md` |

## Style

- Mason's global rules in `~/.claude/CLAUDE.md` apply to every word: no em or en dashes, no hyphens in prose, no blockquotes, no emojis, no semicolons.
- Chat: a few sentences, answer first, no headers or recaps unless asked.
- Plain English, no jargon. Short sentences. Files named in lowercase with hyphens, dated 2026-10-27 style when a date matters.
- Anything a client reads gets shown to Mason as a draft first.
