# Call Flow Agent System

## Overview
The Call Flow Agent System is a controller-based architecture that analyzes code execution paths and generates Mermaid diagrams.

It is designed for:
- Debugging complex flows
- Documenting APIs and services
- Understanding Azure/backend pipelines
- Onboarding and knowledge sharing

The system uses a single controller (**Flow Organizer**) and multiple focused subagents.

---

## Architecture

### Controller
**Flow Organizer**
- Entry point for all requests
- Determines diagram type and scope
- Coordinates subagents
- Produces final Markdown + Mermaid output
- Handles regeneration

### Subagents
- Entry Point Analyzer → identifies entry function, participants, first-hop calls
- Call Tracer → follows downstream call graph
- Branch & Error Mapper → extracts conditionals, retries, error paths
- External Service Enricher → labels Azure/APIs/DB/queues
- Mermaid Formatter & Validator → builds and validates final diagram

All subagents include: `user-invocable: false`

---

## Configuration

### Core Settings

#### entry_point
Where tracing begins.

    entry_point: EmployeeSyncFunction.Run

Supports:
- function name
- file + line
- API route
- Azure Function
- selected code

---

#### diagram_type

    diagram_type: auto

Options:
- auto
- sequence
- flowchart
- context

Use:
- `auto` for default controller selection
- `sequence` for call order and request/response flow
- `flowchart` for branching and decision-heavy flows
- `context` for high-level service/system interaction

---

#### max_depth

    max_depth: 5

Guidelines:
- 3 = high-level
- 5 = default
- 6–7 = deep debugging

---

#### include_external

    include_external: true

Includes things like:
- Azure services
- APIs
- SQL
- queues
- storage
- Key Vault
- Azure DevOps

---

#### show_branches

    show_branches: true

Use this when you want meaningful conditionals and alternate paths included.

---

#### show_error_paths

    show_error_paths: true

Use this when you want retries, failures, catch paths, and fallback behavior surfaced.

---

#### collapse_minor_branches

    collapse_minor_branches: true

Use this to keep diagrams readable by summarizing low-value branch detail.

---

#### show_activation_bars

    show_activation_bars: auto

Options:
- auto
- on
- off

Use:
- `auto` for most cases
- `on` when you want explicit nested call visibility
- `off` when diagrams are getting visually busy

---

## Visual Configuration

Example:

    visual_config:
      mermaid_icons: emoji
      show_notes: true
      alias_mode: short

### mermaid_icons
Options:
- `none` → plain labels only
- `emoji` → emoji-prefixed labels like `🔐 Azure Key Vault`
- `simple` → text-prefixed labels like `[KV] Azure Key Vault`
- `extended` → richer labels, notes, and alias hints

### show_notes
Controls whether helpful notes are added for:
- external dependencies
- inferred boundaries
- retry behavior
- truncation or collapsed detail

### alias_mode
Options:
- `short`
- `descriptive`

Use:
- `short` for compact repeated participants like `KV`, `SQL`, `ADO`
- `descriptive` for more readable, fuller names

---

## Regeneration

    regenerate: true

When enabled, the generated Markdown file should include metadata that supports rerunning the flow later.

Example:

    <!--
    regenerate: flow-organizer
    entry_point: EmployeeSyncFunction.Run
    diagram: sequence
    max_depth: 5
    include_external: true
    -->

This allows the diagram to be refreshed later against updated code without rebuilding the prompt from scratch.

---

## Example Configurations

### Default

    entry_point: EmployeeSyncFunction.Run
    diagram_type: auto
    max_depth: 5
    include_external: true
    show_branches: true
    show_error_paths: true
    collapse_minor_branches: true
    show_activation_bars: auto
    regenerate: true

    visual_config:
      mermaid_icons: emoji
      show_notes: true
      alias_mode: short

### Minimal

    entry_point: getEmployeeById
    diagram_type: sequence
    max_depth: 3
    include_external: false
    show_branches: false
    collapse_minor_branches: true
    regenerate: true

    visual_config:
      mermaid_icons: none

### Debug

    entry_point: src/services/syncService.ts:handleSync
    diagram_type: auto
    max_depth: 6
    include_external: true
    show_branches: true
    show_error_paths: true
    collapse_minor_branches: false
    show_activation_bars: auto
    regenerate: true

    visual_config:
      mermaid_icons: emoji
      show_notes: true
      alias_mode: short

---

## Example Prompts

### Basic

    Generate a call flow diagram for:
    src/hr/employee_sync.cs:42

### Azure Function

    Trace the call flow starting from:
    EmployeeSyncFunction.Run

    Include external services and error paths.

### Debugging

    Analyze flow for:
    syncService.handleSync

    Focus on retries and failures.

### Regenerate

    Regenerate the flow diagram from:
    docs/flows/hr-employee-sync-call-flow.md

---

## Output

The system produces:
- a Markdown file
- an embedded Mermaid diagram
- regeneration metadata
- validation notes or warnings when needed

---

## Design Principles

- Controller-driven with a single visible entry point
- Subagents stay narrow and specialized
- Prefer readability over exhaustive detail
- Avoid diagram noise
- Preserve regeneration capability
- Keep outputs stable across runs so diffs remain readable

---

## When to Use

Use the Call Flow Agent System when you need to:
- understand a complex logic path
- document an API or Azure pipeline
- debug unexpected behavior
- visualize service interactions
- help onboard another developer

---

## Summary

The Call Flow Agent System provides a structured, repeatable way to turn code into clear visual execution flows.

It helps bridge:
- code → understanding
- logic → visualization
- debugging → documentation