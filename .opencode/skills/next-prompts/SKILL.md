---
name: next-prompts
description: Suggest 5 business-focused prompts to copy-paste. Use when the user wants ideas or next steps.
---

# Next Prompts

Generate 5 prompts the user can copy-paste, focused on business, ideas, and UI/UX.

## Process

1. If the user provided an argument (e.g., `/next-prompts e-commerce`), use it as the topic.
2. If no argument, read `README.md` to understand the project, then infer a relevant topic.
3. Generate 5 prompts focused on **business ideas, feature ideas, product strategy, and UI/UX improvements** — not technical implementation details.

## Prompt guidelines

- **Short** — 1 sentence, under 80 characters when possible
- **Business & product focused** — think revenue, users, market fit, monetization, growth
- **UI/UX focused** — think user flows, design improvements, accessibility, user experience ideas
- **Varied** — cover different angles (e.g., new feature idea, UI improvement, pricing strategy, user retention, UX flow, product differentiation)
- **Progressive** — order from quick win to bigger vision

## Output format

```
💡 Next prompts (<topic>):

1. <prompt>
2. <prompt>
3. <prompt>
4. <prompt>
5. <prompt>
```

## Rules

- Output exactly 5 prompts
- Do NOT include slash commands in the prompts
- Do NOT execute any prompts — only suggest them
