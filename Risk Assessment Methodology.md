# Document Reference: ISMS-DOC-02-RM
**Classification:** Internal  
**Version:** 1.0  
**Status:** Approved  
**Owner:** Information Security & Compliance  
**Standard:** ISO/IEC 27001:2022 (Clause 6.1.2) & ISO/IEC 27005:2022

---

# 02 · Risk Assessment Methodology & Identification Framework

## 1. Information Security Risk Criteria (ISO/IEC 27001 Clause 6.1.2.a)

To ensure consistent, valid, and comparable risk assessment results across repeated executions, Northwind Health evaluates information security risks using standardized likelihood and impact parameters.

### 1.1 Likelihood Scale
| Value | Rating | Definition |
| :---: | :--- | :--- |
| **1** | Negligible | Unlikely to occur; possible only under exceptional circumstances. |
| **2** | Unlikely | Low probability; not expected to occur under standard operating conditions. |
| **3** | Possible | Moderate probability; may occur at some point during routine operations. |
| **4** | High | High probability; expected to occur in most operational circumstances. |
| **5** | Very High | Almost certain; continuous or frequent occurrence anticipated. |

### 1.2 Impact Scale
| Value | Rating | Operational Definition |
| :---: | :--- | :--- |
| **1** | Negligible | Minimal operational disruption; minor localized impact requiring routine remediation. |
| **2** | Low | Slight disruption; minor financial loss, minimal data exposure, brief operational delays. |
| **3** | Medium | Moderate operational disruption; customer dissatisfaction, noticeable financial impact, minor contractual non-compliance. |
| **4** | High | Significant disruption; statutory/regulatory non-compliance, severe financial loss, major brand damage. |
| **5** | Critical | Existential impact; severe operational shutdown, substantial regulatory fines, compromise of core systems, catastrophic loss. |

---

## 2. Risk Calculation & Acceptance Thresholds (ISO/IEC 27001 Clause 6.1.2.b)

### 2.1 Risk Formula
Overall risk levels are derived using a qualitative $5 \times 5$ matrix based on the standard formulation:

$$\text{Risk Rating} = \text{Likelihood} \times \text{Impact}$$

### 2.2 Risk Acceptance Criteria
* **Low Risk (1–5):** Within organizational risk appetite. Acceptable without mandatory treatment.
* **Medium Risk (6–12):** Exceeds baseline risk appetite. Risk owner must evaluate; treatment required where standard controls are feasible.
* **High / Critical Risk (13–25):** Strictly exceeds organizational risk appetite. Mandatory risk treatment, executive escalation, and immediate control implementation required.

### 2.3 Baseline Assessment Conditions
A formal risk assessment must be executed prior to granting authorization for policy exceptions, under the baseline condition: *"Prior to major system changes, deployments, policy exception approvals, or architectural alterations."*

### 2.4 Evidence-Based Assessment Rules
* **Mandatory Justification:** Every assigned Likelihood and Impact score must be accompanied by documented rationale.
* **Recorded Assumptions:** Assumptions regarding technical boundaries, vendor configurations, or baseline controls must be explicitly documented in the Risk Register.

---

## 3. Risk Identification & Asset Analysis (ISO/IEC 27001 Clause 6.1.2.c)

Risks are identified by evaluating the intersection of technical vulnerabilities and applicable privacy/security threats across the target asset ecosystem.

$$\text{Risk Scenario} = \text{Vulnerability} + \text{Threat Scenario}$$

### 3.1 Target Asset Architecture & Vulnerability Findings
The policy exception evaluation identified five core asset vulnerabilities within the proposed workflow:

* **V-001 (A005 — Free-Tier AI Writing Assistant):** Authentication operates outside Northwind Identity Provider (no SSO); no Business Associate Agreement (BAA) is executed; vendor terms allow input data to train public models.
* **V-002 (A006 — Vendor Model Improvement Process):** ePHI retained and ingested into model training pipelines without contractual or technical boundaries.
* **V-003 (A007 — AI Local Caching/Storage):** Temporary storage caches ePHI without documented access controls, retention boundaries, or automatic deletion schedules *(Requires Validation)*.
* **V-004 (A009 — Delivery Platform Configuration):** Downstream messaging platform processes notification data; contractual BAA status and ePHI transmission controls unverified *(Requires Validation)*.
* **V-005 (A010 — Patient Delivery Destinations):** Endpoint destinations (phone numbers, email addresses) lack ownership verification and encryption safeguards at rest on recipient devices.

