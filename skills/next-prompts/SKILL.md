---
name: next-prompts
description: Suggest 5 short prompts to copy-paste into Claude Code based on the user's argument or current project context. Use when the user wants prompt ideas, next steps, or invokes /next-prompts.
user_invocable: true
---

# Next Prompts

Generate 5 short, actionable prompts the user can copy-paste into Claude Code.

## Process

### Step 1 — Determine the topic

Check if the user provided an argument after `/next-prompts`:

- If an argument is provided (e.g., `/next-prompts authentication`), use it as the topic.
- If no argument is provided, infer the topic from the current project context:
  1. Read `package.json`, `README.md`, or other project markers to understand the stack.
  2. Run `git log --oneline -5` to see recent work.
  3. Run `git diff --name-only HEAD~3..HEAD` to see recently changed files.
  4. Use these signals to suggest prompts relevant to what the user is actively working on.

### Step 2 — Generate 5 prompts

Create exactly 5 prompts that are:

- **Short** — each prompt should be 1 sentence, under 80 characters when possible
- **Actionable** — each prompt should be something Claude Code can directly act on
- **Specific** — reference the actual stack, framework, or domain from the project
- **Varied** — cover different types of work (e.g., feature, test, refactor, debug, docs)
- **Progressive** — order from simplest/quickest to most involved

### Step 3 — Output the prompts

Display the prompts in this exact format:

```
💡 Next prompts (<topic>):

1. <prompt>
2. <prompt>
3. <prompt>
4. <prompt>
5. <prompt>
```

## Rules

- ALWAYS output exactly 5 prompts — no more, no less
- Keep prompts concise — they should be easy to scan and copy
- Do NOT include slash commands in the generated prompts — these are plain prompts for Claude Code
- Do NOT execute any of the prompts — only suggest them
- Do NOT read or modify project source code beyond what is needed to understand context
- If the topic is too vague to generate useful prompts, ask the user to be more specific
