# Symphony Setup For This Repository

This repository now includes a repo-owned [`WORKFLOW.md`](/C:/Users/bnapp/OneDrive/vcode/symphony-test-app-2/WORKFLOW.md) modeled on the current Symphony Elixir README and intended to be passed to the Symphony service when it starts.

## What to configure

1. Copy [`.env.symphony.example`](/C:/Users/bnapp/OneDrive/vcode/symphony-test-app-2/.env.symphony.example) into your preferred shell env setup.
2. Fill in:
   - `LINEAR_API_KEY`
   - `SYMPHONY_PROJECT_SLUG`
   - `SYMPHONY_WORKSPACE_ROOT`
   - `SOURCE_REPO_URL`
3. In Linear, make sure the workflow includes the non-standard states Symphony commonly expects:
   - `Rework`
   - `Human Review`
   - `Merging`

## Run Symphony

Per the upstream Elixir README:

```sh
git clone https://github.com/openai/symphony
cd symphony/elixir
mise trust
mise install
mise exec -- mix setup
mise exec -- mix build
mise exec -- ./bin/symphony /absolute/path/to/this/repo/WORKFLOW.md
```

For this repository on the current machine, the workflow path is:

```text
C:\Users\bnapp\OneDrive\vcode\symphony-test-app-2\WORKFLOW.md
```

## Notes

- `SOURCE_REPO_URL` is set to the GitHub remote for this repository so Symphony can create fresh workspaces by cloning the canonical source.
- The upstream README says the `commit`, `push`, `pull`, `land`, and `linear` repo skills are optional. They are not included here yet because this repository is currently empty and does not have an established repo automation flow to tailor them against.
