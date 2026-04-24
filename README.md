# Multi-Agent Governance Framework

[![NIST AI RMF](https://img.shields.io/badge/NIST%20AI%20RMF-Aligned-0055A4?style=flat-square)](https://airc.nist.gov/home)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](LICENSE)
[![Discussions](https://img.shields.io/badge/Discussions-Join-7289da?style=flat-square&logo=github)](https://github.com/simaba/multi-agent-governance/discussions)

A governance framework for multi-agent AI systems, covering oversight, accountability, inter-agent trust, and risk management for systems where multiple AI agents collaborate or compete to complete tasks.

---

## Choose this repo when

Use this repository when you need the **oversight and accountability model** for multi-agent systems:

- who owns the system
- how trust tiers are defined
- where human review is mandatory
- how failure accountability and audit trails are structured
- what monitoring is required at the system level

Do **not** start here if you need control-flow design patterns. Use [`agent-orchestration`](https://github.com/simaba/agent-orchestration).

Do **not** start here if you need evaluation metrics and benchmark scenarios. Use [`agent-eval`](https://github.com/simaba/agent-eval).

Do **not** start here if you want runnable examples. Use [`agent-simulator`](https://github.com/simaba/agent-simulator).

---

## Why multi-agent systems need dedicated governance

Single-agent AI systems are complex. Multi-agent systems compound that complexity:

- **Emergent behavior**: agents interacting can produce outcomes no single agent was designed for
- **Diffuse accountability**: multiple agents can contribute to the same decision path
- **Trust propagation**: a compromised or unreliable agent can influence downstream behavior
- **Cascading failures**: a local failure can propagate through the pipeline
- **Opaque reasoning**: multi-step agent-to-agent flows are harder to audit than single-model decisions
- **Goal misalignment**: local agent objectives can conflict with system-level objectives

---

## Framework components

### 1. Agent classification

Before deploying a multi-agent system, classify each agent:

| Dimension | Categories |
|---|---|
| **Role** | Orchestrator / Executor / Validator / Monitor |
| **Trust Level** | Trusted / Semi-trusted / Untrusted |
| **Autonomy Level** | Supervised / Semi-autonomous / Fully autonomous |
| **Risk Class** | High / Medium / Low |
| **Data Access** | Read-only / Read-write / No access |

### 2. Inter-agent trust model

```text
┌─────────────────────────────────────────────────────────┐
│                    ORCHESTRATOR                         │
│              (high trust, human-supervised)             │
└──────────────────────┬──────────────────────────────────┘
                       │ delegates tasks + validates outputs
           ┌───────────┼───────────┐
           ▼           ▼           ▼
    ┌──────────┐ ┌──────────┐ ┌──────────┐
    │ AGENT A  │ │ AGENT B  │ │ AGENT C  │
    │ executor │ │ executor │ │ validator│
    │semi-trust│ │semi-trust│ │high-trust│
    └──────────┘ └──────────┘ └──────────┘
           │                       │
           ▼                       ▼
    ┌──────────┐             ┌──────────┐
    │EXTERNAL  │             │ HUMAN    │
    │  TOOL    │             │ REVIEW   │
    │untrusted │             │required  │
    │ sandbox  │             │for high  │
    └──────────┘             │  risk    │
                             └──────────┘
```

### 3. Governance gates for multi-agent systems

| Gate | Timing | Requirements |
|---|---|---|
| **System Design Review** | Before development | agent roles, trust model, and failure modes documented |
| **Individual Agent Validation** | Before integration | each agent validated independently |
| **Integration Testing** | Before staging | end-to-end scenarios including failure injection |
| **Red Team** | Before production | adversarial scenarios such as prompt injection and agent hijacking |
| **Human Oversight Check** | Before production | human review points defined for all high-risk decision paths |
| **Monitoring Activation** | At deployment | per-agent and system-level monitoring configured |

### 4. Accountability framework

For every multi-agent system, document:

- **System Owner**: accountable for overall system behavior
- **Agent Ownership Map**: named owner for each agent
- **Decision Attribution**: how outputs are traced to contributing agents
- **Failure Responsibility**: who is notified and who owns remediation
- **Audit Trail Requirements**: what is logged, where, and for how long

### 5. Monitoring requirements

| Metric | Frequency | Alerting Threshold |
|---|---|---|
| Task completion rate | Real-time | drop > 10% from baseline |
| Inter-agent latency | Real-time | P99 > configured SLA |
| Agent error rate | Real-time | error rate > 1% |
| Goal drift (planned vs. actual) | Per task | configurable by use case |
| Token usage / cost | Hourly | > 150% of daily budget |
| Human escalation rate | Daily | > 20% increase week-over-week |

---

## NIST AI RMF alignment

Full mapping: [docs/nist-rmf-mapping.md](docs/nist-rmf-mapping.md)

Key NIST AI RMF categories addressed:

- **GV.4**: human oversight for high-autonomy decisions
- **MP.3**: risk categorization for emergent multi-agent behavior
- **MS.2**: ongoing monitoring of per-agent and system-level metrics
- **MG.4**: rollback and recovery procedures for agents and full systems

---

## Related repositories

| Repository | What it adds |
|---|---|
| [`agent-orchestration`](https://github.com/simaba/agent-orchestration) | routing, delegation, validation, and failure-handling patterns |
| [`agent-eval`](https://github.com/simaba/agent-eval) | evaluation dimensions, scenarios, and reporting structure |
| [`agent-simulator`](https://github.com/simaba/agent-simulator) | runnable behavior and bounded workflow examples |
| [`governance-playbook`](https://github.com/simaba/governance-playbook) | broader enterprise governance operating model |
| [`nist-rmf-guide`](https://github.com/simaba/nist-rmf-guide) | practitioner guide for RMF implementation |

*Maintained by [Sima Bagheri](https://github.com/simaba) · Connect on [LinkedIn](https://www.linkedin.com/in/simaba/)*
