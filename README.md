# kit — Claude Code Kit

A Claude Code plugin with productivity skills for committing code, writing user stories, and generating user guides.

## Skills

| Command              | What it does                                                |
| -------------------- | ----------------------------------------------------------- |
| `/push`              | Commit all changes and push to the remote repository        |
| `/write-user-story`  | Write user stories with acceptance criteria                  |
| `/write-user-guide`  | Create step-by-step user guides for web app features        |
| `/research-apis`     | Research third-party APIs with setup guides and curl examples |

## Installation

```bash
claude plugin marketplace add quochuydev/kit
claude plugin install kit
```

## Updating

```bash
claude plugin marketplace update kit-marketplace
claude plugin update kit@kit-marketplace
```

## Remove

```bash
claude plugin remove kit
```

## Usage

```
/push
/write-user-story
/write-user-guide
/research-apis
```

## License

MIT
