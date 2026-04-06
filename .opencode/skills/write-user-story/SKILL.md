---
name: write-user-story
description: Use when the user wants to write, add, or draft user stories for features, epics, or requirements. Triggers on requests to create user stories, acceptance criteria, or feature specifications.
---

# Write User Story

Generate user stories following the project's established format.

## Structure

Each user story MUST follow this exact structure:

```markdown
### US {epic}.{number}: {Title}

**As a {role}**, I want to {action}, {so that benefit}.

**Acceptance Criteria:**

- {Criterion 1}
- {Criterion 2}
- ...
```

Separate each user story with a horizontal rule (`---`).

## Rules

- **Role**: Use specific roles (e.g., "new patient", "returning patient", "administrator", "system operator", "content creator"), not generic "user"
- **Action**: State what the user wants to do — one clear action per story
- **Benefit**: State why — the value or outcome the user gains
- **Acceptance Criteria**: Concrete, testable, and specific
  - Include measurable thresholds (e.g., "within 2 seconds", "max 5 items", "min. 10 characters")
  - Include API behavior where applicable (endpoints, error handling, retry logic)
  - Include GDPR/privacy requirements where personal data is involved
  - Include error/edge case handling (fallbacks, rate limits, timeouts)
  - Include UI behavior specifics (what is visible, when, where)

## Epic Grouping

When writing multiple stories, group them under epics:

```markdown
## {number} Epic: {Epic Name}
```

## Numbering

- Epics: `1.1`, `1.2`, `1.3`, ...
- Stories within an epic: `US 1.1.1`, `US 1.1.2`, ...

When adding to an existing document, continue from the last used number.

## Quality Checklist

Before finishing, verify each story has:

- [ ] A specific user role (not "user")
- [ ] One clear action per story
- [ ] A stated benefit
- [ ] 3-6 acceptance criteria that are testable and measurable
- [ ] Error handling / edge cases addressed
- [ ] Privacy (GDPR) considerations if personal data is involved

## Output

Write user stories to `docs/user-stories.mdx`. If the file exists, append new stories. If creating a new epic, add it after the last epic and before the Summary section.
