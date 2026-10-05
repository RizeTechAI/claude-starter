---
name: skill-builder
description: Use when the user wants to create a new skill, modify an existing skill, troubleshoot why a skill isn't triggering, or asks how Claude Code skills work. Walks through the skill structure, frontmatter, file placement, supporting files, and common patterns.
---

# Skill Builder

Use this skill when the user wants to build a new Claude Code skill, edit an existing one, troubleshoot one that isn't triggering, or learn how the skill system works.

## Workflow

### Step 1: Understand the goal
Confirm with the user (skip if already clear from the request):
- What should the skill do? (the task or workflow it executes)
- When should it trigger? (auto-detection on natural language, or `/slash-command` only)
- Where should it live?
  - **Project-only:** `.claude/skills/<name>/SKILL.md` (in the current project)
  - **Personal, all projects:** `~/.claude/skills/<name>/SKILL.md`
  - **Plugin:** `<plugin>/skills/<name>/SKILL.md`

### Step 2: Check the reference
Read `reference.md` in this directory for the full technical reference: frontmatter fields, invocation control matrix, argument substitution variables, file location priority, `allowed-tools` syntax, advanced patterns (subagent forks, lifecycle hooks, dynamic context injection, extended thinking keyword), permissions, and troubleshooting.

### Step 3: Plan the skill
Before writing any markdown, lock these:
1. **Name** (lowercase, hyphens only, max 64 chars).
2. **Description** (one sentence, keyword-rich so Claude can auto-invoke when relevant).
3. **Location** (project / personal / plugin).
4. **Trigger conditions** (auto-invocation keywords vs `/slash-command` only).
5. **Tools needed** (use `allowed-tools` to restrict if needed).
6. **Context mode** (main context vs `context: fork` subagent. Only use fork if the task is self-contained and doesn't need conversation history).
7. **Supporting files** (does the skill need a `reference.md` for detail, or a `scripts/` folder?).

### Step 4: Write SKILL.md
- Lead with YAML frontmatter.
- Keep the file **under 500 lines.** Move detail to a separate `reference.md` in the same skill directory.
- Include a clear workflow with numbered steps.
- Reference any supporting files explicitly so Claude knows they exist (Claude does NOT auto-load them).
- **CRITICAL.** Do NOT include literal argument-substitution placeholders (the dollar-sign forms) or the extended-thinking keyword in the SKILL.md content unless you want them to take effect on every invocation. Use neutral wording or describe them in `reference.md` instead. Backticks and code fences do NOT escape these. See `reference.md` for the actual syntax.

### Step 5: Install the skill
- Create the directory at the chosen location.
- Save `SKILL.md` there.
- If using supporting files (`reference.md`, scripts, examples), put them in the same directory.
- For a project skill: `.claude/skills/<name>/SKILL.md`

### Step 6: Test
- Confirm the skill appears in the `/` menu (if `user-invocable: true`, which is the default).
- Try `/skill-name` to verify it loads.
- If auto-invocation matters, test with a natural-language phrase that matches the description.
- If something doesn't work, check the **Troubleshooting** section in `reference.md`.

---

## Common Patterns (described, not literal)

The literal YAML and placeholder syntax for these patterns is in `reference.md`. Below is the conceptual map of what each pattern does and when to use it.

### Read-only research skill (runs in a subagent)
Use `context: fork` plus `agent: Explore` and restrict tools to `Read, Grep, Glob`. Best when the skill does a self-contained research task and the answer can return as a single report. Bad when the skill needs back-and-forth conversation.

### Skill that runs a bundled script
Use `allowed-tools` to permit only the specific command (e.g. a python script) and have the SKILL.md tell Claude to run it. The script lives in the skill directory at `<skill>/scripts/<name>.py`. Good for visual or computationally heavy work.

### Skill that takes positional arguments
Use `argument-hint` in frontmatter to document expected args. In the SKILL.md body, reference the args by the dollar-sign-positional syntax. **Do not put these literal placeholders into THIS skill-builder's SKILL.md** because they would substitute when this skill loads. See `reference.md` for the exact syntax.

### Skill with dynamic context injection
The exclamation-mark plus backticked-command syntax runs the shell command BEFORE Claude sees the prompt, replacing the placeholder with the command's output. Useful for injecting `git status`, `gh pr diff`, file listings, etc. **Be careful:** these execute every time the skill loads. If the command can fail (e.g. PR-related skill on a non-PR branch), the whole skill fails to load. Same warning: don't put the literal syntax into THIS file. See `reference.md`.

---

## Anti-patterns (do NOT do these)

- **Putting always-relevant project rules in a skill.** Those belong in `CLAUDE.md`. Skills are for task-specific workflows, not project-wide context.
- **Using `context: fork` for a skill without a concrete task.** Subagents need an actionable prompt. Reference-only material with no instruction returns nothing useful.
- **Writing a SKILL.md over 500 lines.** Move detail to a `reference.md` in the same directory.
- **Forgetting to reference supporting files in SKILL.md.** Supporting files do NOT auto-load. Claude reads them only when SKILL.md mentions them.
- **Vague descriptions.** "A helper skill" won't trigger auto-invocation. Be specific about the task and when to use it.
- **Putting literal argument-substitution syntax or the extended-thinking keyword in your SKILL.md.** They will trigger on every invocation. Describe them in prose or move literal examples to `reference.md`.

---

## Reference

Full technical reference lives in `reference.md` in this directory. Includes:
- Complete frontmatter field table
- Invocation control matrix (`disable-model-invocation`, `user-invocable`)
- Argument substitution variables (dollar-sign forms, session-id variable)
- File location priority (enterprise / personal / project / plugin)
- `allowed-tools` syntax with glob patterns
- Subagent fork behavior and agent options
- Hooks (PreToolUse, PostToolUse, Stop)
- Permission rules (`Skill(name)`, `Skill(name *)`)
- The extended-thinking keyword and how to use it intentionally
- Troubleshooting (skill not triggering, triggers too often, subagent returns nothing, arguments not substituted)
