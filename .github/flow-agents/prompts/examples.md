# 1. Basic Diagram Flow (default usage)
Generate a call flow diagram for:
src/hr/employee_sync.cs:42

Use default settings.

# 2. Named Function / Method
Map the call flow for function:
syncEmployee

Output mode: diagram
Keep it concise and limit depth to 5.

# 3. API Endpoint Diagram
Generate a sequence diagram for this endpoint:
/api/hr/employees POST

Include external services and show request/response flow.

# 4. Azure Function Diagram
Trace the call flow starting from this Azure Function:
EmployeeSyncFunction.Run

Output mode: diagram
Include:
- external services
- retries
- error paths

Limit depth to 6.
Use emoji icons.

# 5. Debugging-Oriented Combined Output
I want to understand what happens in this flow:

src/services/syncService.ts:handleSync

Output mode: both
Detail level: deep
Focus on:
- error paths
- retries
- conditional branches

Keep the diagram readable even if some detail is collapsed.

# 6. Branch-Heavy Flow (forces flowchart)
Generate a flowchart for:
validateEmployeeRequest

Output mode: diagram
Focus on decision points and alternate paths rather than sequence.

# 7. External Systems Focus
Map the call flow for:
processPayrollBatch

Output mode: diagram
Emphasize:
- external APIs
- database interactions
- queues

Use simple labels instead of emoji.

# 8. Minimal / Clean Diagram
Generate a call flow diagram for:
getEmployeeById

Output mode: diagram
Keep it minimal:
- no icons
- collapse minor branches
- depth 3

# 9. Narrative Walkthrough (normal)
Explain this flow as a step-by-step narrative:
EmployeeSyncFunction.Run

Output mode: narrative
Detail level: normal
Include:
- why major steps exist
- branch notes
- external dependency notes

# 10. Narrative Walkthrough (light)
Give me a concise narrative walkthrough for:
validateEmployeeRequest

Output mode: narrative
Detail level: light
Focus on the main path and major decisions only.

# 11. Narrative Walkthrough (deep)
Create a detailed narrative for:
src/services/syncService.ts:handleSync

Output mode: narrative
Detail level: deep
Include:
- retries and failure handling
- important side effects
- assumptions or uncertainty

# 12. Regenerate Existing Flow Doc
Regenerate the flow documentation from this file:
docs/flows/hr-employee-sync-call-flow.md

Keep the same settings but refresh based on latest code.

# 13. Regenerate With Changes
Regenerate the flow documentation from:
docs/flows/hr-employee-sync-call-flow.md

Changes:
- output_mode: both
- increase depth to 7
- include more detailed error paths
- switch to emoji icons

# 14. DevOps / MCP Style Prompt
Generate a call flow for:
getActivePullRequests

Output mode: both
Include:
- Azure DevOps interactions
- API calls
- data transformations

Make external systems very clear.

# 15. Full Configuration Style (power user prompt)
Generate flow documentation for:
EmployeeSyncFunction.Run

Configuration:
- output_mode: both
- diagram_type: sequence
- detail_level: normal
- max_depth: 6
- include_external: true
- show_branches: true
- show_error_paths: true

visual_config:
- mermaid_icons: emoji

narrative_config:
- include_why: true
- include_branch_notes: true
- include_external_dependencies: true
- include_assumptions: true

Focus on:
- service interactions
- retry behavior
- database writes

# 16. Quick “Right-Click” Style Prompt
Generate flow documentation for selected code.
Output mode: both.

# 17. Default template to reuse
Generate flow documentation for:
{entry_point}

Configuration:
- output_mode: both
- max_depth: 5
- include_external: true

visual_config:
- mermaid_icons: emoji

narrative_config:
- include_why: true
- include_branch_notes: true

Focus on:
- main flow
- key branches
- external systems
- outcome