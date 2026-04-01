---
name: next-prompts
description: Suggest 5 short, actionable prompts the user can copy-paste into Claude Code to continue their current work. Use when the user wants prompt ideas, next steps, or invokes /next-prompts.
user_invocable: true
---

# Next Prompts

Analyze the user's current project and recent work, then suggest 5 short prompts they can copy-paste directly into Claude Code.

## Process

### Step 1 — Understand the current context

Gather context by reading (do NOT modify anything):

1. **Git status** — any uncommitted changes, current branch, recent commits (`git log --oneline -10`)
2. **Project type** — scan for `package.json`, `pyproject.toml`, `go.mod`, `Cargo.toml`, etc.
3. **Open issues** — if this is a GitHub repo, check `gh issue list --limit 5` (skip silently if `gh` is not available or not authenticated)
4. **TODOs in code** — quickly scan for `TODO`, `FIXME`, `HACK`, `XXX` comments
5. **Test coverage gaps** — look for files with no corresponding test file
6. **README / docs state** — check if docs are missing or outdated relative to code

### Step 2 — Generate 5 prompts

Based on the context, produce exactly **5 prompts** that are:

- **Short** — one sentence each, under 100 characters when possible
- **Actionable** — each prompt can be pasted directly into Claude Code and executed immediately
- **Diverse** — cover different types of work (e.g., fix a bug, add a feature, write tests, refactor, improve docs)
- **Relevant** — tied to the actual state of the project, not generic advice
- **Prioritized** — ordered from most impactful to least

### Step 3 — Present the prompts

Output the prompts in this exact format so they are easy to scan and copy:

```
Here are 5 prompts for your next move:

1. <prompt text>
2. <prompt text>
3. <prompt text>
4. <prompt text>
5. <prompt text>
```

## Rules

- Do NOT modify any files — this skill is read-only
- Do NOT suggest prompts that require information you don't have (e.g., "fix the bug in ticket #123" when you haven't checked issues)
- Do NOT suggest generic prompts like "write tests" — be specific (e.g., "add unit tests for the `parseConfig` function in src/config.ts")
- Keep each prompt self-contained — the user should be able to paste it without extra context
- If the project is clean with nothing obvious to do, suggest improvement-oriented prompts (performance, refactoring, documentation, CI/CD)
