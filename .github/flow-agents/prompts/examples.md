# 1. Basic Call Flow (default usage)
Generate a call flow diagram for:
src/hr/employee_sync.cs:42

Use default settings.

# 2. Named Function / Method
Map the call flow for function:
syncEmployee

Keep it concise and limit depth to 5.

# 3. API Endpoint
Generate a sequence diagram for this endpoint:
/api/hr/employees POST

Include external services and show request/response flow.

# 4. Azure Function
Trace the call flow starting from this Azure Function:
EmployeeSyncFunction.Run

Include:
- external services
- retries
- error paths

Limit depth to 6.
Use emoji icons.

# 5. Debugging-Oriented Flow
I want to understand what happens in this flow:

src/services/syncService.ts:handleSync

Focus on:
- error paths
- retries
- conditional branches

Keep the diagram readable even if some detail is collapsed.

# 6. Branch-Heavy Flow (forces flowchart)
Generate a flowchart for:
validateEmployeeRequest

Focus on decision points and alternate paths rather than sequence.

# 7. External Systems Focus
Map the call flow for:
processPayrollBatch

Emphasize:
- external APIs
- database interactions
- queues

Use simple labels instead of emoji.

# 8. Minimal / Clean Diagram
Generate a call flow diagram for:
getEmployeeById

Keep it minimal:
- no icons
- collapse minor branches
- depth 3

# 9. Regenerate Existing Diagram
Regenerate the flow diagram from this file:
docs/flows/hr-employee-sync-call-flow.md

Keep the same settings but refresh based on latest code.

# 10. Regenerate With Changes
Regenerate the flow diagram from:
docs/flows/hr-employee-sync-call-flow.md

Changes:
- increase depth to 7
- include more detailed error paths
- switch to emoji icons

# 11. DevOps / MCP Style Prompt
Generate a call flow for:
getActivePullRequests

Include:
- Azure DevOps interactions
- API calls
- data transformations

Make external systems very clear.

# 12. Full Configuration Style (power user prompt)
Generate a sequence diagram for:
EmployeeSyncFunction.Run

Configuration:
- max_depth: 6
- include_external: true
- show_branches: true

visual_config:
- mermaid_icons: emoji

Focus on:
- service interactions
- retry behavior
- database writes

# 13. Quick “Right-Click” Style Prompt
Generate call flow for selected code.

# 14. Default template to reuse
Generate a call flow diagram for:
{entry_point}

Configuration:
- max_depth: 5
- include_external: true

visual_config:
- mermaid_icons: emoji

Focus on:
- main flow
- key branches
- external systems