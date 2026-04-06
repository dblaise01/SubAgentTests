# SubAgentTests

A personal testing ground for a configurable sub-agent team. The interaction matrix in `docs/` defines how roles collaborate, and the prompt templates in `docs/prompts/` provide structured starting points for engaging the team.

## Project Structure

### `docs/matrix.md`

The core reference document. Defines:

- **RACI-style interaction matrix** across 15 roles (Team Lead, Architect, Product Strategist, etc.)
- **Best interaction paths** — who should talk to whom first and why
- **Interaction rules** for leadership, execution, and specialist behavior
- **`TEAM_MODE`** (`controller` vs `multi`) — single consolidated voice vs explicit per-role debate
- **`TEAM_SHAPE`** (`dev`, `debug`, `architecture`, `release`, `ai-workflow`) — which roles activate based on task type
- **`TEAM_INTENSITY`** — controls how strictly roles challenge and gate decisions

### `docs/prompts/`

Fill-in-the-blank templates that wire a user's task into the team configuration defined by the matrix.

| File | Mode / Shape | Purpose |
|---|---|---|
| `default.md` | `controller` / `dev` | Standard feature build or iteration |
| `high-level.md` | `multi` / `architecture` | High-level project review and next-phase readiness assessment |
| `refactor.md` | `multi` / `architecture` | Structural refactor or redesign with full role debate |
