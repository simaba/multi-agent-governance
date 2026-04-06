# Multi-Agent Governance Framework

[![NIST AI RMF](https://img.shields.io/badge/NIST%20AI%20RMF-Aligned-0055A4?style=flat-square)](https://airc.nist.gov/home)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](LICENSE)
[![Discussions](https://img.shields.io/badge/Discussions-Join-7289da?style=flat-square&logo=github)](https://github.com/simaba/multi-agent-governance-framework/discussions)

A governance framework for multi-agent AI systems — covering oversight, accountability,
inter-agent trust, and risk management for systems where multiple AI agents collaborate
or compete to complete tasks.

---

## Why Multi-Agent Systems Need Dedicated Governance

Single-agent AI systems are complex. Multi-agent systems compound that complexity:

- **Emergent behavior** — agents interacting produce outcomes no single agent was designed for
- **Diffuse accountability** — when multiple agents contribute to a decision, who is responsible?
- **Trust propagation** — an agent that trusts a compromised agent can become an attack vector
- **Cascading failures** — a single agent's failure can propagate through the entire pipeline
- **Opaque reasoning** — chains of agent-to-agent communication are harder to audit than single-model decisions
- **Goal misalignment** — individual agent objectives can conflict with system-level objectives

---

## Framework Components

### 1. Agent Classification

Before deploying a multi-agent system, classify each agent:

| Dimension | Categories |
|---|---|
| **Role** | Orchestrator / Executor / Validator / Monitor |
| **Trust Level** | Trusted / Semi-trusted / Untrusted (for external agents) |
| **Autonomy Level** | Supervised / Semi-autonomous / Fully autonomous |
| **Risk Class** | High / Medium / Low (based on possible impact of failure) |
| **Data Access** | Read-only / Read-write / No access |

### 2. Inter-Agent Trust Model

```
┌─────────────────────────────────────────────────────────┐
│                    ORCHESTRATOR                          │
│              (high trust, human-supervised)              │
└──────────────────────┬──────────────────────────────────┘
                       │ delegates tasks + validates outputs
           ┌───────────┼───────────┐
           ▼           ▼           ▼
    ┌──────────┐ ┌──────────┐ ┌──────────┐
    │ AGENT A  │ │ AGENT B  │ │ AGENT C  │
    │(executor)│ │(executor)│ │(validator│
    │semi-trust│ │semi-trust│ │high-trust│
    └──────────┘ └──────────┘ └──────────┘
           │                       │
           ▼                       ▼
    ┌──────────┐             ┌──────────┐
    │EXTERNAL  │             │ HUMAN    │
    │  TOOL    │             │ REVIEW   │
    │(untrusted│             │(required │
    │ sandbox) │             │for high  │
    └──────────┘             │  risk)   │
                             └──────────┘
```

### 3. Governance Gates for Multi-Agent Systems

| Gate | Timing | Requirements |
|---|---|---|
| **System Design Review** | Before development | Agent roles, trust model, and failure modes documented |
| **Individual Agent Validation** | Before integration | Each agent validated independently |
| **Integration Testing** | Before staging | End-to-end scenarios including failure injection |
| **Red Team** | Before production | Adversarial scenarios: prompt injection, agent hijacking, goal manipulation |
| **Human Oversight Check** | Before production | Human review points defined for all high-risk decision paths |
| **Monitoring Activation** | At deployment | Per-agent and system-level monitoring configured |

### 4. Accountability Framework

For every multi-agent system, document:

- **System Owner** — the person accountable for the system's overall behavior
- **Agent Ownership Map** — named owner for each agent in the system
- **Decision Attribution** — how to trace a system output to the contributing agents
- **Failure Responsibility** — who is notified and responsible when which agent fails
- **Audit Trail Requirements** — what gets logged, at which agent, for how long

### 5. Monitoring Requirements

| Metric | Frequency | Alerting Threshold |
|---|---|---|
| Task completion rate | Real-time | Drop > 10% from baseline |
| Inter-agent latency | Real-time | P99 > configured SLA |
| Agent error rate | Real-time | Error rate > 1% |
| Goal drift (planned vs. actual) | Per task | Configurable by use case |
| Token usage / cost | Hourly | > 150% of daily budget |
| Human escalation rate | Daily | > 20% increase week-over-week |

---

## NIST AI RMF Alignment

Full mapping: [docs/nist-rmf-mapping.md](docs/nist-rmf-mapping.md)

Key NIST AI RMF categories addressed:
- **GV.4** — Human oversight for high-autonomy agent decisions
- **MP.3** — Risk categorization specific to multi-agent emergent behavior
- **MS.2** — Ongoing monitoring of per-agent and system-level metrics
- **MG.4** — Rollback and recovery procedures for individual agents and full systems

---

## Ecosystem

| Repository | Purpose |
|---|---|
| [agent-system-simulator](https://github.com/simaba/agent-system-simulator) | Simulate and evaluate multi-agent system behavior |
| [multi-agent-orchestration-patterns](https://github.com/simaba/multi-agent-orchestration-patterns) | Orchestration design patterns for multi-agent pipelines |
| [ai-agent-evaluation-framework](https://github.com/simaba/ai-agent-evaluation-framework) | Evaluation metrics and benchmarks for AI agents |
| [enterprise-ai-governance-playbook](https://github.com/simaba/enterprise-ai-governance-playbook) | Organizational governance playbook |
| [nist-ai-rmf-implementation-guide](https://github.com/simaba/nist-ai-rmf-implementation-guide) | NIST AI RMF practitioner guide |

*Maintained by [Sima Bagheri](https://github.com/simaba) · Connect on [LinkedIn](https://www.linkedin.com/in/simaba/)*
