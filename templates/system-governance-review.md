# Multi-Agent System Governance Review

Use this template before integrating or releasing a multi-agent system.

## 1. System Metadata

| Field | Value |
|---|---|
| System name | `[TBD]` |
| Version | `[TBD]` |
| Review date | `[TBD]` |
| System owner | `[TBD]` |
| Business owner | `[TBD]` |
| Environment | `[development / staging / production]` |
| Risk tier | `[low / medium / high]` |

## 2. System Purpose

**Primary objective:** `[TBD]`

**User or business outcome:** `[TBD]`

**Out-of-scope behavior:**

- `[TBD]`

## 3. Agent Inventory

| Agent | Role | Trust level | Autonomy level | Data access | Owner |
|---|---|---|---|---|---|
| `[agent-name]` | `[orchestrator/executor/validator/monitor]` | `[trusted/semi-trusted/untrusted]` | `[supervised/semi-autonomous/fully autonomous]` | `[none/read/read-write]` | `[TBD]` |

## 4. Trust Boundaries

Document where untrusted input, tools, models, or external systems enter the workflow.

| Boundary | Source | Risk | Control |
|---|---|---|---|
| `[TBD]` | `[TBD]` | `[TBD]` | `[TBD]` |

## 5. Human Oversight Points

| Trigger | Required human action | Owner | SLA |
|---|---|---|---|
| `[low confidence]` | `[review / approve / reject]` | `[TBD]` | `[TBD]` |
| `[tool failure]` | `[TBD]` | `[TBD]` | `[TBD]` |
| `[high-risk output]` | `[TBD]` | `[TBD]` | `[TBD]` |

## 6. Failure Modes

| Failure mode | Likelihood | Impact | Detection | Mitigation |
|---|---|---|---|---|
| `[agent produces incorrect output]` | `[low/medium/high]` | `[low/medium/high]` | `[TBD]` | `[TBD]` |
| `[agent-to-agent handoff fails]` | `[TBD]` | `[TBD]` | `[TBD]` | `[TBD]` |
| `[external tool unavailable]` | `[TBD]` | `[TBD]` | `[TBD]` | `[TBD]` |

## 7. Logging and Audit Trail

Minimum required fields:

- task ID
- agent ID
- model or tool version
- input summary
- output summary
- confidence or quality signal
- escalation decision
- timestamp
- human reviewer when applicable

## 8. Release Decision

- [ ] Approved for integration
- [ ] Approved for staging only
- [ ] Not approved

### Required actions before next gate

- `[TBD]`

## 9. Sign-off

| Role | Name | Decision | Date |
|---|---|---|---|
| System owner | `[TBD]` | `[approve/reject]` | `[TBD]` |
| Technical owner | `[TBD]` | `[approve/reject]` | `[TBD]` |
| Governance owner | `[TBD]` | `[approve/reject]` | `[TBD]` |
