---
name: repo-meta
description: Read the current working folder and suggest a GitHub repo name, description, topic tags, and an image-generation prompt for a logo. Use when the user wants to publish a project to GitHub, or invokes /repo-meta.
user_invocable: true
---

# Repo Meta

Inspect the current working directory and propose GitHub metadata the user can paste straight into the "Create repository" form, plus a ready-to-use logo prompt for an image model (e.g. Gemini Nano Banana, Midjourney, DALL·E).

## Process

1. Detect the project. Read only what's needed — in priority order, stop once you have enough:
   - `README.md` (title, tagline, first paragraph) — usually the best single source
   - The primary manifest for the stack: `package.json`, `pyproject.toml`, `Cargo.toml`, `go.mod`, or `.claude-plugin/`
   - Top-level folder names only if the above are thin
2. If signals are thin or conflicting, ASK one short clarifying question (e.g. "Is this a CLI, library, or web app?") before generating suggestions. Otherwise skip straight to output.
3. Produce the output below. Offer **3 repo name options** so the user can pick one.

## Output Format

```
**Detected:** {one-line summary — e.g. "Node.js CLI for converting Markdown to PDF"}

**Repo name options:**
1. `{kebab-case-name-1}` — {why it fits}
2. `{kebab-case-name-2}` — {why it fits}
3. `{kebab-case-name-3}` — {why it fits}

**Description** (80–100 chars, GitHub "About" field):
> {one-sentence description, no trailing period unless it reads better with one}

**Topics** (GitHub tags, lowercase, hyphenated, max 20):
`tag-1` `tag-2` `tag-3` ...

**Logo prompt** (for image AI, non-transparent background):
> {prompt paragraph — see Rules below}
```

## Rules

### Repo name
- Lowercase, kebab-case, ASCII only, no leading/trailing hyphens.
- Short (ideally ≤ 25 chars). Memorable over descriptive.
- Avoid trademarked names (don't prefix with `react-`, `next-`, `openai-`, etc. unless the project is genuinely an extension of that ecosystem).
- Don't reuse the user's GitHub username as a prefix unless it's already their convention in the folder.

### Description
- One sentence, **80–100 characters** — aim for this range, don't go over.
- Lead with the noun (what it IS), then the verb (what it does). Example: "CLI that converts Markdown to styled PDFs."
- No marketing fluff ("blazing fast", "next-gen"). No emojis unless the user explicitly asks.

### Topics
- Lowercase, hyphen-separated, 5–15 tags.
- Mix: language (`typescript`), framework (`nextjs`), domain (`markdown`, `pdf`), and type (`cli`, `library`, `plugin`).
- Use tags that already exist on GitHub (check https://github.com/topics/{tag} mentally — prefer common ones over invented ones).

### Logo prompt
- Write ONE paragraph, 2–4 sentences, that an image model can consume directly.
- Must specify: subject, style (flat / 3D / isometric / minimalist / etc.), color palette, and **a solid background color** (because the user generates non-transparent logos).
- Keep the subject simple — a single icon or symbol, not a scene.
- End with format hint: `Square 1:1, centered, suitable for a GitHub repo avatar.`
- Do NOT include text or letters in the logo (image models render text poorly).

## Example

```
**Detected:** Node.js CLI that batch-renames image files using EXIF data

**Repo name options:**
1. `exif-rename` — direct, describes the core action
2. `photo-tidy` — friendlier, works if you expand beyond EXIF later
3. `snap-sort` — short and memorable

**Description:**
> CLI that batch-renames photos based on EXIF timestamps and camera metadata

**Topics:**
`cli` `nodejs` `typescript` `exif` `photography` `image-processing` `batch-rename` `metadata`

**Logo prompt:**
> A minimalist flat-design icon of a camera shutter blending into a file-folder shape, rendered in soft teal and warm orange on a solid deep-navy background. Clean geometric lines, subtle inner shadow for depth, no text. Square 1:1, centered, suitable for a GitHub repo avatar.
```
