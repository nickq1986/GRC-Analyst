# Document Reference: ISMS-DOC-07-ES
**Classification:** Confidential  
**Version:** 1.0  
**Status:** Approved  
**Owner:** Information Security & Compliance  
**Standard:** ISO/IEC 27001:2022 (Clause 9.3, Control A.5.8) & HIPAA Security Rule (§ 164.308)

---

# 07 · Executive Summary & Decision Paper

**To:** Executive Leadership Team, Northwind Health  
**From:** Information Security & Compliance  
**Date:** October 2026  
**Subject:** Information Security Risk Assessment: Policy Exception Request & Key Compliance Findings  

---

## 1. Executive Summary

Northwind Health maintains technical and administrative custody of electronic Protected Health Information (ePHI) for approximately 1.2 million patients across 400 healthcare clinics. A formal security risk assessment was conducted following a policy exception request from the Marketing Department to utilize a third-party free-tier Artificial Intelligence (AI) writing assistant for personalizing patient appointment reminders.

The assessment identified **1 Critical Risk** and **5 High/Medium Risks** spanning HIPAA non-compliance, unmanaged third-party ePHI disclosure, and lack of identity governance. The primary critical vulnerability involves the processing of ePHI within consumer-tier AI software lacking a signed Business Associate Agreement (BAA) and Single Sign-On (SSO) integration.

Remediation of the critical gap requires **zero additional capital expenditure** and can be resolved immediately by formally denying the policy exception for the free tier while approving the controlled onboarding of the enterprise-licensed alternative.

---

## 2. Risk Exposure Analysis

| Risk ID | Risk Scenario | Pre-Mitigation Rating | Primary Regulatory / Operational Impact |
| :---: | :--- | :---: | :--- |
| **R-001** | **Unapproved Third-Party AI Data Processing:** Marketing inputs patient names, dates, and clinic details into a free-tier AI assistant lacking a BAA. | **25 (Critical)** | Direct violation of HIPAA Privacy Rule (§ 164.514) and ISO 27001 Control A.5.10. Mandatory regulatory breach reporting and statutory fines. |
| **R-002** | **Vendor Model Ingestion & Data Retention:** Free-tier terms grant the vendor rights to retain and utilize input prompts for global model training. | **16 (High)** | Irreversible external exposure of patient care relationships; loss of organizational data ownership and boundary control. |
| **R-003** | **Unvalidated Session Caching:** Ephemeral session storage and caching within the AI database software lack verified retention schedules. | **16 (High)** | Non-compliance with ISO 27002 Control A.8.10 (Information Deletion); risk of lingering ePHI in unmanaged storage. |
| **R-004** | **Unmanaged Access & Authentication:** Third-party accounts operate outside Northwind's central Identity Provider (IdP) without SSO/MFA. | **12 (High)** | Inability to enforce centralized access lifecycle controls, immediate deprovisioning, or audit logging (ISO 27001 Control A.5.15). |
| **R-005 / R-006** | **Unverified Messaging Delivery Safeguards:** Downstream reminder channels and endpoints operate without confirmed BAAs or data masking. | **8–9 (Medium)** | Potential misdirection of sensitive medical notifications to shared or unverified recipient endpoints. |

---

## 3. Recommended Remediation Roadmap

| Timeframe | Key Actions | Strategic Objective |
| :--- | :--- | :--- |
| **30-Day Actions** *(Immediate)* | • Formally deny policy exception for free-tier AI assistant (A005).<br>• Issue updated AI Acceptable Use Policy (AUP) to Marketing and staff.<br>• Execute BAA and security verification for downstream messaging platform (A009). | Eliminate immediate HIPAA breach exposure and address active compliance gaps. |
| **90-Day Actions** *(Medium-Term)* | • Procure Enterprise AI licenses (A008) at $30/user/month ($120/month total).<br>• Enforce SAML 2.0 / SSO integration and mandatory MFA via corporate IdP.<br>• Configure automated 24-hour cache purging and zero-data-retention API headers. | Establish enterprise identity governance and technical data retention controls. |
| **180-Day Actions** *(Strategic)* | • Deploy Cloud Access Security Broker (CASB) / DLP rules to block shadow AI.<br>• Establish automated Vendor Risk Assessment (VRA) intake workflows.<br>• Conduct annual ISO 27001 ISMS Management Review and SOC 2 Type II readiness. | Embed automated technical safeguards and maintain continuous audit readiness. |

---

## 4. Key Decisions Required from Leadership

1. **Formal Rejection of Policy Exception:** Approve the formal denial of the policy exception request for the free-tier AI writing assistant to eliminate immediate HIPAA breach liability.
2. **Budget Authorization for Enterprise Tier:** Authorize an operational expenditure of **$120.00/month** ($30/user/month across 4 Marketing staff) to transition to the Enterprise AI Tier (A008), providing a fully compliant, BAA-covered, and SSO-integrated solution.
3. **Endorsement of AI Governance Policy:** Approve the publication of the standalone AI Governance Policy enforcing zero-data-retention requirements across all departmental software procurement.

---

## 5. Post-Remediation Target State

Upon execution of the 30-day and 90-day recommended actions:

* **Residual Risk Reduction:** Critical Risk **R-001** decreases from **25 (Critical)** to **2 (Low)**; High Risks **R-002 through R-004** fall to **Medium/Low**.
* **Compliance Alignment:** Fully aligns Northwind Health with ISO/IEC 27001:2022 Controls A.5.19, A.5.20, A.8.10, and HIPAA Security Rule § 164.308.
* **Audit Readiness:** Satisfies prerequisite vendor management and access control criteria for upcoming SOC 2 Type II audit certifications required by enterprise clinic clients.
