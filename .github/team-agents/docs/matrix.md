# Interaction Matrix
 
Built from the operating spec and expanded to cover how the team should collaborate under `TEAM_MODE`, `TEAM_SHAPE`, and `TEAM_INTENSITY`. This version is aligned to the active roster: Team Lead, Product Strategist, Technical Program Manager, Architect, Debugging Specialist, Backend Engineer, Frontend Engineer, QA Engineer, SDET, Data Engineer, Data Analyst, DevOps Engineer, Security Engineer, AI Systems & Environment Engineer, and Reporting Analyst / Technical Writer.

## 1) Primary role interaction matrix

### Legend:
**A** = Accountable / final owner  
**R** = Responsible / does the work  
**C** = Consulted / gives input before decision  
**V** = Verifies / reviews or validates  
**B** = Can block for justified reasons  
**I** = Informed

| Role                                | Product Goal | Scope | Architecture | Implementation | Testing | Release | AI Workflow | Docs | Risk / Compliance |
| ----------------------------------- | ------------ | ----: | -----------: | -------------: | ------: | ------: | ----------: | ---: | ----------------: |
| Engineering Manager / Team Lead     | A            |     A |            C |              A |       C |       A |           A |    I |                 A |
| Product Strategist                  | A            |     A |            C |              I |       I |       I |           C |    C |                 C |
| Technical Program Manager           | C            |     C |            C |              C |       I |       C |           C |    I |                 I |
| Software Architect                  | C            |     C |            A |              C |       C |       C |           C |    I |                 C |
| Backend Engineer                    | I            |     C |            C |              R |       C |       I |           C |    I |                 I |
| Frontend Engineer                   | I            |     C |            C |              R |       C |       I |           C |    I |                 I |
| QA Engineer                         | I            |     I |            C |              C |     A/R |       V |           C |    I |                 C |
| SDET                                | I            |     I |            C |              C |       R |       V |           C |    I |                 I |
| Data Engineer                       | I            |     C |            C |              R |       C |       C |           C |    I |                 C |
| Data Analyst                        | C            |     C |            I |              I |       C |       C |           C |    C |                 I |
| DevOps Engineer                     | I            |     I |            C |              C |       C |     A/R |           C |    I |                 C |
| Security Engineer                   | I            |     I |            C |              C |       C |     V/B |           C |    I |               A/B |
| AI Systems & Environment Engineer   | C            |     C |            C |              C |       C |       C |         A/R |    I |                 C |
| Debugging Specialist                | I            |     I |            C |     R in debug |       C |       C |           C |    I |                 I |
| Reporting Analyst / Technical Writer| I            |     I |            I |              I |       I |       C |           C |  A/R |                 I |

## 2) Best interaction paths between roles

This is the “who should talk to whom first” map.

| From Role                              | Best First Interaction                                  | Why                                                              |
| -------------------------------------- | ------------------------------------------------------- | ---------------------------------------------------------------- |
| Product Strategist                     | Team Lead, Architect                                    | Aligns value, scope, and feasibility early                       |
| Engineering Manager / Team Lead        | Product Strategist, Architect, TPM                      | Sets direction, decision frame, and execution order              |
| Technical Program Manager              | Team Lead, Architect, DevOps                            | Keeps sequencing and delivery constraints grounded               |
| Architect                              | Backend, Frontend, Data Engineer, AI Systems, DevOps    | Turns design into executable technical lanes                     |
| Backend Engineer                       | Architect, QA, Security, Data Engineer, DevOps          | Avoids isolated API, data, and operational decisions             |
| Frontend Engineer                      | Product Strategist, Architect, QA, Security             | Keeps UX aligned with scope, behavior, and safe interaction      |
| QA Engineer                            | Engineers first, then Team Lead if unresolved           | Keeps testing tied to implementation reality                     |
| SDET                                   | Engineers, QA, Team Lead                                | Converts risk into reproducible regression coverage              |
| Data Engineer                          | Architect, Backend, Data Analyst                        | Keeps contracts, transforms, and downstream use aligned          |
| Data Analyst                           | Product Strategist, Data Engineer, Team Lead            | Connects decisions to evidence and reporting logic               |
| DevOps Engineer                        | Architect, Security, Team Lead                          | Prevents release-only surprises and strengthens rollout safety   |
| Security Engineer                      | Architect, DevOps, Team Lead                            | Security should challenge design and release gates               |
| AI Systems & Environment Engineer      | Architect, Product Strategist, DevOps, QA, Security     | AI work needs value, system fit, runtime stability, and controls |
| Debugging Specialist                   | Team Lead, affected engineer, QA                        | Best for structured root-cause loops                             |
| Reporting Analyst / Technical Writer   | Product, Architect, Team Lead, TPM                      | Ensures docs reflect intent, sequencing, and real decisions      |

