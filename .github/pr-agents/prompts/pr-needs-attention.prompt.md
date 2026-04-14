# PR Needs Attention

Use this prompt when you want to know which pull requests need action now for a specific account email.

Goal:
Identify the PRs that most need attention and explain why, using the latest live snapshot plus change context when available.

Instructions:
- Route the request through the PR Controller.
- Extract the target account email from the request.
- Fetch the current active PR snapshot using Azure DevOps MCP Caller.
- Load the most recent prior snapshot from the workspace when available.
- Use PR Change Analyzer to detect recent movement when prior state exists.
- Use PR Triage to classify PRs by urgency and action status.
- Use PR Report Writer to produce the final readable summary.

Default behavior:
- Default to active PRs only.
- Prefer reasons tied to reviewer votes, unresolved threads, active thread counts, age, and merge/conflict state.
- Use prior snapshot context when available, but still work if only current live data exists.
- Do not dump raw JSON unless explicitly requested.

Primary categories:
- needs my action
- waiting on others
- blocked
- stalled
- healthy / no action

Prioritization guidance:
- Put items requiring the user’s immediate action first.
- Prefer exact PR ids, titles, and repositories.
- Call out why a PR needs attention in one line when possible.
- Separate blockers from passive waiting states.

Desired final output sections:
- Summary
- Needs Attention
- Waiting / Healthy
- Changes by PR
- Suggested Next Actions

Output rules:
- Always include PR id, title, and repository when discussing a PR.
- Keep the result concise and operational.
- If live retrieval is partial, continue with best available data and state what is missing.
- If no prior snapshot exists, say that attention ranking is based on the current snapshot only.

Example usage:
- Which PRs need attention for username@company.com?
- Show me my blocked or stalled PRs for username@company.com
- What needs my action right now in my active PRs?