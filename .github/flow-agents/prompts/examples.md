Generate a call flow diagram for:
src/hr/employee_sync.cs:42

Use default settings.

Map the call flow for function:
syncEmployee

Keep it concise and limit depth to 5.

Generate a sequence diagram for this endpoint:
/api/hr/employees POST

Include external services and show request/response flow.

Trace the call flow starting from this Azure Function:
EmployeeSyncFunction.Run

Include:
- external services
- retries
- error paths

Limit depth to 6.
Use emoji icons.

I want to understand what happens in this flow:

src/services/syncService.ts:handleSync

Focus on:
- error paths
- retries
- conditional branches

Keep the diagram readable even if some detail is collapsed.

Generate a flowchart for:
validateEmployeeRequest

Focus on decision points and alternate paths rather than sequence.

Map the call flow for:
processPayrollBatch

Emphasize:
- external APIs
- database interactions
- queues

Use simple labels instead of emoji.

Generate a call flow diagram for:
getEmployeeById

Keep it minimal:
- no icons
- collapse minor branches
- depth 3

Regenerate the flow diagram from this file:
docs/flows/hr-employee-sync-call-flow.md

Keep the same settings but refresh based on latest code.

Regenerate the flow diagram from:
docs/flows/hr-employee-sync-call-flow.md

Changes:
- increase depth to 7
- include more detailed error paths
- switch to emoji icons

Generate a call flow for:
getActivePullRequests

Include:
- Azure DevOps interactions
- API calls
- data transformations

Make external systems very clear.

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

Generate call flow for selected code.

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