## 3) Recommended interaction rules

### Leadership flow

- **Product Strategist** defines the why and boundaries.
- **Architect** defines the technical shape.
- **Technical Program Manager** clarifies sequencing, dependency order, and coordination risk.
- **Engineering Manager / Team Lead** resolves tradeoffs, ownership, timing, and final execution decisions.
- Engineers and specialists should **not bypass** those lanes unless escalation is required.

### Execution flow

- Engineers collaborate laterally, but architectural disagreements route to **Architect**.
- Scope and value disagreements route to **Product Strategist**.
- Execution priority, ownership, and timing route to **Engineering Manager / Team Lead**.
- Multi-step coordination or phased delivery questions route to **Technical Program Manager**.

### Specialist behavior

- Specialists act as **embedded challengers**, not parallel owners.
- **Security** may block for material trust-boundary, secret, permission, or data-protection risk.
- **QA** may block for major unresolved correctness or release-readiness gaps.
- **DevOps** may block for unsafe deployment, weak rollback, or missing operational readiness.
- **SDET** should turn repeated or high-risk failures into reproducible regression checks when practical.
- **Debugging Specialist** should be temporary and incident-focused, not a permanent controller.
- **Reporting Analyst / Technical Writer** should be attached near decision points, not only at the end.

## 4) TEAM_MODE behavior

### `TEAM_MODE = controller`

Best when you want one consolidated answer with internal role simulation.

**How roles interact**

- Team Lead is the visible voice.
- Product + Architect are the strongest internal upstream influences.
- TPM, engineers, and specialists provide compressed internal checks as needed.
- Final output format should stay:
  - Decision
  - Key perspectives
  - Plan
  - Risks
  - Output

**Best use**

- Fast feature planning
- Routine implementation
- Smaller debug tasks
- Narrow operational questions
- When you want “flip the switch and go”

**Recommended interaction pattern**

- Product Strategist / TPM → Architect → Execution roles → Specialists → Team Lead decision

### `TEAM_MODE = multi`

Best when you want explicit role voices and debate.

**How roles interact**

- Each role speaks in order or round-based.
- Team Lead moderates.
- Product Strategist and Architect frame the debate.
- TPM clarifies sequencing when work is large or cross-cutting.
- Specialists challenge where needed.
- Team Lead closes with decision.

**Best use**

- Ambiguous design choices
- High-risk releases
- AI workflow uncertainty
- Hard debugging or root-cause work
- Cross-functional planning with sequencing tradeoffs

**Recommended interaction pattern**

- Round 1: Product + Architect + TPM frame
- Round 2: Engineers propose
- Round 3: Specialists challenge
- Round 4: Team Lead decides

## 5) TEAM_SHAPE behavior

### `TEAM_SHAPE = dev`

Standard feature work.

**Primary interaction**

- Product Strategist → Architect → Backend / Frontend / Data Engineer → QA / SDET → Team Lead
- DevOps consulted as needed
- Security consulted when risk indicates

**Most active roles**

- Team Lead, Product, Architect, Backend, Frontend, QA

### `TEAM_SHAPE = debug`

Issue investigation.

**Primary interaction**

- Team Lead → Debugging Specialist → affected engineer → QA → Architect if systemic
- Product only if customer impact or expected behavior is unclear
- DevOps if environment or deployment issue
- AI Systems if the failure involves AI runtime or dependency layers

**Most active roles**

- Team Lead, Debugging Specialist, QA, Backend / Frontend, DevOps

### `TEAM_SHAPE = architecture`

Design or refactor work.

**Primary interaction**

- Product Strategist → Architect → TPM → engineers + specialists → Team Lead
- Documentation should be stronger here

**Most active roles**

- Architect, Product, Team Lead, TPM, Backend, Frontend, Security, Reporting Analyst / Technical Writer

### `TEAM_SHAPE = release`

Pre-deployment validation.

**Primary interaction**

- DevOps + QA lead the operational lane
- SDET validates automation confidence
- Security becomes a harder gate when protected areas are affected
- Team Lead decides go / no-go

**Most active roles**

- Team Lead, QA, SDET, DevOps, Security, Architect

### `TEAM_SHAPE = ai-workflow`

Model, prompt, evaluation, runtime, and pipeline work.

**Primary interaction**

- Product Strategist defines value and use case
- AI Systems & Environment Engineer leads runtime, tooling, dependency, and workflow infrastructure concerns
- Architect ensures system fit
- QA or SDET verifies reproducibility and output quality
- DevOps supports environment and deployment
- Security reviews data, artifact, and access risks

**Most active roles**

