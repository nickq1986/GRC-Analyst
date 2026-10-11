# Document Reference: ISMS-DOC-01-SC
**Classification:** Internal  
**Version:** 1.0  
**Status:** Approved  
**Owner:** Information Security & Compliance  
**Standard:** ISO/IEC 27001:2022 (Clauses 4.1, 4.2, 4.3, 4.4)

---

# 01 · Context of the Organization & ISMS Scope

## 1. Organizational Context (ISO/IEC 27001 Clause 4.1 & 4.2)

### 1.1 Organizational Profile
* **Organization Name:** Northwind Health, Inc.
* **Industry:** Healthcare Software-as-a-Service (SaaS)
* **Primary Business Function:** Provision of cloud-based patient scheduling and automated appointment reminder platform services.
* **Scale & Operations:** 120 personnel operating under a remote-first model (Headquarters: Austin, TX, USA).
* **Client Ecosystem:** Serves ~400 outpatient healthcare clinics across the United States.
* **Information Asset Classification:** Holds and processes Electronic Protected Health Information (ePHI) for approximately 1.2 million patient data subjects, including personally identifiable information (PII), appointment dates, clinic metadata, and clinical visit descriptions.
* **Regulatory Role:** Business Associate (BA) under the Health Insurance Portability and Accountability Act (HIPAA) to client Covered Entities.
* **Technical Architecture:** Amazon Web Services (AWS) single production cloud region, Google Workspace for corporate operations, integrated Identity Provider (IdP) for Single Sign-On (SSO).

### 1.2 Internal and External Issues (Clause 4.1)
* **Internal Context:** Expanding marketing and operational requirements driving demand for third-party automated tools (including Artificial Intelligence and Natural Language Processing tools) to improve efficiency.
* **External Context:** High regulatory enforcement environment surrounding ePHI privacy and data security; evolving threat landscape targeting healthcare SaaS sub-processors and vendors.

### 1.3 Interested Parties & Requirements (Clause 4.2)
* **Healthcare Clinic Clients (Covered Entities):** Demand strict HIPAA compliance, executed Business Associate Agreements (BAAs), and SOC 2 Type II attestation as a condition of service and renewal.
* **Regulatory Bodies (U.S. Department of Health and Human Services / OCR):** Enforce HIPAA Security and Privacy Rules, requiring formal periodic risk analysis (45 CFR Section 164.308(a)(1)(ii)(A)) and risk management measures.
* **Board of Directors:** Requires visibility into critical information security risks and approval governance over security capital investments.

---

## 2. Scope of the Information Security Management System (ISO/IEC 27001 Clause 4.3)

### 2.1 Statement of Applicability & Boundaries
The scope of the Information Security Management System (ISMS) encompasses all processes, systems, and personnel involved in the processing, storage, transmission, and management of ePHI and supporting SaaS operations.

### 2.2 In-Scope Boundaries
* **Production Application & Services:** Cloud-native patient scheduling application (web and mobile interfaces).
* **Cloud Infrastructure:** AWS production environment, including database clusters, document storage repositories, and network configurations processing or storing ePHI.
* **Identity & Access Management:** Workforce identity provider (IdP / SSO), corporate email, endpoint device management, and access lifecycle operations.
* **Third-Party & Vendor Processing:** Third-party software services, applications, and sub-processors processing, storing, or transmitting ePHI (including marketing and communication automation tools).

### 2.3 Out-of-Scope Boundaries
* Public-facing marketing website (isolated infrastructure; processes no ePHI).
* Corporate Finance and Human Resources systems (governed under separate administrative operational controls).
* Physical security of client clinic facilities.

---

## 3. ISMS Operations & Stakeholder Engagement (ISO/IEC 27001 Clause 4.4)

### 3.1 Risk Assessment Boundaries & Assumptions
* **Assessment Scope:** Point-in-time risk evaluation effective October 2026.
* **Assessment Methodology:** Documentation review, architectural configuration evaluation, and structured stakeholder interviews.
* **Technical Validation:** Risk identification based on architectural and configuration review; dynamic penetration testing evaluated under separate risk cycles.

### 3.2 Key Stakeholders Consulted
| Stakeholder Role | Domain of Responsibility |
| :--- | :--- |
| **Chief Technology Officer (CTO)** | Platform Architecture, Cloud Infrastructure, Engineering Practices |
| **IT Manager** | Endpoint Security, Identity & Access Management (IAM), User Onboarding/Offboarding |
| **Compliance Manager** | HIPAA Alignment, Vendor Risk Management, BAA Governance, ISMS Policies |
| **Customer Success Lead** | Client Data Processing Requests, Downstream Vendor Tooling Usage |
