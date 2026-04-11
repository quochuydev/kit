# kit — AI Coding Agent Kit

A plugin with productivity skills for committing code, writing user stories, and generating user guides. Works with **Claude Code** and **OpenCode**.

## Skills

| Command             | What it does                                                        |
| ------------------- | ------------------------------------------------------------------- |
| `/research-apis`    | Research third-party APIs with setup guides and curl examples       |
| `/write-user-story` | Write user stories with acceptance criteria                         |
| `/run-app`          | Detect project type, check env vars, and start/restart on localhost |
| `/push`             | Commit all changes and push to the remote repository                |
| `/write-user-guide` | Create step-by-step user guides for web app features                |

## Installation

### Claude Code

```bash
claude plugin marketplace add quochuydev/kit
claude plugin install kit
```

### OpenCode

```bash
npx skills add quochuydev/kit -a opencode
```

## Updating

### Claude Code

```bash
claude plugin marketplace update kit-marketplace
claude plugin update kit@kit-marketplace
```

### OpenCode

```bash
npx skills add quochuydev/kit -a opencode
```

## Remove

### Claude Code

```bash
claude plugin remove kit
```

### OpenCode

```bash
npx skills remove quochuydev/kit -a opencode
```

## Usage

```
/research-apis
/run-app
/push
/write-user-story
/write-user-guide
```

## License

MIT
