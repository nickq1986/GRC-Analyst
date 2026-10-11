# Document Reference: ISMS-DOC-02-AR
**Classification:** Internal  
**Version:** 1.0  
**Status:** Approved  
**Owner:** Information Security & Compliance  
**Standard:** ISO/IEC 27001:2022 (Clause 5.9, Control A.5.9, A.5.10)

---

# 01.1 · Northwind Health Asset Register

## 1. Context & Governance (ISO/IEC 27001 Control A.5.9)

In accordance with ISO/IEC 27001:2022 Control A.5.9 (Inventory of Information and Other Associated Assets), Northwind Health identifies, classifies, and tracks ownership for all critical information assets and supporting infrastructure. 

This asset register specifically captures the target environment evaluated during the AI writing assistant policy exception request, detailing trust boundary status, Business Associate Agreement (BAA) execution, and Single Sign-On (SSO) integration.

---

## 2. Information Asset Inventory

| Asset ID | Asset Name | Asset Category | Owner / Location / Dept | Business Purpose | Storing / Processing ePHI | BAA Required | BAA Executed | SSO Integrated |
| :---: | :--- | :--- | :--- | :--- | :---: | :---: | :---: | :---: |
| **A001** | Patient Database | Information | Head of Clinical Operations | Value, confidentiality, integrity, and compliance of ePHI storage. | Yes | No | No | Yes |
| **A002** | Patient Database Software | Software / SaaS | Chief Information Officer (CIO) | Database engine continuity; system patching, stability, security, and licensing. | Yes | No | No | Yes |
| **A003** | On-Premises Identity Provider (SSO) | Software / SaaS | Head of Infrastructure | Automates single-point user authentication; enforces MFA and access control policies. | No | Yes | Yes | Yes |
| **A004** | Marketing Team | Human | Chief Marketing Officer | Public outreach and campaign management. | Yes | No | No | N/A |
| **A005** | Free-Tier AI Writing Assistant | Software / SaaS | Third-Party Vendor | Prompt drafts including patient name, appointment type, clinic, and date. | Yes | Yes | No | No |
| **A006** | AI Data Improvement Process | Information | Third-Party Vendor | Inputs containing ePHI stored and utilized to train/improve vendor models. | Yes | Yes | No | N/A |
| **A007** | AI Database Software | Software / SaaS | Third-Party Vendor | Ephemeral session caching and data processing to deliver API responses. | Yes | Yes | No | N/A |
| **A008** | Enterprise AI Tier | Information | Third-Party Vendor | Enterprise LLM processing under formal enterprise privacy and security terms. | Yes | Yes | Yes | Yes |
| **A009** | Message Delivery Platform | Software / SaaS | Clinic / Healthcare Provider | Delivery of personalized appointment reminders containing ePHI. | Yes | No | No | Yes |
| **A010** | Patient Delivery Destinations | Human / Software / Hardware | Not Specified | Recipient endpoints (SMS, email, mobile devices) receiving clinic communications. | Yes | No | No | Unknown |

---

## 3. Key Observations & Security Baseline Gaps

1. **Third-Party AI Exception Boundary (A005–A007):** Assets A005, A006, and A007 operate entirely outside the Northwind Trust Boundary. They process ePHI without executed Business Associate Agreements (BAAs) or Single Sign-On (SSO) authentication, violating HIPAA §164.502(e) and internal Access Control Policies.
2. **Enterprise AI Alternative (A008):** Represents the compliant target asset configuration, possessing required technical safeguards (SSO) and administrative controls (executed BAA).
3. **Delivery Channel Verification (A009–A010):** Asset A009 processes ePHI without a recorded BAA requirement, while endpoint delivery destinations (A010) lack explicit asset ownership and safeguard definitions, requiring formal validation.
