# GRC Case Study: AI Policy Exception Risk Assessment

A Governance, Risk, and Compliance (GRC) assessment of an AI policy exception request involving Electronic Protected Health Information (ePHI) at a healthcare SaaS company. This case study evaluates ePHI classification under HIPAA, conducts a comprehensive risk assessment mapped to ISO/IEC 27001/27002 controls, determines a compliance decision, and drafts stakeholder communication.

---

## Executive Overview

* **Organization:** Northwind Health, Inc. (120 employees, remote-first, HQ in Austin, TX)
* **Industry & Role:** Healthcare SaaS / Business Associate serving ~400 outpatient clinics (~1.2M patient records)
* **Role:** GRC Analyst
* **Task:** Evaluate an exception request from the Head of Marketing to use a free third-party AI tool for personalizing appointment reminder messages.

### The Exception Request
> "We'd like to use a free AI writing assistant to personalise appointment reminder messages. The team would paste in the patient's first name, appointment type, clinic, and date. It would save us around 10 hours a week. Can we get an exception?"

### Policy Mandate (Acceptable Use Policy, Section 4.3)
> "ePHI must not be entered into any system that has not been approved by Security and covered by a Business Associate Agreement (BAA) where required."

---

## Tool Comparison & Profile

| Feature | Free Tier (Requested) | Enterprise Tier (Available) |
| :--- | :--- | :--- |
| **Data Training** | Public training enabled on inputs | Excluded from model training |
| **Contractual Protection** | **No BAA Available** | **BAA Provided** |
| **Access Control** | Personal accounts (No SSO) | Identity Provider / SSO Integration |
| **Auditability** | None | Full audit & activity logging |
| **Cost** | $0 | $30 / user / month ($120/mo for 4 staff) |

---

## Deliverables & Key Findings

### Deliverable 1: Determination of ePHI
**Result: YES.** 

The dataset proposed for processing (Patient First Name + Appointment Type + Clinic + Date) constitutes **Electronic Protected Health Information (ePHI)** under 45 CFR Section 160.103. 

Under HIPAA Section 164.514(b) (Safe Harbor Method for De-Identification), data is only considered de-identified if 18 specific categories of identifiers are removed. The proposed workflow explicitly violates:
1. **Identifier #1 (Names):** Patient's first name.
2. **Identifier #3 (Dates):** Appointment date (all elements of dates except year are restricted).

Combining these identifiers with clinical data (clinic name and appointment type) allows direct re-identification of an individual's health status and healthcare schedule.

---

### Deliverable 2: Risk Scoring Matrix

Risk scores are calculated using **Likelihood (1–5) × Impact (1–5) = Risk Rating (1–25)**.

| Risk ID | Risk Scenario | Likelihood | Impact | Rating | Classification | Justification |
| :---: | :--- | :---: | :---: | :---: | :---: | :--- |
| **R-001** | **Public Model Training on ePHI** | 5 | 5 | **25** | Critical | Inputs on the free tier are used for public model training, creating an instantaneous, unmitigated HIPAA breach and regulatory exposure. |
| **R-002** | **Data Retention & Re-identification** | 4 | 4 | **16** | High | Vendor retention of data outside Northwind's control creates permanent third-party exposure and re-identification risks. |
| **R-003** | **Indefinite Data Lingering** | 4 | 4 | **16** | High | Lack of enforced retention/deletion schedules allows sensitive data to reside in unmonitored temporary storage indefinitely. |
| **R-004** | **Unmanaged Account Access (No SSO)** | 4 | 3 | **12** | High/Medium | Absence of SSO prevents centralized identity lifecycle management, allowing former employees to retain access post-offboarding. |
| **R-005** | **Outdated Contact Misdirection** | 3 | 3 | **9** | Medium | Inaccurate or shared contact details risk exposing appointment details to unintended recipients during delivery. |
| **R-006** | **Lack of Business Associate Agreement** | 4 | 2 | **8** | Medium | Transmitting ePHI without a executed BAA directly violates HIPAA Security & Privacy Rules, exposing the firm to statutory fines. |

#### Summary Breakdown
| Severity | Count | Primary Issue |
| :--- | :---: | :--- |
| **Critical** | 1 | Direct statutory violation and public model ingestion of ePHI |
| **High** | 2 | Third-party retention, re-identification, and lingering data risks |
| **Medium / High** | 3 | Access governance deficiencies, missing BAAs, and contact error risks |

---

### Deliverable 3: Governance Decision

**Decision: DENIED as written | APPROVED WITH CONDITIONS (Option B)**

* **Denied:** The free tier cannot be approved under any circumstances due to non-negotiable HIPAA regulatory non-compliance and Acceptable Use Policy Section 4.3 violations.
* **Approved with Conditions (Enterprise Tier):** Marketing may utilize the tool *only* upon upgrading to the Enterprise Tier ($120/month total), subject to the following mandatory controls:
  1. **Execute BAA:** A signed Business Associate Agreement must be finalized with the vendor.
  2. **Enable SSO & Audit Logging:** Enforce Single Sign-On via Northwind's Identity Provider and enable central logging.
  3. **Zero-Training Verification:** Confirm vendor data-use controls opt out of model training.
  4. **Zero-ePHI Prompt Structure (Preferred Mitigation):** Transition templates to anonymous placeholders.

---

### Deliverable 4: Stakeholder Communication

**To:** Head of Marketing  
**From:** GRC Analyst  
**Subject:** Response: AI Policy Exception Request – Appointment Reminders  

Hi [Name],

Thank you for reaching out. We evaluated your request to use the free AI writing assistant for personalized appointment reminders. 

**Decision:** We cannot approve the **free tier** of this tool. Because it retains data to train public models and lacks a Business Associate Agreement (BAA), entering patient names and appointment dates creates an immediate HIPAA violation and regulatory fine risk.

**How We Move Forward Together:**
We want to help you save those 10 hours a week safely. Here are two approved paths forward:

1. **Zero-ePHI Templates (Free & Immediate):** Use static variables/placeholders in the AI prompt (e.g., *"Write a warm reminder for [FIRST_NAME] about a [APPOINTMENT_TYPE] on [DATE]"*). The team copies the AI output into your sending platform and fills in real details locally. No patient data ever leaves Northwind.
2. **Enterprise Tier Upgrade ($120/mo):** Upgrading your 4-person team to the Enterprise tier ($30/user/month) provides a signed BAA, zero data training, SSO access, and full audit logging. 

Let me know which option you'd like to pursue, and I'll help you set it up!

Best regards,  
**GRC Analyst** | Northwind Health
