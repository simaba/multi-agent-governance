# Agent Roles

A multi-agent system should assign each agent a clear role with bounded responsibility.

## Common roles

### Planner
Breaks the task into steps, chooses the sequence of work, and defines handoffs.

### Executor
Performs the primary action for a step such as retrieval, synthesis, transformation, or tool use.

### Evaluator
Checks whether the executor output meets the required standard and whether the system should continue, retry, or escalate.

### Supervisor
Controls the broader flow, enforces stop conditions, and decides when human escalation is required.

## Design rule
No two agents should own the same decision authority unless the redundancy is intentional and explicitly controlled.
