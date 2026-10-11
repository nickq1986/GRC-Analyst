# Document Reference: ISMS-DOC-06-RR
**Classification:** Internal  
**Version:** 1.0  
**Status:** Approved  
**Owner:** Information Security & Compliance  
**Standard:** ISO/IEC 27001:2022 (Clause 6.1.2, 6.1.3) & ISO/IEC 27005:2022

---

# 06 · Information Security Risk Register & Risk Treatment Plan

## Table of Contents

- [Risk Register](#risk-register)
- [Risk Treatment Plan](#risk-treatment-plan)
- [Reference Tables](#reference-tables)
  - [Likelihood Rating](#likelihood-rating)
  - [Business Impact](#business-impact)
  - [Risk Rating Matrix](#risk-rating-matrix)
  - [Risk Categories](#risk-categories)
  - [Status Guidance](#status-guidance)

---

## Risk Register

> **Risk Rating = Likelihood (Probability) × Impact (Business Impact)**

| Risk ID | Risk Description | Risk Category | Likelihood (1–5) | Impact (1–5) | Risk Rating | Mitigation Measures | Risk Owner | Status | Review Date |
|:---:|:---|:---:|:---:|:---:|:---:|:---|:---:|:---:|:---:|
| **R-001** | Risk of leaking patient data and breaking privacy laws because Marketing uses free AI tools with real patient details. | Data Security | 5 | 5 | **25 (Critical)** | **Control:** A.5.8 (Information security in project management) & A.5.10<br><br>Ban free-tier AI tools. Require staff to use only enterprise-licensed AI software with strict data protection terms and signed privacy agreements. | Compliance Manager | In Progress | 2026-10-15 |
| **R-002** | Risk of patients being identified because outside AI vendors keep and use patient data to train their systems. | Data Security | 4 | 4 | **16 (High)** | **Control:** A.5.19 (Information security in supplier relationships) & A.5.20 (Addressing information security within supplier agreements)<br><br>Mandate legal contracts with AI suppliers prohibiting the retention or use of organisational data for model training, with strict requirements to delete data post-processing. | Chief Technology Officer | In Progress | 2026-10-15 |
| **R-003** | Risk of patient data lingering indefinitely or being accessed improperly due to weak storage and deletion controls in AI software. | Compliance | 4 | 4 | **16 (High)** | **Control:** A.8.10 (Information deletion) & A.8.12 (Data leakage prevention)<br><br>Configure automatic data deletion and purging rules within AI software to ensure temporary caches and logs are permanently erased after processing. | IT Manager | In Progress | 2026-10-20 |
| **R-004** | Risk of unauthorised access and former employees keeping system access because AI accounts do not use company login controls (SSO). | Access Control | 3 | 4 | **12 (High)** | **Control:** A.5.15 (Access control), A.5.18 (Access rights), & A.8.5 (Secure authentication)<br><br>Enforce Enterprise Single Sign-On (SSO) with Multi-Factor Authentication (MFA) so user access is centrally managed and immediately revoked upon offboarding. | IT Manager | In Progress | 2026-10-20 |
| **R-005** | Risk of patient medical details reaching the wrong person due to outdated, shared, or unverified contact information. | Data Security | 3 | 3 | **9 (Medium)** | **Control:** A.8.11 (Data masking) & A.8.24 (Use of cryptography / Secure messaging)<br><br>Sanitize and genericize automated messages to exclude sensitive details, while enforcing routine contact validation before sending notifications. | Customer Success Lead | Monitored | 2026-11-01 |
| **R-006** | Risk of privacy breaches and legal penalties because messaging tools lack required vendor contracts (BAAs) and security controls. | Compliance | 2 | 4 | **8 (Medium)** | **Control:** A.5.21 (Managing information security in the ICT supply chain) & A.5.31 (Legal, statutory, regulatory and contractual requirements)<br><br>Halt messaging operations until legal and compliance teams formally verify security controls and execute required Business Associate Agreements (BAAs). | Compliance Manager | In Progress | 2026-10-15 |

---

## Risk Treatment Plan

| RTP Ref | Risk No. | Department | Risk Owner | Risk Summary | Treatment Measures | Control Reference | Assigned Lead | Target Completion | Actual Completion | Status Update |
|:---:|:---:|:---:|:---:|:---|:---|:---:|:---:|:---:|:---:|:---|
| **RTP-001** | R-001 | Marketing | Compliance Manager | Unapproved free-tier AI assistant usage processing ePHI without BAA or SSO. | Reject policy exception request. Formalize AI Acceptable Use Policy prohibiting unvetted consumer AI tools. | A.5.8, A.5.10 | Compliance Lead | 2026-10-15 | 2026-10-12 | Policy exception request formally denied; AUP updated and communicated. |
| **RTP-002** | R-002 | Engineering | Chief Technology Officer | Third-party vendor data retention and model training on prompt inputs. | Transition to enterprise AI tier (A008) featuring non-training commitments and executed BAA. | A.5.19, A.5.20 | Head of Engineering | 2026-10-30 | Pending | Procurement evaluation for enterprise AI license in progress. |
| **RTP-003** | R-003 | IT Operations | IT Manager | Temporary session caching and unverified retention schedules in AI systems. | Implement automated 24-hour cache purging and technical verification of vendor zero-data-retention APIs. | A.8.10, A.8.12 | Infrastructure Lead | 2026-10-30 | Pending | Vendor API session persistence configuration under technical review. |
| **RTP-004** | R-004 | IT Operations | IT Manager | Lack of centralized authentication (SSO) and access lifecycle governance. | Enforce SAML 2.0 / SSO integration via corporate IdP with mandatory MFA enforcement. | A.5.15, A.8.5 | IAM Engineer | 2026-10-25 | Pending | IdP integration mapped for approved enterprise AI alternative. |
| **RTP-005** | R-005 | Customer Success | Customer Success Lead | Potential notification misdirection to unverified or shared patient destinations. | Redact detailed clinical information from reminders; restrict payload to clinic name and time. | A.8.11, A.8.24 | Product Manager | 2026-11-15 | Pending | Message template audit initiated across messaging channels. |
| **RTP-006** | R-006 | Compliance | Compliance Manager | Downstream delivery platform operating without verified BAA documentation. | Suspend unverified messaging pipelines until BAA execution and SOC 2 Type II review complete. | A.5.21, A.5.31 | Legal Counsel | 2026-10-20 | Pending | Vendor vendor compliance assessment underway. |

---

## Reference Tables

### Likelihood Rating

| Probability | Definition | Rating |
|:---|:---|:---:|
| Very High | The event is almost certain to happen in the near future (e.g., monthly). | 5 |
| High | The event has a strong chance of occurring again within the next few months. | 4 |
| Medium | The event may happen at some point within the next year. | 3 |
| Low | The event is unlikely but could happen in the next few years. | 2 |
| Very Low | The event is highly improbable and may happen only in rare circumstances. | 1 |

---

### Business Impact

| Impact Level | Definition | Scale |
|:---|:---|:---:|
| Severe | Major disruption, extremely costly, affects critical functions, potentially business-threatening. | 5 |
| High | Significant operational damage, costly, but still manageable. | 4 |
| Moderate | Noticeable impact on operations with moderate costs and delays. | 3 |
| Low | Slight operational disruption, small financial cost, easily managed. | 2 |
| Minimal | Little to no impact on operations, negligible financial or resource costs. | 1 |

---

### Risk Rating Matrix

> **Risk Rating = Likelihood (Probability) × Impact (Business Impact)**

| Probability | Definition | Percentage | Scale |
|:---|:---|:---:|:---:|
| Almost Certain | Expected to occur frequently (monthly or more) | ≥75% | 5 |
| Likely | Likely to occur several times a year | 50%–75% | 4 |
| Moderate | May occur at some point within the next year | 25%–50% | 3 |
| Unlikely | Rare, may occur every few years (3+ years) | 10%–25% | 2 |
| Rare | Extremely unlikely, may occur once in 5+ years | <10% | 1 |

**Suggested thresholds:**

| Rating | Severity | Action Required |
|:---:|:---|:---|
| **20–25** | Critical | Unacceptable risk level. Mandatory executive escalation and immediate mitigation. |
| **12–19** | High | Exceeds risk appetite. Formal mitigation plan and risk owner sign-off required. |
| **6–11** | Medium | Evaluate risk treatment; implement control improvements where cost-effective. |
| **1–5** | Low | Acceptable within risk appetite. Monitor during periodic risk reviews. |

---

### Risk Categories

| Risk Category | Weighting |
|:---|:---:|
| Data Security | 90% |
| Third-Party / Vendor Risk | 4% |
| Physical Security | 2% |
| Compliance | 1% |
| Access Control | 1% |
| Network Security | 1% |
| Operational | 1% |

---

### Status Guidance

| Status | Notes |
|:---|:---|
| Pending | Risk identified, but no action taken yet. Needs attention. |
| In Progress | Risk is currently being mitigated. Regular updates required. |
| Mitigated | Risk has been addressed, but periodic review is still necessary. |
| Monitored | Risk is under observation. No immediate action required but keep an eye on it. |
| Closed | Risk fully resolved or no longer relevant. Can be archived for future reference. |