---

### 3.2 Threat Modeling (LINDDUN Privacy & STRIDE Framework)
Threat scenarios mapped against the proposed architecture include:

| Threat ID | Threat Category | Scenario Description |
| :--- | :--- | :--- |
| **T-01** | Linkability | Repeated ePHI prompts enable vendor systems to construct patient profiles. |
| **T-02** | Identifiability | Combination of first name, clinic, and date allows direct patient identification. |
| **T-03** | Disclosure | Unprotected transmission of identifiable ePHI to unauthorized third-party vendor. |
| **T-04** | Non-Compliance | Ingestion of ePHI without a executed BAA violates HIPAA §164.514(b) and internal AUP §4.3. |
| **T-05** | Linkability | Metadata or recurring reminder intervals expose patient care patterns. |
| **T-06** | Identifiability | Unencrypted reminder text on external platforms reveals clinical relationships. |
| **T-07** | Non-Repudiation | Delivery logs establish permanent evidentiary records of medical care. |
| **T-08** | Detectability | External notifications expose patient association with specialized clinics. |
| **T-09** | Disclosure | Misdirected messages deliver ePHI to unauthorized third parties or shared devices. |
| **T-10** | Linkability | Vendor training datasets link individual prompts across multiple appointments. |
| **T-11** | Identifiability | Vendor temporary storage caches persist patient identifiers indefinitely. |
| **T-12** | Non-Repudiation | Retained vendor prompts serve as external records of patient care. |
| **T-13** | Detectability | Model output generation reveals prior ingestion of proprietary patient data. |
| **T-14** | Disclosure | Vendor data breach or unauthorized access exposes cached ePHI storage. |
| **T-15** | Unawareness | Patients remain uninformed that third-party AI vendors process appointment data. |
| **T-16** | Disclosure | Messaging platform infrastructure lacks verified encryption controls. |
| **T-17** | Non-Compliance | Unclear BAA execution status with downstream messaging providers. |

---

## 4. Derived Risk Register Statements

Combining vulnerabilities and mapped threat scenarios yields five core risk statements for formal scoring and prioritization:

### R-001: Public Model Training on Unsanitized ePHI
* **Vulnerability:** V-001 (Free-tier AI assistant lacking BAA and SSO).
* **Mapped Threats:** T-02, T-03, T-04, T-13.
* **Risk Statement:** If Marketing enters identifiable patient details into the free-tier AI assistant, ePHI will be disclosed to an unvetted vendor and ingested into public training models without statutory safeguards, causing an immediate HIPAA breach and regulatory non-compliance.

### R-002: Third-Party Data Retention & Re-identification
* **Vulnerability:** V-002 (Vendor model training pipeline).
* **Mapped Threats:** T-01, T-05, T-10, T-12.
* **Risk Statement:** If the vendor retains ePHI for model training, patient data across multiple appointments could be linked or inferred within vendor-controlled storage, creating permanent external data exposure beyond Northwind's governance boundary.

### R-003: Indefinite Data Persistence in Temporary Caches
* **Vulnerability:** V-003 (Unvalidated AI caching mechanisms).
* **Mapped Threats:** T-11, T-14.
* **Risk Statement:** If vendor local caching mechanisms lack enforced auto-deletion and access restrictions, persistent ePHI records could be exposed during a third-party vendor compromise or unauthorized system access.

### R-004: Unverified Messaging Infrastructure Governance
* **Vulnerability:** V-004 (Delivery platform BAA uncertainty).
* **Mapped Threats:** T-16, T-17.
* **Risk Statement:** If downstream message delivery platforms process appointment metadata without a verified BAA or adequate technical safeguards, transmission records could expose clinical relationship details to unauthorized intermediaries.

### R-005: Message Misdirection to Unintended Recipients
* **Vulnerability:** V-005 (Unverified patient delivery destinations).
* **Mapped Threats:** T-08, T-09, T-15.
* **Risk Statement:** If appointment notifications are transmitted to shared, outdated, or incorrect recipient destinations, private healthcare details will be disclosed to unintended third parties, generating privacy complaints and breach notification obligations.
