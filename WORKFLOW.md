---
tracker:
  kind: linear
  api_key: $LINEAR_API_KEY
  project_slug: $SYMPHONY_PROJECT_SLUG
  active_states:
    - Todo
    - In Progress
    - Human Review
    - Merging
    - Rework
  terminal_states:
    - Closed
    - Cancelled
    - Canceled
    - Duplicate
    - Done
polling:
  interval_ms: 5000
workspace:
  root: $SYMPHONY_WORKSPACE_ROOT
hooks:
  after_create: |
    git clone "$SOURCE_REPO_URL" .
    if command -v mise >/dev/null 2>&1 && [ -f .mise.toml ]; then
      mise trust
      mise install
    fi
agent:
  max_concurrent_agents: 3
  max_turns: 20
codex:
  command: codex app-server
---
You are working on Linear issue `{{ issue.identifier }}` for this repository.

Issue context:
- Identifier: {{ issue.identifier }}
- Title: {{ issue.title }}
- State: {{ issue.state }}
- Labels: {{ issue.labels }}
- URL: {{ issue.url }}

Description:
{% if issue.description %}
{{ issue.description }}
{% else %}
No description provided.
{% endif %}

Operating rules:
1. Work only inside the provided issue workspace.
2. Start by reproducing the problem or confirming the requested behavior.
3. Keep changes scoped to the issue.
4. Validate your work with relevant tests, checks, or manual verification.
5. If you are blocked by missing credentials, permissions, or external configuration, stop and report the blocker clearly.
6. If repo-local skills exist under `.codex/skills`, use them when they fit the task.

Expected final response:
- What changed
- How it was validated
- Any remaining blocker or risk
