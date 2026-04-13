# SubAgentTests — Comprehensive Agent System

A production-ready collection of **three specialized agent ecosystems** for GitHub Copilot in VS Code:

1. **Team Agents** — A full roster of 15 specialized roles (Product, Architect, Engineering, QA, DevOps, Security, AI, etc.) that collaborate using a RACI-style interaction matrix
2. **Flow Agents** — Controller-based system for analyzing code execution paths, tracing call flows, and generating Mermaid diagrams
3. **PR Agents** — Specialized agents for pull request triage, change analysis, reporting, and Azure DevOps integration

---

## 🚀 Quick Start

### Prerequisites: Configure Agent File Locations

⚠️ **DO THIS FIRST** — VS Code needs to know where to find your agent files.

1. Open VS Code **Settings** (Ctrl+Comma or Cmd+,)
2. Search for `Agent Files Locations`
3. Add the agent folders to your settings:
   - Add `~/AppData/Roaming/Code/User/agents` (Windows)
   - Or add any custom folder where you'll store agents
4. Click **Add Item** for each location
5. **NOTE** Until glob patterns are added for chat agent locations, add specific paths if you organize your agents like so:
   - Add `~/AppData/Roaming/Code/User/agents/flow-agents` (Windows)

Alternatively, edit your `settings.json` directly:
```json
{
  "github.copilot.chat.agentFileLocations": [
    "~/AppData/Roaming/Code/User/agents"
  ]
}
```

### Installation to VS Code Roaming Profile

Once locations are configured, copy agent files to your roaming profile:

**Windows Roaming Profile Location:**
```
C:\Users\<YourUsername>\AppData\Roaming\Code\User\agents
```

#### Manual Copy
1. Navigate to your roaming profile agents folder
2. Create subdirectories for each agent ecosystem:
   ```
   C:\Users\<YourUsername>\AppData\Roaming\Code\User\agents\
     ├── team-agents/
     ├── flow-agents/
     └── pr-agents/
   ```
3. Copy agent definitions from `.github/<agent-system>/agents/` to the corresponding roaming folder
4. Copy prompt templates from `.github/<agent-system>/prompts/` if available
5. Reload VS Code

---

## 📁 Project Structure

```
.github/
├── team-agents/                    # Full team of 15 specialized roles
│   ├── agents/                     # 15 role agents
│   ├── docs/
│   │   └── matrix.md               # RACI interaction matrix
│   ├── prompts/                    # Task entry templates
│   └── templates/                  # Workflow templates
│
├── flow-agents/                    # Code flow & diagram generation
│   ├── agents/
│   │   ├── flow-organizer.agent.md (controller)
│   │   ├── entry-point-analyzer.agent.md
│   │   ├── call-tracer.agent.md
│   │   ├── branch-and-error-mapper.agent.md
│   │   ├── external-service-enricher.agent.md
│   │   └── mermaid-formatter.agent.md
│   ├── prompts/
│   └── README.md
│
└── pr-agents/                      # Pull request management
    ├── agents/
    │   ├── pr-controller.agent.md (controller)
    │   ├── pr-triage.agent.md
    │   ├── pr-change-analyzer.agent.md
    │   ├── pr-report-writer.agent.md
    │   └── azure-devops-mcp-caller.agent.md
    ├── config/                     # PR agent configuration
    └── README.md (implies)
```

---

## 🧑‍💼 Team Agents System

### Overview
A **role-based collaboration framework** designed for complex software development tasks. It includes 15 specialized roles that interact through defined best practices and escalation paths.

### Roles Roster
| Role | Focus | Primary Collaborators |
|------|-------|----------------------|
| **Team Lead** | Ownership, timing, final decisions | Product, Architect, TPM |
| **Product Strategist** | Value, scope, boundaries | Team Lead, Architect |
| **Technical Program Manager** | Sequencing, dependencies, coordination | Team Lead, Architect, DevOps |
| **Architect** | Design, technical shape, APIs | Backend, Frontend, Data, Security, DevOps |
| **Backend Engineer** | API, business logic, data integration | Architect, QA, Security, Data, DevOps |
| **Frontend Engineer** | UX, client behavior, accessibility | Product, Architect, QA, Security |
| **QA Engineer** | Test coverage, release readiness | Engineers, Team Lead |
| **SDET** | Regression automation, reliability | Engineers, QA, Team Lead |
| **Data Engineer** | Pipelines, transforms, contracts | Architect, Backend, Data Analyst |
| **Data Analyst** | Reporting, evidence, metrics | Product, Data Engineer, Team Lead |
| **DevOps Engineer** | Infrastructure, release safety, operations | Architect, Security, Team Lead |
| **Security Engineer** | Trust boundaries, secrets, compliance | Architect, DevOps, Team Lead |
| **AI Systems & Environment Engineer** | AI integration, runtime stability | Architect, Product, DevOps, QA, Security |
| **Debugging Specialist** | Root-cause analysis, incident resolution | Team Lead, affected engineers, QA |
| **Reporting Analyst / Technical Writer** | Documentation, knowledge sharing | Product, Architect, Team Lead, TPM |

