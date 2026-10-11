# Document Reference: ISMS-DOC-05-VM
**Classification:** Internal  
**Version:** 1.0  
**Status:** Approved  
**Owner:** Information Security & Compliance  
**Standard:** ISO/IEC 27001:2022 (Clause 6.1.2.c) & ISO/IEC 27005:2022

---

# 05 · Vulnerability-to-Threat Mapping & Risk Statement Register

## 1. Scope & Objective (ISO/IEC 27001 Clause 6.1.2.c)

This document formalizes the risk identification methodology by evaluating the structural relationship between identified asset vulnerabilities, mapped LINDDUN privacy threat scenarios, and consolidated risk statements. 

In accordance with ISO/IEC 27005 guidelines, individual vulnerabilities and granular threat vectors are aggregated into five core Risk Identifiers (**R-001** through **R-005**) for downstream qualitative scoring and treatment planning in the Risk Register.

---

## 2. Risk Identification Methodology

### Vulnerability-to-Threat Mapping

| Vulnerability | Mapped LINDDUN threats | Threat descriptions | Risk statement | Risk-ID |
| --- | --- | --- | --- | --- |
| **A005 — Free-tier AI writing assistant** | T01 Linkability; T02 Identifiability; T03 Disclosure; T04 Non-compliance | **T01:** Repeated prompts may be linked into a patient profile.<br>**T02:** Prompt attributes may identify the patient.<br>**T03:** Identifiable ePHI is disclosed to the free-tier vendor.<br>**T04:** Processing may conflict with policy or privacy obligations. | If Marketing uses the free tier with identifiable appointment data, ePHI could be disclosed to the vendor and retained or used for model improvement without Northwind’s approved safeguards, potentially exposing patient-care relationships and causing policy or privacy non-compliance. | R-001 |
| **A006 — AI data improvement process** | T01 Linkability; T10 Linkability; T11 Identifiability; T12 Non-repudiation; T13 Detectability; T14 Disclosure | **T01:** Repeated prompts may be linked into a patient profile.<br>**T10:** Training data may link prompts across appointments.<br>**T11:** Stored prompts may retain patient identifiers.<br>**T12:** Retained prompts may evidence an appointment.<br>**T13:** Vendor data or model behavior may reveal patient-data inclusion.<br>**T14:** Retained ePHI may be exposed from vendor storage. | If the vendor retains ePHI for model improvement, data from multiple appointments could be linked or inferred in vendor-controlled storage or models, increasing the chance of identifying patients or exposing their care information outside Northwind’s control. | R-002 |
| **A007 — AI database software/cache** | T11 Identifiability; T12 Non-repudiation; T14 Disclosure | **T11:** Cached prompts may retain patient identifiers.<br>**T12:** Retained cache or session records may evidence an appointment.<br>**T14:** Cached ePHI may be exposed if safeguards are inadequate. | If cached ePHI lacks effective access, protection, retention, or deletion safeguards, identifiers and appointment details could persist and be exposed. The register does not establish whether these safeguards are absent, so this risk requires validation. | R-003 |
| **A009 — Message delivery platform** | T05 Linkability; T06 Identifiability; T07 Non-repudiation; T09 Disclosure; T16 Disclosure; T17 Non-compliance | **T05:** Repeated reminders or metadata may reveal a care pattern.<br>**T06:** Reminder content or records may identify the patient and care context.<br>**T07:** Delivery records may evidence a care relationship.<br>**T09:** ePHI may reach a shared or incorrect destination.<br>**T16:** The platform’s ePHI safeguards are not established.<br>**T17:** Whether a BAA is required remains unresolved. | If the delivery platform lacks appropriate safeguards, or a required BAA is absent, reminder content, metadata, or delivery records could reveal patient-care information to others and create privacy or contractual non-compliance. The platform’s role and BAA applicability need confirmation. | R-004 |
| **A010 — Patient delivery destinations** | T05 Linkability; T06 Identifiability; T07 Non-repudiation; T08 Detectability; T09 Disclosure | **T05:** Repeated reminders may reveal a care pattern.<br>**T06:** Reminder content may identify the patient and care context.<br>**T07:** Delivery records may evidence a care relationship.<br>**T08:** A notification may reveal clinic involvement.<br>**T09:** A shared or incorrect destination may receive ePHI. | If a destination is shared, outdated, or incorrect, or a notification is visible to others, reminders or delivery metadata could reveal a patient’s identity and care relationship to an unintended recipient. Destination ownership and safeguards are unspecified. | R-005 |

---

## 3. Risk Statement Synthesis Rules

To maintain consistency with ISO/IEC 27001 documentation standards, each consolidated risk statement incorporates three mandatory elements:

1. **Condition / Cause:** The technical vulnerability or administrative gap present in the baseline system (e.g., *Free-tier usage lacking a signed BAA*).
2. **Event / Threat:** The specific failure mechanism or unauthorized action (e.g., *Disclosure and model ingestion of identifiable patient data*).
3. **Consequence / Impact:** The business, legal, or privacy outcome (e.g., *HIPAA non-compliance, statutory fines, or loss of patient privacy*).
