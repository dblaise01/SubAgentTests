# PR Agents Usage

This folder contains a controller-based PR workflow for Azure DevOps pull requests.
It is designed to answer two common operational questions quickly:

- What changed since my last PR snapshot?
- Which PRs need attention right now?

## What Is Included

- `agents/pr-controller.agent.md`: Main orchestrator.
- `agents/azure-devops-mcp-caller.agent.md`: Live PR retrieval and normalization.
- `agents/pr-snapshot-manager.agent.md`: Snapshot load/save in workspace.
- `agents/pr-change-analyzer.agent.md`: Current vs previous comparison.
- `agents/pr-triage.agent.md`: Urgency and action classification.
- `agents/pr-report-writer.agent.md`: Final readable report.
- `prompts/pr-changes.prompt.md`: Prompt template for delta view.
- `prompts/pr-needs-attention.prompt.md`: Prompt template for action-first view.

## Typical Workflow

1. User asks for PR changes or attention status for an account email.
2. PR Controller extracts and normalizes the email (lowercase).
3. Azure DevOps MCP Caller fetches the current active PR state.
4. PR Snapshot Manager loads the latest prior snapshot when available.
5. PR Change Analyzer computes exact deltas.
6. PR Triage classifies urgency.
7. PR Report Writer generates concise operational output.
8. PR Snapshot Manager persists the new snapshot as latest and history.

## Supported Prompt Intents

Use one of the provided prompts (or equivalent natural language):

- PR Changes
	- "Give me PR changes for username@company.com"
	- "Compare today's PR status with the prior snapshot for username@company.com"
- PR Needs Attention
	- "Which PRs need attention for username@company.com?"
	- "Show me my blocked or stalled PRs for username@company.com"

Defaults:

- Active PRs only.
- Comparison target is the most recent prior snapshot.
- Output stays concise and actionable.
- Raw JSON is not returned unless explicitly requested.

## Output Shape

Final reports should contain these sections:

- Summary
- Changes by PR
- Needs Attention
- Waiting / Healthy
- Suggested Next Actions

When discussing a PR, always include:

- PR id
- PR title
- Repository

## Snapshot Storage

Snapshots are project-local and isolated per repository workspace.

Folders:

- `.github/pr-snapshots/latest/`
- `.github/pr-snapshots/history/<normalized-email>/`

Files:

- Latest: `.github/pr-snapshots/latest/<normalized-email>.json`
- History: `.github/pr-snapshots/history/<normalized-email>/<timestamp>.json`

Timestamp format:

- `YYYY-MM-DDTHH-mm-ss`

Notes:

- Email lookup is case-insensitive by normalizing to lowercase.
- If no prior snapshot exists, the system still returns a valid current-state report.
- If live retrieval is partial, the system continues with best available data and reports missing parts.

## Operational Guidance

- Use PR Changes for movement tracking between snapshots.
- Use PR Needs Attention for immediate prioritization.
- Keep prompts specific by including target account email.
- Run the workflow regularly to build useful history for trend comparison.

## Quick Start

1. Ensure the PR agent files are available to your Copilot agent locations.
2. Open chat and invoke the PR Controller flow using one of the prompt examples above.
3. Provide the target account email.
4. Review the generated attention and action sections first.
