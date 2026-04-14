# PR Changes

Use this prompt when you want the latest PR movement for a specific account email.

Goal:
Show what changed across the user’s active pull requests compared with the most recent prior snapshot.

Instructions:
- Route the request through the PR Controller.
- Extract the target account email from the request.
- Fetch the current active PR snapshot using Azure DevOps MCP Caller.
- Load the most recent prior snapshot from the workspace when available.
- Compare current vs previous state using PR Change Analyzer.
- Rank urgency using PR Triage.
- Produce the final readable summary using PR Report Writer.

Default behavior:
- Default to active PRs only.
- Default comparison target is the most recent prior snapshot.
- Prefer concise operational output.
- Do not dump raw JSON unless explicitly requested.
- If some live data is missing, continue with the best available comparison and state what is missing.

Focus the comparison on:
- new PRs
- removed, merged, or closed PRs
- reviewer changes
- vote changes
- thread/comment deltas
- draft ↔ ready-for-review changes
- merge/conflict changes

Desired final output sections:
- Summary
- Changes by PR
- Needs Attention
- Waiting / Healthy
- Suggested Next Actions

Output rules:
- Always include PR id, title, and repository when discussing a PR.
- Prefer exact before/after values when available.
- Call out partial retrieval clearly.
- Keep the result concise and actionable.

Example usage:
- Give me PR changes for username@company.com
- Show what changed on my PRs since the last snapshot for username@company.com
- Compare today’s PR status with the prior snapshot for username@company.com