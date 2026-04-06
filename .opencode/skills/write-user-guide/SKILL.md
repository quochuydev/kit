---
name: write-user-guide
description: Use when the user wants to create a user guide, walkthrough, or step-by-step instructions for how to use features on a web app. Triggers on requests to write user guides, feature tutorials, or onboarding docs.
---

# Write User Guide

Generate step-by-step user guides for web app features.

## Process

Before writing, ASK the user to fill in or confirm a feature table:

| Step | Action | Page |
|------|--------|------|
| 1 | Go to `{url}` | {Page name} |
| 2 | Click "{Button/Link}" | {Page name} |
| 3 | Fill in "{Field}" with {value} | {Page name} |
| ... | ... | ... |

Present this table as a template and ask the user to provide the steps. Do NOT guess the steps — the user knows their app.

## Output Format

Once the user confirms the steps, generate the guide as a markdown file with this structure:

```markdown
# {Feature Name}

## Overview
{One sentence describing what this feature does and who it's for.}

## Steps

### Step 1: {Action summary}
**Page:** {Page name}

{Action description}. Go to `{url}`.

### Step 2: {Action summary}
**Page:** {Page name}

Click **"{Button/Link}"**.

### Step 3: {Action summary}
**Page:** {Page name}

Fill in the **"{Field}"** field with your {value}.

...
```

## Action Types

Use these verbs consistently:

| Verb | When to use |
|------|-------------|
| **Go to** | Navigate to a URL or page |
| **Click** | Press a button, link, or menu item |
| **Fill in** | Enter text into an input field |
| **Select** | Choose from a dropdown or radio buttons |
| **Toggle** | Turn a switch on or off |
| **Upload** | Attach a file |
| **Confirm** | Accept a dialog or review a summary |

## Rules

- Always ask for the step table FIRST — never assume the app's UI
- Keep each step to ONE action
- Bold all UI element names (buttons, fields, links)
- Include the page name for every step
- Use backticks for URLs
- Write in plain language — the audience is end users, not developers
- Save output to `docs/user-guides/{feature-name}.md`