### Key Documents
- **[Interaction Matrix](.github/team-agents/docs/matrix.md)** — RACI assignments and escalation paths
- **[Best Practices](.github/team-agents/docs/matrix.md#2-best-interaction-paths-between-roles)** — Who should talk to whom and why
- **[Workflow Templates](.github/team-agents/templates/)** — Task entry points (default, high-level, refactor, debug)

### When to Use
- **Feature development** — Product definition → Architecture → Parallel implementation
- **Architecture reviews** — Multi-perspective debate with full role engagement
- **Refactoring** — Design + implementation collaboration
- **Release readiness** — Final cross-role verification
- **Incident investigation** — Structured root-cause analysis

### Configuration
Agents respect three control parameters:
- **`TEAM_MODE`**: `controller` (single voice) or `multi` (explicit debate)
- **`TEAM_SHAPE`**: `dev`, `debug`, `architecture`, `release`, `ai-workflow`
- **`TEAM_INTENSITY`**: How strictly roles challenge decisions

---

## 🔄 Flow Agents System

### Overview
A **controller-based system** for analyzing and visualizing code execution paths. Designed for debugging, documentation, and knowledge transfer.

### Architecture
- **Controller**: Flow Organizer (entry point, orchestration, output)
- **Subagents** (non-user-invocable):
  - Entry Point Analyzer
  - Call Tracer
  - Branch & Error Mapper
  - External Service Enricher
  - Mermaid Formatter & Validator

### Capabilities
| Feature | Description |
|---------|-------------|
| **Entry Point Detection** | Identifies functions, APIs, Azure Functions as trace origins |
| **Call Graph Tracing** | Follows downstream calls with parameter passing and return values |
| **Control Flow Mapping** | Captures conditionals, loops, error paths, retries |
| **External Service Labeling** | Marks Azure services, APIs, databases, message queues |
| **Mermaid Diagram Generation** | Produces publication-ready flowcharts and sequence diagrams |

### When to Use
- **Debugging complex flows** — Understand what actually executes
- **API documentation** — Generate flow diagrams from code
- **Onboarding** — Visual explanation of critical paths
- **Architecture** — Audit data and service dependencies
- **Azure pipelines** — Trace function chaining and integration patterns

### Configuration Parameters
```
entry_point:       The starting function/API/Azure Function
diagram_type:      sequence | flowchart | deployment | dependency
scope:             local | service | cross-service
include_diagnostics: false | error-only | full
format:            mermaid | text
```

### Example
**Input**: `entry_point: EmployeeSyncFunction.Run`  
**Output**: Mermaid diagram showing call chain → database writes → queue publishes

---

## 📦 PR Agents System

### Overview
A **specialized team** for pull request lifecycle management, with tight Azure DevOps integration.

### Agents
| Agent | Role | Key Functions |
|-------|------|---------------|
| **PR Controller** | Orchestrator | Routes work to specialists, consolidates output |
| **PR Triage** | Initial screening | Scope, author, status, quick health check |
| **PR Change Analyzer** | Deep dive | File-level analysis, impact assessment, risk flags |
| **PR Report Writer** | Synthesis | Generates summaries, recommendations, decision aids |
| **Azure DevOps MCP Caller** | Integration | Links to work items, pull requests, build data |

### Capabilities
- **PR triage** — Quick classification (new, review-ready, blocked, merged)
- **Change analysis** — File, line, and diff-level impact reporting
- **Risk detection** — Large changes, high-risk patterns, compliance gaps
- **Azure DevOps linking** — Associate PRs with work items, builds, commits
- **Report generation** — Markdown summaries for team communication

### When to Use
- **Code review workflows** — Structured PR analysis
- **Release coordination** — Track PR status across teams
- **Compliance auditing** — Screen PRs for risk patterns
- **Knowledge transfer** — Automated change documentation
- **DevOps pipelines** — Integrate PR decisions with CI/CD

### Configuration
```
repos:        List of targeted repositories
teams:        Azure DevOps teams to liaison with
risk_gates:   Which patterns should trigger escalation
report_style: detailed | summary | checklist
```

---

## 📚 Documentation

### Team Agents
- [Interaction Matrix](.github/team-agents/docs/matrix.md) — Complete RACI and escalation paths
- [Role Responsibilities](.github/team-agents/agents/) — Individual role prompts

### Flow Agents
- [System Overview](.github/flow-agents/README.md) — Architecture and use cases
- [Agent Definitions](.github/flow-agents/agents/) — Controller and subagent prompts

### PR Agents
- [PR Agent Design](.github/pr-agents/config) — Configuration schema
- [Agent Implementations](.github/pr-agents/agents/) — Agent prompt files

---

## 🔧 Advanced Setup

### Syncing to Multiple Workstations
If you work across multiple machines, use one of these approaches:

**Option A: Git** (Recommended for teams)
```powershell
# Clone to a shared or synced location
git clone https://github.com/your-org/SubAgentTests.git
# Then use the batch script above to copy to roaming profile
```

**Option B: OneDrive / Dropbox**
```powershell
# Keep source in your cloud-synced folder
$cloudPath = "$env:OneDrive\code-tools\SubAgentTests"
# Copy latest agents to roaming profile
```

**Option C: GitHub Codespaces**
Agents work in dev containers — just ensure the `.github/` folder is present.

### Custom Extensions
To add your own agents:

1. Create a new `.agent.md` file in `.github/your-team/agents/`
2. Follow the YAML frontmatter pattern from existing agents
3. Add role name, scope, and task description
4. Copy to roaming profile agents folder
5. Reload VS Code

Template:
```markdown
---
model: gpt-4o
system_role: Your Role Name
user_invocable: true
agents: []
---

# Your Agent Name

Your agent instructions and capabilities here.
```

---

## 🎯 Usage Examples

### Team Agents
```
Prompt (in VS Code Chat):
"Use the Architecture team to review the design of a new caching layer"

→ Architecture → Backend → Frontend → Data → DevOps
   (validate design) → (note impacts) → (UX fit) → (storage) → (ops)
```

### Flow Agents
```
Prompt:
"Trace the execution for the EmployeeSyncFunction, including error handling and Azure Service Bus publishing"

→ Flow Organizer → Entry Point Analyzer
   → Call Tracer → Branch Mapper
   → External Service Enricher → Mermaid Formatter
→ Outputs: Sequence diagram + call list + risk notes
```

### PR Agents
```
Prompt:
"Analyze PR #1234 for impact and compliance risks"

→ PR Controller → PR Triage (classify)
   → PR Change Analyzer (deep analysis)
   → Azure DevOps MCP Caller (fetch context)
   → PR Report Writer (synthesize)
→ Outputs: Structured review, linked work items, risk summary
```

---

## 🛠️ Troubleshooting

### Agents Not Showing in VS Code
1. Verify files are in: `C:\Users\<YourUsername>\AppData\Roaming\Code\User\agents`
2. Check file extensions are `.agent.md` (not `.md` or `.txt`)
3. Reload VS Code (`Ctrl+Shift+P` → "Developer: Reload Window")
4. Check VS Code version is latest (agents require Copilot Chat 0.20+)

### Agent Not Activating
1. Check YAML frontmatter syntax (use VS Code YAML extension for validation)
2. Verify `user_invocable: true` is set (for controller agents)
3. Confirm agent references subagents correctly
4. Test in a fresh VS Code window

### Sync Issues
1. If using Settings Sync, wait 30 seconds for cloud sync to complete
2. Manually verify files exist in roaming profile
3. Check file permissions: agents folder should be user-writable
4. On Linux/Mac: `~/.config/Code/User/agents` (same structure)

---

## 📋 System Requirements

- **VS Code**: 1.85+
- **GitHub Copilot Chat**: 0.20+
- **Git**: For cloning this repository
- **PowerShell**: 5.0+ (for batch installation)

---

## 📞 Support & Contribution

Issues, questions, or improvements? Please contribute back to this repository.

---

## 📄 License

[Add your license here]
