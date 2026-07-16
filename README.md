# Multi-Agent Governance Framework

[![NIST AI RMF](https://img.shields.io/badge/NIST%20AI%20RMF-Informed-0055A4?style=flat-square)](https://airc.nist.gov/home)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](LICENSE)

A practitioner framework for governing systems in which multiple agents, tools, memories, and human principals exchange information or authority.

The repository focuses on the questions that simple “human in the loop” or “trusted agent” labels leave unanswered: what can each component actually do, whose authority is it exercising, how does one agent’s output propagate into another agent’s action, and how can the workflow be contained when evidence or control fails?

## Start here

| Artifact | Use it for |
|---|---|
| [`docs/authority-and-containment.md`](docs/authority-and-containment.md) | describing authority envelopes, propagation controls, containment, and recovery |
| [`docs/nist-rmf-mapping.md`](docs/nist-rmf-mapping.md) | practitioner cross-reference to selected NIST AI RMF concepts |
| [`agent-orchestration`](https://github.com/simaba/agent-orchestration) | control-flow patterns |
| [`agent-eval`](https://github.com/simaba/agent-eval) | evaluation evidence and decision semantics |
| [`agent-simulator`](https://github.com/simaba/agent-simulator) | runnable bounded workflow examples |

## Why a dedicated model is needed

Multi-agent systems can create risk through composition even when each component looks acceptable in isolation.

- **Authority amplification:** a low-impact recommendation can trigger a high-impact tool through another agent.
- **Instruction propagation:** retrieved or generated content may be interpreted as executable direction downstream.
- **Common-mode error:** planner, executor, and validator may share the same model, prompt assumptions, retrieval errors, or policy gaps.
- **Diffuse attribution:** a final action may combine decisions from several agents, tools, memories, and human approvals.
- **State and persistence:** one component can alter memory, configuration, credentials, or future context.
- **Partial execution:** retries and delegation can leave external systems in an uncertain state.
- **Containment complexity:** stopping the orchestrator may not cancel delegated, queued, or already authorized work.

Governance must therefore cover the interaction graph, not only the individual agents.

## Replace “trust tier” with an authority description

A global label such as trusted, semi-trusted, or untrusted is rarely precise enough. Describe each component across these dimensions:

| Dimension | Example distinctions |
|---|---|
| Principal | named user, service account, organization, unknown source |
| Role | planner, router, executor, reviewer, monitor, memory service |
| Data reach | public, tenant-scoped, sensitive fields, cross-tenant, no data |
| Action authority | read, draft, submit, approve, publish, delete, purchase, execute |
| Externality | private/reversible, internally visible, externally visible, financial, physical |
| Delegation | none, allow-listed, recursive, capable of granting new authority |
| Persistence | stateless, session memory, durable memory, configuration or credential write |
| Validation | executable checks, independent review, human authorization, none |
| Isolation | sandbox, network boundary, tenant boundary, direct production access |
| Revocation and recovery | immediate, delayed, partial, irreversible, unknown |

Authority should be enforced by identity, data, and tool controls rather than relying on a prompt to remember its limits.

## Authority envelopes

An authority envelope defines the actions an agent may take under stated conditions.

For every authority-bearing agent, record:

- principal and identity binding;
- allowed data, tools, and action types;
- prohibited actions and data classes;
- argument and destination restrictions;
- confirmation and dual-control requirements;
- rate, cost, time, and delegation limits;
- logging and provenance expectations;
- revocation, cancellation, and recovery mechanisms.

See the worked structure in [`docs/authority-and-containment.md`](docs/authority-and-containment.md).

## Governance the transitions, not only the roles

A controlled workflow separates several transitions:

```text
request
  ↓
propose ──► validate ──► authorize ──► execute ──► verify ──► record
             │              │              │
             └─ reject      └─ defer       └─ contain / recover
```

For each transition, define:

- input schema and provenance;
- accountable owner;
- control or reviewer;
- allowed state change;
- evidence required to continue;
- failure and disagreement behavior;
- timeout and cancellation behavior;
- output record.

A “validator agent” is not automatically independent. Independence can be weakened by common models, prompts, retrieval, context, rubrics, and incentives.

## Propagation controls

When one agent consumes another agent’s output, specify:

- whether the output is data, recommendation, or instruction;
- which fields are untrusted content;
- schema and provenance validation;
- authority that may be exercised based on the output;
- conditions that stop propagation;
- how disagreement and missing evidence are retained;
- whether downstream actions can be traced back to the source run.

No agent should gain authority merely because another agent emitted authoritative-sounding text.

## Human oversight

“Human in the loop” is not a complete control description. Record:

- the decision the human is authorized to make;
- evidence visible at the review point;
- time available for review;
- whether the interface makes refusal or correction practical;
- consequences of approval, rejection, delay, or no response;
- whether automation bias is measured;
- who reviews the quality of human decisions;
- what happens when the human and system disagree.

For high-consequence actions, separate proposal, authorization, and execution so an approval can be independently attributed and revoked where possible.

## Containment and recovery

Every authority-bearing workflow should have a tested response for:

- stopping new work;
- revoking credentials and sessions;
- cancelling queued and delegated actions;
- isolating memory and generated artifacts;
- moving to read-only or draft-only operation;
- identifying completed, partial, and uncertain external actions;
- reversing or compensating for state changes;
- restoring a known-good configuration;
- verifying downstream recovery;
- preserving evidence under privacy and retention controls.

A rollback plan that only restarts the orchestrator is insufficient when delegated work or external actions may continue.

## Monitoring

Do not use fixed percentages as universal alert thresholds. Derive thresholds from the workflow’s authority, service objectives, baseline, and harm model.

Monitor:

| Level | Signals |
|---|---|
| Agent | invalid outputs, tool errors, retries, refusal and escalation reasons |
| Interaction | delegation depth, authority transitions, disagreement, propagation failure |
| Workflow | completion, partial execution, recovery, human intervention |
| Control | denied calls, bypass attempts, confirmation failures, revocation health |
| Outcome | user correction, unauthorized action, incident, harmful external effect |

Interpretation matters. A rising escalation rate can indicate safer caution, degraded capability, workload shift, or a broken dependency.

## Review gates

| Gate | Evidence expected |
|---|---|
| Purpose and authority review | intended use, prohibited use, authority envelopes, principal model |
| Component evaluation | task and failure evidence for each material component |
| Interaction evaluation | propagation, disagreement, common-mode, and cascading-failure scenarios |
| Control verification | identity, permission, confirmation, revocation, and containment tests |
| Operational readiness | monitoring, incident ownership, recovery exercise, change process |
| Decision review | residual risks, conditions, owners, and re-evaluation triggers |

The gate outcome should distinguish blockers, evidence gaps, required actions, conditions, and accepted residual risks rather than returning a vague pass/fail label.

## Governance record

Maintain a versioned record of:

- purpose and prohibited uses;
- system and delegation graph;
- authority envelopes;
- data and tool boundaries;
- model, prompt, memory, tool, and policy versions;
- validation and authorization points;
- containment and recovery evidence;
- evaluation scope and known gaps;
- owners and incident responsibilities;
- residual-risk decisions;
- changes that invalidate prior evidence.

## Maturity and scope

This is a practitioner governance framework, not a formal assurance case, certified control system, or proof that emergent behavior has been fully characterized. Adapt it to the actual authority, externality, jurisdiction, and operational environment.

References to NIST AI RMF are practitioner mappings and should be verified against official material.

## Related repositories

| Repository | Distinct role |
|---|---|
| [`agent-orchestration`](https://github.com/simaba/agent-orchestration) | routing, delegation, validation, and failure-handling patterns |
| [`agent-eval`](https://github.com/simaba/agent-eval) | defensible evaluation design and release-decision semantics |
| [`agent-simulator`](https://github.com/simaba/agent-simulator) | runnable bounded retries, fallback, and escalation |
| [`mcp-agent-risk-checklist`](https://github.com/simaba/mcp-agent-risk-checklist) | tool-server and agent-integration risk review |

---

*Maintained by [Sima Bagheri](https://github.com/simaba).*
