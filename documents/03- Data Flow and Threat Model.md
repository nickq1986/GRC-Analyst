# Document Reference: ISMS-DOC-02-TM
**Classification:** Internal  
**Version:** 1.0  
**Status:** Approved  
**Owner:** Information Security & Compliance  
**Standard:** ISO/IEC 27001:2022 (Clause 6.1.2) & ISO/IEC 27701:2019 (Clause 6.5)

---

# 02.1 · Threat Identification & LINDDUN Privacy Model

## 1. Scope & Objective (ISO/IEC 27001 Clause 6.1.2.a)

This document records the systematic threat identification executed for the proposed AI writing assistant policy exception request. In alignment with ISO/IEC 27005 guidelines, threat scenarios are identified and mapped against target system assets without assigning likelihood or impact scores at this stage. Qualitative risk analysis and scoring are conducted subsequently in the Risk Register.

---

## 2. Asset & Vulnerability Baseline

The threat modeling boundary evaluates five primary asset components identified in the exception request:

* **A005 — Free-Tier AI Writing Assistant:** Unmanaged account operating outside Northwind SSO; no executed Business Associate Agreement (BAA); vendor terms enable model training on user inputs.
* **A006 — Vendor Model Improvement Pipeline:** Process where prompt inputs containing ePHI are ingested and retained for vendor model optimization.
* **A007 — AI Local Storage / Caching:** Local temporary storage caching ePHI prompts without documented access, retention, or deletion controls. *(Requires Validation)*
* **A009 — Appointment Reminder Delivery Platform:** Intermediary messaging platform processing reminder content; BAA status and transmission safeguards unconfirmed. *(Requires Validation)*
* **A010 — Patient Destination Endpoints:** Recipient devices and communication channels (SMS/Email); ownership and endpoint encryption safeguards unspecified.

---

## 3. Threat Model Architecture Diagram

The following data flow diagram illustrates the movement of ePHI across organizational trust boundaries, highlighting the 17 identified LINDDUN privacy threat annotations:

```mermaid
flowchart LR
    subgraph NW["Northwind Health Trust Boundary"]
        DB[("Patient Database<br/>ePHI Source")]
        SSO["Identity Provider<br/>(SSO)"]
        M["Marketing Team<br/>(4 Staff)"]

        DB -->|"Patient & appointment details"| M
        SSO -->|"SSO authentication"| M
    end

    AI["Free-Tier AI Writing Assistant<br/>Unmanaged Account | No SSO<br/>No BAA | Model Training Enabled"]
    V[("Vendor Data Store<br/>Model Improvement Pipeline")]

    subgraph DELIVERY["Reminder Delivery Platform (Trust Boundary to Confirm)"]
        DP["Appointment Reminder Delivery<br/>Safeguards & BAA Status to Validate"]
    end

    P["Patient<br/>Message Destination / Device"]

    M -->|"T01–T04: ePHI prompt (Name, Type, Clinic, Date) [A005]"| AI
    AI -->|"Personalized reminder draft returned"| M
    AI -->|"T10–T14: Inputs retained for model training [A006];<br/>Cache controls require validation [A007]"| V
    M -->|"Reminder content & recipient details"| DP
    DP -->|"T05–T09: Reminder sent; delivery records unspecified [A009–A010]"| P

    subgraph LINDDUN["LINDDUN Threat Annotations (17 Threats Identified)"]
        direction TB
        TAI["AI Prompt Flow (A005–A006)<br/>T01 Linkability — Repeated prompts build patient profiles<br/>T02 Identifiability — Prompt attributes identify patients<br/>T03 Disclosure — Identifiable ePHI sent to free-tier vendor<br/>T04 Non-Compliance — Policy and privacy obligations breached"]
        TV["Vendor Storage (A006–A007)<br/>T10 Linkability — Storage connects appointments over time<br/>T11 Identifiability — Cached prompts retain patient identifiers<br/>T12 Non-Repudiation — Retained records evidence appointment<br/>T13 Detectability — Model behavior reveals patient data ingestion<br/>T14 Disclosure — Cached ePHI exposed via vendor breach"]
        TR["Reminder Delivery & Receipt (A009–A010)<br/>T05 Linkability — Messages reveal patient care patterns<br/>T06 Identifiability — Delivery records identify patient and care<br/>T07 Non-Repudiation — Delivery logs prove care relationship<br/>T08 Detectability — Notifications reveal clinic association<br/>T09 Disclosure — Shared/incorrect endpoints receive ePHI"]
        TP["Patient Awareness<br/>T15 Unawareness — Patients uninformed of vendor processing"]
        TDP["Delivery Platform (A009)<br/>T16 Disclosure — Platform ePHI safeguards unestablished<br/>T17 Non-Compliance — BAA applicability unresolved"]
    end

    AI -.-> TAI
    V -.-> TV
    DP -.-> TDP
    P -.-> TP
    DP -.-> TR

    classDef northwind fill:#eff6ff,stroke:#2563eb,stroke-width:2px,color:#172554;
    classDef vendor fill:#fff7ed,stroke:#ea580c,stroke-width:2px,color:#7c2d12;
    classDef delivery fill:#f8fafc,stroke:#64748b,stroke-width:2px,color:#0f172a;
    classDef patient fill:#f5f3ff,stroke:#7c3aed,stroke-width:2px,color:#3b0764;
    classDef threat fill:#fff1f2,stroke:#e11d48,stroke-width:1.5px,color:#881337;

    class DB,SSO,M northwind;
    class AI,V vendor;
    class DP delivery;
    class P patient;
    class TAI,TV,TR,TP,TDP threat;
