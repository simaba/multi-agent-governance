# Escalation Logic

Escalation logic defines when a multi-agent system stops normal flow and hands control to a stronger control path.

## Trigger examples

- repeated evaluator rejection
- confidence below threshold
- conflicting agent outputs
- tool failure or unavailable dependency
- policy or safety concern

## Escalation options

- retry with constraints
- reroute to fallback agent
- escalate to supervisor agent
- escalate to a human reviewer
- terminate the workflow safely

## Design rule
Escalation thresholds should be explicit, observable, and tied to a real action.
