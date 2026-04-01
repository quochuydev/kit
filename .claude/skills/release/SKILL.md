---
name: release
description: Bump the .claude-plugin version (patch, minor, or major) in plugin.json and marketplace.json, commit, and push. Use when the user wants to release a new version, or invokes /release.
user_invocable: true
---

# Release

Bump the plugin version, commit the change, and push to remote.

## Process

### Step 1 — Determine the bump type

Check if the user specified a bump type in their message:

- `patch` (default) — e.g., 0.1.2 → 0.1.3
- `minor` — e.g., 0.1.2 → 0.2.0
- `major` — e.g., 0.1.2 → 1.0.0

If not specified, default to **patch**.

### Step 2 — Read the current version

Read `.claude-plugin/plugin.json` and extract the current `version` field.

### Step 3 — Calculate the new version

Increment the appropriate segment based on the bump type. Reset lower segments to 0 when bumping minor or major.

### Step 4 — Update version in both files

Update the `version` field in:

1. `.claude-plugin/plugin.json`
2. `.claude-plugin/marketplace.json` (inside the `plugins[0].version` field)

Both files must have the exact same new version.

### Step 5 — Commit and push

1. Stage both files: `git add .claude-plugin/plugin.json .claude-plugin/marketplace.json`
2. Commit with message: `Bump version to <new_version>`
3. Push to the current remote branch: `git push`

### Step 6 — Confirm

Output:

```
✅ Released v<new_version> (was v<old_version>)
   Bump: <patch|minor|major>
   Pushed to: <branch>
```

## Rules

- ALWAYS update both `plugin.json` and `marketplace.json` — they must stay in sync
- NEVER amend an existing commit — always create a new one
- If there are other uncommitted changes, commit ONLY the two version files — do not include unrelated changes
- If the push fails, show the error and suggest the user fix it manually (e.g., set upstream, resolve conflicts)
