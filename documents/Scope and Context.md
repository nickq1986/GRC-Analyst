# 01 · Context of the Organization & ISMS Scope (ISO/IEC 27001)

## 1. Context of the Organization (Clause 4.1 & 4.2)

### 1.1 Organizational Profile
* **Organization:** Northwind Health, Inc.
* **Industry:** Healthcare Software-as-a-Service (SaaS)
* **Primary Business Function:** Patient scheduling and automated appointment reminders.
* **Scale & Operations:** ~120 personnel (remote-first operational model; HQ in Austin, TX, USA).
* **Target Operating Environment:** Serves ~400 outpatient healthcare clinics across the United States.
* **Information Assets Held:** Protected Health Information (ePHI) for ~1.2 million data subjects, encompassing personally identifiable identifiers, contact attributes, appointment dates, insurance metadata, and clinical visit rationales.
* **Regulatory & Contractual Role:** Business Associate (BA) under HIPAA regulations to its clinic clients (Covered Entities).

### 1.2 Drivers for Risk Assessment
* **Regulatory Compliance:** Mandated compliance with HIPAA Security Rule requirements (§164.308(a)(1)(ii)(A)–(B)) for periodic risk analysis and management.
* **Contractual Requirements:** SOC 2 Type II attestation is a mandatory prerequisite for contract renewals across three enterprise customer accounts.
* **Governance & Oversight:** Provision of executive-level risk visibility to the Board of Directors to justify security controls investment and resource allocation.

---

## 2. Scope of the Information Security Management System (Clause 4.3)

The boundaries and applicability of the Information Security Management System (ISMS) are formally defined as follows:

### 2.1 In-Scope Boundaries
* **Production Platforms:** Cloud-native patient scheduling application (Web and Mobile interfaces).
* **Infrastructure & Hosting:** AWS Production Environment, including database clusters and document repositories processing or hosting ePHI.
* **Identity & Endpoint Governance:** Corporate Identity Provider (IdP / Single Sign-On), corporate email, Google Workspace, and managed workforce endpoints.
* **Third-Party Ecosystem:** External vendors and sub-processors processing, storing, or transmitting ePHI.

### 2.2 Out-of-Scope Boundaries
* Public-facing marketing website (isolated from ePHI environments).
* Internal corporate Finance and Human Resources information systems (governed under separate operational controls).
* Physical security of client clinic facilities.

---

## 3. Assumptions, Constraints & Stakeholder Engagement (Clause 4.4)

### 3.1 Assessment Boundaries & Constraints
* **Assessment Methodology:** Evaluated via document review, architectural configuration analysis, and simulated stakeholder interviews.
* **Temporal Boundary:** Point-in-time risk posture evaluation effective September 2026.
* **Technical Validation:** Excludes dynamic penetration testing; technical risk findings are derived from system and access configuration audits.

### 3.2 Key Stakeholders Consulted
| Stakeholder Role | Domain of Responsibility |
| :--- | :--- |
| **Chief Technology Officer (CTO)** | Cloud Infrastructure, Platform Architecture, Engineering Controls |
| **IT Manager** | Endpoint Security, Identity & Access Management (IAM), User Lifecycle |
| **Compliance Manager** | Regulatory Alignment (HIPAA), Third-Party / Vendor Risk Management |
| **Customer Success Lead** | Client Data Processing Requests, Shadow IT / Tooling Usage |
