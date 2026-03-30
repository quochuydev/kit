---
name: push
description: Commit all changes and push to the remote repository. Use when the user wants to save and push their work, or invokes /push.
user_invocable: true
---

# Push

Commit all current changes and push them to the remote repository.

## Process

1. Run `git status` to see all changed and untracked files. If there are no changes, inform the user and **stop**.
2. Run `git diff` and `git diff --cached` to review all staged and unstaged changes.
3. Run `git log --oneline -5` to understand the recent commit message style.
4. Stage all relevant changes with `git add -A`.
5. Generate a concise commit message that summarizes the changes (1-2 sentences, focus on the "why"). Use a HEREDOC to pass the message:
   ```
   git commit -m "$(cat <<'EOF'
   Your commit message here
   EOF
   )"
   ```
6. Push to the remote with `git push`. If the branch has no upstream, use `git push -u origin <branch>`.
7. Confirm success by showing the push output to the user.
8. **Stop.** You are done.

## Rules

- Do NOT commit files that likely contain secrets (`.env`, credentials, tokens)
- Do NOT amend existing commits — always create a new commit
- Do NOT force push
- If there are no changes, say so and stop
- Keep commit messages short and meaningful
