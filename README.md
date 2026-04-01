# kit — Claude Code Kit

A Claude Code plugin with productivity skills for committing code, writing user stories, and generating user guides.

## Skills

| Command             | What it does                                                        |
| ------------------- | ------------------------------------------------------------------- |
| `/research-apis`    | Research third-party APIs with setup guides and curl examples       |
| `/write-user-story` | Write user stories with acceptance criteria                         |
| `/run-app`          | Detect project type, check env vars, and start/restart on localhost |
| `/next-prompts`     | Suggest 5 short prompts to copy-paste into Claude Code              |
| `/push`             | Commit all changes and push to the remote repository                |
| `/write-user-guide` | Create step-by-step user guides for web app features                |

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
/next-prompts
/research-apis
/run-app
/push
/write-user-story
/write-user-guide
```

## License

MIT
