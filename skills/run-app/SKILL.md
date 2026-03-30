---
name: run-app
description: Detect the local project type, check for required environment variables, and start or restart the app on localhost. Use when the user wants to run, start, or restart their local app, or invokes /run-app.
user_invocable: true
---

# Run App

Detect the project type, verify environment setup, and start (or restart) the app on localhost.

## Process

### Step 1 — Detect the project type

Read the current directory for project markers to determine the stack:

| Marker file            | Stack                  | Default start command            |
|------------------------|------------------------|----------------------------------|
| `package.json`         | Node.js                | Read `scripts.dev` or `scripts.start` from package.json |
| `requirements.txt` / `pyproject.toml` / `setup.py` | Python | `python manage.py runserver` / `uvicorn` / `flask run` (infer from deps) |
| `Gemfile`              | Ruby / Rails           | `bundle exec rails server`       |
| `go.mod`               | Go                     | `go run .`                       |
| `Cargo.toml`           | Rust                   | `cargo run`                      |
| `docker-compose.yml`   | Docker Compose         | `docker compose up`              |
| `Makefile`             | Check for `run`/`dev`/`start` target | `make dev` or `make run` |

If multiple markers exist, prefer `docker-compose.yml` first, then the primary language marker. If you cannot determine the stack, ASK:

> What command do you normally use to start this app?

### Step 2 — Check required environment variables

1. Look for `.env.example`, `.env.sample`, `.env.template`, or environment documentation in the project.
2. Compare with the existing `.env` file (if any).
3. Also scan the codebase for `process.env.`, `os.environ`, `os.Getenv`, `ENV[` or similar patterns to discover required variables.

If any required variables are **missing or empty**, print a clear setup guide:

```
⚠️  Missing environment variables:

| Variable        | Description              | Where to get it            |
|-----------------|--------------------------|----------------------------|
| DATABASE_URL    | PostgreSQL connection    | Your database provider     |
| API_KEY         | Third-party API key      | https://example.com/keys   |

Create a `.env` file or copy from the template:

  cp .env.example .env

Then fill in the missing values and run /run-app again.
```

**Stop here** if critical variables (like database URLs or required API keys) are missing — do NOT attempt to start the app.

### Step 3 — Kill any existing process on the target port

1. Determine the port from: `.env`, config files, or default for the framework (e.g., 3000, 8000, 8080, 4000).
2. Check if the port is already in use: `lsof -ti:<port>`
3. If a process is running on that port, kill it: `kill -9 $(lsof -ti:<port>)`
4. Confirm the port is free before proceeding.

### Step 4 — Install dependencies (if needed)

If a lock file exists but `node_modules` / `vendor` / `.venv` / `target` is missing, install first:

| Lock file            | Install command         |
|----------------------|-------------------------|
| `package-lock.json`  | `npm install`           |
| `yarn.lock`          | `yarn install`          |
| `pnpm-lock.yaml`     | `pnpm install`          |
| `bun.lockb`          | `bun install`           |
| `Gemfile.lock`       | `bundle install`        |
| `requirements.txt`   | `pip install -r requirements.txt` |
| `poetry.lock`        | `poetry install`        |
| `go.sum`             | `go mod download`       |
| `Cargo.lock`         | `cargo build`           |

### Step 5 — Start the app

Run the start command **in the background** using the Bash tool with `run_in_background: true`.

After launching, briefly confirm:

```
✅ App started on http://localhost:<port>
   Command: <the command used>
   To stop:  kill -9 $(lsof -ti:<port>)
```

## Rules

- NEVER expose or log secret values from `.env` files
- ALWAYS kill the existing process before starting a new one — do not leave orphan processes
- If `docker-compose.yml` exists and the user hasn't said otherwise, prefer `docker compose up` over bare commands
- If the start command fails, read the error output and suggest a fix rather than silently retrying
- Use the project's own scripts (e.g., `npm run dev`) rather than inventing custom commands
- Do NOT modify any project files — this skill only reads and runs
