# Decision Flow

A multi-agent system needs an explicit decision flow so agents do not conflict, duplicate work, or loop without purpose.

## Core flow

1. Planner interprets the task and defines the work structure.
2. Executor performs the required action.
3. Evaluator checks the result.
4. Supervisor decides whether to accept, retry, reroute, or escalate.

## Decision questions

At each stage, the system should know:
- who can continue the flow,
- who can reject an output,
- who can trigger fallback,
- who can stop the workflow.

## Failure mode
Without explicit decision flow, systems tend to drift into repeated retries, vague coordination, and poor debuggability.
