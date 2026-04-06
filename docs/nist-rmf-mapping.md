# NIST AI RMF Cross-Reference

This document maps the content in this repository to the corresponding
NIST AI Risk Management Framework (AI RMF 1.0) functions, categories,
and subcategories.

**Full NIST AI RMF implementation guide:** [nist-ai-rmf-implementation-guide](https://github.com/simaba/nist-ai-rmf-implementation-guide)

---

## NIST AI RMF Function Overview

```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│   GOVERN    │ ──► │     MAP     │ ──► │   MEASURE   │ ──► │   MANAGE    │
│             │     │             │     │             │     │             │
│ GV.1–GV.6  │     │ MP.1–MP.5  │     │ MS.1–MS.5  │     │ MG.1–MG.4  │
└─────────────┘     └─────────────┘     └─────────────┘     └─────────────┘
```

---

## How This Repository Implements NIST AI RMF

### GOVERN (GV) — Policies and Accountability

| NIST Subcategory | Implementation in This Repository |
|---|---|
| GV.1.1 — Organizational policies | Governance framework documents serve as organizational policy templates |
| GV.1.3 — Prohibited uses defined | Use case classification includes explicit prohibited patterns |
| GV.4.1 — Human oversight defined | Human-in-the-loop requirements documented per pattern |
| GV.6.1 — AI systems monitored | Monitoring requirements specified per design pattern |

### MAP (MP) — Risk Contextualization

| NIST Subcategory | Implementation in This Repository |
|---|---|
| MP.1.1 — Intended use documented | Each pattern includes intended use scope and limitations |
| MP.2.1 — Scientific basis reviewed | Patterns include evidence of effectiveness and known limitations |
| MP.3.1 — Risk identification | Risk considerations documented per pattern/framework element |
| MP.4.1 — Impact assessment | Stakeholder impact analysis included in high-risk patterns |
| MP.5.1 — Trustworthy AI characteristics | Patterns mapped to NIST's seven trustworthy AI characteristics |

### MEASURE (MS) — Risk Analysis

| NIST Subcategory | Implementation in This Repository |
|---|---|
| MS.1.1 — AI risk identification | Risk categories enumerated with likelihood and impact |
| MS.2.3 — AI system monitoring | Monitoring metrics and alerting thresholds defined |
| MS.3.1 — Evaluation techniques | Evaluation approaches specified per framework element |
| MS.5.1 — Bias evaluation | Fairness and bias considerations documented |

### MANAGE (MG) — Risk Response

| NIST Subcategory | Implementation in This Repository |
|---|---|
| MG.2.1 — Treatments defined | Mitigation strategies specified for each identified risk |
| MG.4.1 — Rollback procedures | Recovery and fallback procedures documented |
| MG.3.2 — Residual risk accepted | Residual risk acknowledgment process defined |

---

## EU AI Act Alignment

For organizations subject to the EU AI Act, see the cross-reference mapping:
[nist-ai-rmf-implementation-guide/docs/eu-ai-act-mapping.md](https://github.com/simaba/nist-ai-rmf-implementation-guide/blob/main/docs/eu-ai-act-mapping.md)

---

## The Seven Characteristics of Trustworthy AI (NIST)

Each component of this repository addresses one or more of these characteristics:

| Characteristic | Addressed By |
|---|---|
| Accountable | Governance framework, role definitions, audit trails |
| Explainable | Documentation requirements, decision logging patterns |
| Interpretable | Output interpretation guidelines, confidence requirements |
| Privacy-Enhanced | Data handling patterns, PII processing guidelines |
| Reliable | Performance monitoring, regression testing requirements |
| Safe | Safety evaluation checklists, failure mode analysis |
| Fair | Bias evaluation requirements, subgroup testing |

---

*Maintained by [Sima Bagheri](https://github.com/simaba) · Not affiliated with NIST.*
*For authoritative guidance, refer to [airc.nist.gov](https://airc.nist.gov)*
