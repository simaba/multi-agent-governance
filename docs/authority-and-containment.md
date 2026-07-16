# Authority and Containment Model for Multi-Agent Systems

“Trust” is too vague to govern an agent. A component may be reliable on one task, unverified on another, read-only in one workflow, and capable of irreversible external action in another.

Governance should describe the authority granted, the evidence required before outputs propagate, and the mechanisms available to contain or reverse harm.

## Describe each agent by capability

Record at least the following dimensions.

| Dimension | Questions |
|---|---|
| Identity and principal | Which user, service, or organization is the agent acting for? Can that binding be verified? |
| Role | Planner, router, executor, reviewer, monitor, memory service, or other? |
| Data reach | Which stores, fields, tenants, and sensitivity classes can it read? |
| Action authority | Can it draft, submit, approve, modify, delete, publish, purchase, message, or execute code? |
| Externality | Are actions private and reversible, internally visible, externally visible, financial, legal, physical, or safety-relevant? |
| Delegation | Can it invoke other agents or tools? Can delegated authority exceed its own? |
| Persistence | Can it write memory, change configuration, create credentials, or alter future behavior? |
| Validation | Which outputs require deterministic checks, independent review, human confirmation, or no further control? |
| Isolation | What sandbox, network, filesystem, tenant, or execution boundary limits failure? |
| Revocation | How quickly can credentials, tools, sessions, queued work, and persistent state be disabled? |
| Observability | Can actions be attributed to model, prompt, tool, principal, version, and run? |
| Recovery | Can the effect be rolled back, compensated, or reconstructed? |

Avoid one global autonomy or trust label when the authority differs by tool or workflow state.

## Use an authority envelope

An authority envelope is the bounded set of actions the agent may take under defined conditions.

Example:

```yaml
agent: catalog-correction-drafter
principal: authenticated-library-operator
allowed:
  data:
    - public-catalog-records
  tools:
    - search_catalog
    - draft_correction
  actions:
    - read
    - create_draft
prohibited:
  - publish_correction
  - delete_record
  - access_patron_history
conditions:
  - every draft includes source_record_ids
  - publication requires operator confirmation
  - tool calls expire after 15 minutes
containment:
  - revoke service token
  - stop queued drafts
  - quarantine persistent memory
```

The envelope should be enforceable at the identity, tool, and data layers—not merely written in the agent prompt.

## Control propagation between agents

When one agent consumes another agent’s output, define:

- the expected schema and provenance;
- whether the producer is allowed to issue instructions or only data;
- which fields are treated as untrusted content;
- validation and sanitization before use;
- authority that the consumer may exercise based on the output;
- whether disagreement, missing evidence, or invalid structure stops propagation;
- whether the receiving agent can trace the source and version.

A validator agent is not independent merely because it has a different role name. Independence can be weakened by shared model errors, common prompts, common retrieval, shared context, or the same evaluator rubric.

## Separate recommendation from action

Use distinct control states:

1. **propose** — agent produces a draft or recommendation;
2. **validate** — rules or reviewers check structure, evidence, and policy boundaries;
3. **authorize** — an accountable principal grants permission for the action;
4. **execute** — a bounded tool performs the action;
5. **verify** — the system confirms the intended state change and detects partial failure;
6. **record** — provenance and disposition are retained under an approved policy.

Combining authorization and execution inside one opaque agent step makes incident analysis and least-privilege design harder.

## Containment design

For each authority-bearing component, define:

### Preventive boundaries

- scoped credentials and tenant restrictions;
- allow-listed tools and arguments;
- network and filesystem isolation;
- rate, cost, and concurrency limits;
- write confirmation or dual control;
- untrusted-content separation;
- idempotency and replay protection.

### Detection

- unauthorized or out-of-envelope tool attempts;
- abnormal delegation depth or fan-out;
- repeated retries and oscillating plans;
- output or action divergence from validated intent;
- unusual data access, egress, cost, or persistence;
- failure to verify an external state change.

### Response

- stop new work;
- revoke credentials and sessions;
- cancel queued or delegated actions;
- isolate affected memory and artifacts;
- move to a reduced read-only or draft-only mode;
- notify named owners;
- preserve forensic evidence with privacy controls.

### Recovery

- identify completed, partial, and uncertain actions;
- reverse or compensate where possible;
- re-establish a known-good configuration;
- verify downstream state;
- create regression cases for the failure path;
- review whether the authority envelope was too broad.

## Escalation conditions

Escalation should be tied to defined states rather than a generic confidence threshold.

Examples:

- required evidence is absent or contradictory;
- the requested action is outside the authority envelope;
- the action is irreversible or externally consequential;
- a validator and executor disagree;
- repeated attempts produce inconsistent plans;
- a dependency returns an unverifiable or partial result;
- identity or data classification is uncertain;
- the system cannot confirm the final state;
- a control has degraded or been bypassed.

## Monitoring design

Avoid universal alert thresholds. Derive signals from the service contract, baseline, authority, and harm model.

Monitor at several levels:

| Level | Examples |
|---|---|
| Agent | invalid outputs, tool errors, retries, refusal/escalation reasons |
| Interaction | delegation graph, authority transitions, disagreement, propagation failures |
| Workflow | completion, recovery, human intervention, partial state changes |
| Control | denied calls, confirmation bypass attempts, credential/revocation health |
| Outcome | user correction, incident, harmful or unauthorized external effect |

A change in escalation rate may indicate improved caution, worsening capability, changed workload, or a broken dependency. Diagnose the cause before treating the metric as good or bad.

## Governance record

For every deployed multi-agent workflow, retain a versioned record of:

- system purpose and prohibited uses;
- authority envelopes;
- principal and identity model;
- data classification and tool permissions;
- agent and tool versions;
- validation and authorization points;
- containment and recovery procedures;
- evaluation evidence and known gaps;
- owners and on-call responsibilities;
- residual risks and decision conditions;
- change triggers requiring re-evaluation.

This record supports review and incident response. It does not prove that emergent behavior has been fully characterized.
