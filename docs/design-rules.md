# Design Rules

## Rule 1: Separate authority from action
The agent that performs an action should not always be the same agent that approves continuation.

## Rule 2: Bound retries
Every retry loop should have an explicit limit and a defined next step after failure.

## Rule 3: Prefer clear handoffs
Agent interactions should use explicit handoff conditions rather than vague chaining.

## Rule 4: Make fallback deliberate
Fallback paths should be designed before launch, not improvised after repeated failure.

## Rule 5: Preserve observability
A multi-agent system should log decisions, reroutes, retries, and escalation events in a reconstructable way.
