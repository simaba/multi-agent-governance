# Example: Research Assistant System

This example uses a simple four-agent structure:
- planner,
- executor,
- evaluator,
- supervisor.

## Example flow

1. Planner breaks the question into sub-problems.
2. Executor gathers evidence and drafts an answer.
3. Evaluator checks relevance, coherence, and gaps.
4. Supervisor decides whether to accept, retry, or escalate.

## Governance value

This design reduces role confusion, limits uncontrolled looping, and makes the system easier to debug when quality drops.
