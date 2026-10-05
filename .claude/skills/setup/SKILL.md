---
name: setup
description: First day setup. Interviews the user one question at a time and fills in CLAUDE.md and the context folder. Trigger on "/setup", "set me up", "fill in my brain", "get started". Safe to re run any time to update answers.
---

# Setup

Fill in this folder's brain by asking the user a few questions, one at a time.

## Questions (ask one, wait, then the next)

1. What's your name and role, and what do you do day to day?
2. What ideas or projects do you want to use this folder for?
3. What are your top 3 priorities right now?
4. How do you like answers: short and direct, or detailed? Anything you hate?
5. What tools do you use every day (email, spreadsheets, CRM, anything)?

## After the last answer

1. Rewrite `CLAUDE.md`: replace each placeholder in parentheses with the answers. Keep the "Where things live" and "Skills" sections as they are.
2. Write `context/about-me.md` from answers 1 and 4.
3. Write `context/priorities.md` from answer 3, one line per priority.
4. Add one row per tool from answer 5 to `connections.md`, all marked "Not yet".
5. For each project in answer 2, create a folder in `projects/` with a short `README.md` saying what it is.
6. Show a short summary of what was filled in and suggest trying `/grill-me` on the first project.

## Rules
- One question at a time. Never dump all five at once.
- If re running, show the current answer and ask what changed. Only update what changed.
