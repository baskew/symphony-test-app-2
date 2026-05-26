# symphony-test-app-2

This repository is a minimal Symphony test repository configured to use Linear as its issue tracker.

## Repository contents

- `WORKFLOW.md` defines the Symphony tracker, polling, workspace, and agent configuration used to run this repo.
- `SYMPHONY_SETUP.md` documents the environment variables and local steps required to launch Symphony against this repository.
- `.env.symphony.example` provides the expected environment variable names for local setup.

## Prerequisites

Before running Symphony, configure these environment variables:

- `LINEAR_API_KEY`
- `SYMPHONY_PROJECT_SLUG`
- `SYMPHONY_WORKSPACE_ROOT`
- `SOURCE_REPO_URL`

This repository also expects the Linear workflow to include these active states:

- `Todo`
- `In Progress`
- `Human Review`
- `Merging`
- `Rework`

## Running Symphony

Follow the upstream Symphony Elixir setup:

```sh
git clone https://github.com/openai/symphony
cd symphony/elixir
mise trust
mise install
mise exec -- mix setup
mise exec -- mix build
mise exec -- ./bin/symphony /absolute/path/to/this/repo/WORKFLOW.md
```

On the current machine, the workflow file is located at:

```text
C:\Users\bnapp\OneDrive\vcode\symphony-test-app-2\WORKFLOW.md
```

## Notes

- `SOURCE_REPO_URL` should point at the canonical Git remote for this repository so new workspaces clone the correct source.
- The repo is intentionally small and currently focuses on validating Symphony workflow configuration rather than shipping an application.
- For more setup detail, see `SYMPHONY_SETUP.md`.
