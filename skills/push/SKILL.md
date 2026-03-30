---
name: push
description: Commit all changes and push to the remote repository. Use when the user wants to save and push their work, or invokes /push.
user_invocable: true
---

# Push

Commit all current changes and push them to the remote repository.

## Rules

- Do NOT commit files that likely contain secrets (`.env`, credentials, tokens)
- Do NOT amend existing commits — always create a new commit
- If there are no changes, commit and push empty changes
- Keep commit messages short and meaningful