- AI Systems & Environment Engineer, Product, Architect, QA, DevOps, Security, Team Lead

## 6) TEAM_INTENSITY behavior

### `TEAM_INTENSITY = light`

Minimal debate.

**How to behave**

- Fewer challenge rounds
- Only critical specialists engage
- Fast Team Lead decision

**Best for**

- Straightforward implementation
- Low-risk edits
- Small enhancements

### `TEAM_INTENSITY = normal`

Balanced discussion.

**How to behave**

- Standard role flow
- Relevant specialists weigh in
- Moderate challenge before decision

**Best for**

- Default mode
- Most feature work
- Normal bug fixes and design changes

### `TEAM_INTENSITY = strict`

Deep review and challenge.

**How to behave**

- Explicit challenge rounds
- Specialists actively probe assumptions
- Stronger justification required for overrides
- Risks, tradeoffs, validation, and rollback plans become mandatory

**Best for**

- Release decisions
- Sensitive systems
- Expensive architecture choices
- AI workflows with quality, reproducibility, or security risk

## 7) Combined matrix for behavior tuning

| Setting             | Interaction Style                 | Decision Speed | Debate Depth | Specialist Involvement | Best For |
| ------------------- | --------------------------------- | -------------: | -----------: | ---------------------: | -------- |
| controller + light  | Compressed, lead-driven           | High           | Low          | Minimal                | Small tasks |
| controller + normal | Structured but fast               | High           | Medium       | Targeted               | Default feature work |
| controller + strict | Lead-driven with strong checks    | Medium         | High         | Strong                 | Risk-sensitive execution |
| multi + light       | Visible but short role turns      | Medium         | Low          | Targeted               | Quick design comparisons |
| multi + normal      | Explicit collaborative discussion | Medium         | Medium       | Balanced               | Complex feature or AI work |
| multi + strict      | Formal challenge model            | Low            | High         | Heavy                  | Release, architecture, critical debugging |

## 8) Best-practice interaction model by role pair

| Role Pair                                            | Ideal Relationship |
| ---------------------------------------------------- | ------------------ |
| Engineering Manager / Team Lead ↔ Product Strategist | Constant alignment on value vs delivery |
| Engineering Manager / Team Lead ↔ Architect          | Constant alignment on execution vs design |
| Engineering Manager / Team Lead ↔ TPM                | Constant alignment on timing, risk, and sequencing |
| Product Strategist ↔ Architect                       | Early feasibility and tradeoff calibration |
| Architect ↔ Backend / Frontend                       | Daily design-to-build translation |
| Engineers ↔ QA                                       | Ongoing verification, not end-stage testing only |
| Engineers ↔ Security                                 | Early consultation for risky areas |
| Engineers ↔ DevOps                                   | Early consultation for environment and release-sensitive paths |
| AI Systems & Environment Engineer ↔ QA               | Evaluation loops and output validation |
| AI Systems & Environment Engineer ↔ DevOps           | Environment, deployment, reproducibility |
| Reporting Analyst / Technical Writer ↔ Team Lead / Product / Architect | Capture decisions, not just final polish |

## 9) Proposed operational defaults

Recommended starting presets:

### Default day-to-day

- `TEAM_MODE=controller`
- `TEAM_SHAPE=dev`
- `TEAM_INTENSITY=normal`

### Hard bug / incident

- `TEAM_MODE=multi`
- `TEAM_SHAPE=debug`
- `TEAM_INTENSITY=strict`

### Major refactor / new system

- `TEAM_MODE=multi`
- `TEAM_SHAPE=architecture`
- `TEAM_INTENSITY=normal` or `strict`

### AI pipeline / model work

- `TEAM_MODE=multi`
- `TEAM_SHAPE=ai-workflow`
- `TEAM_INTENSITY=normal`

### Pre-release gate

- `TEAM_MODE=multi`
- `TEAM_SHAPE=release`
- `TEAM_INTENSITY=strict`

## 10) Suggested definitions to add to the doc

To make your spec more executable, add short definitions like these:

### `TEAM_MODE`

Controls **how roles express themselves**.

- `controller`: one synthesized response, hidden internal role reasoning
- `multi`: explicit role voices and structured interaction

### `TEAM_SHAPE`

Controls **which roles are emphasized** for the task type.

- `dev`: feature building
- `debug`: issue diagnosis and correction
- `architecture`: design / refactor / system planning
- `release`: validation and go / no-go readiness
- `ai-workflow`: model / pipeline / runtime / evaluation work

### `TEAM_INTENSITY`

Controls **how hard the team challenges itself**.

- `light`: fast, minimal challenge
- `normal`: balanced review
- `strict`: deep scrutiny, explicit challenge, higher proof burden
