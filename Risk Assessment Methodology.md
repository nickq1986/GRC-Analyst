# Establish Risk Criteria: Define risk acceptance criteria and baseline conditions for conducting risk assessments.

## 1. Risk assessment parameters 

Likeliness:

1 = Negligible, unlikely to happen unless under exceptional circumstances. 
2 = Unlikely, not expected to happen frequently 
3 = Possible, may occur at some point 
4 = High, expected to occur in most circumstances. 
5 = Very High, Almost certain. Continuous or frequent occurrence.

Impact; 

1 = Negligible, minimal operational disruption; minor localized impact requiring basic remediation.   
2 = Low, slight disruption; minor financial loss, minimal data exposure, or brief operational delays.  
3 = Medium, moderate operational disruption; customer dissatisfaction, noticeable financial impact, or minor contractual non-compliance.  
4 = High, significant disruption; legal or regulatory non-compliance, severe financial loss, or major brand/reputational damage.   
5 = Critical, existential impact; severe operational shutdown, substantial regulatory fines, loss of critical IP, or catastrophic financial damage.   

## 2. Risk Formula

Overall risk is calculated using the formula

Risk = Likeliness x Impact 


```mermaid
flowchart TB
    subgraph matrix["Risk Matrix: Likeliness x Impact"]
        direction TB
        subgraph header[" "]
            direction LR
            h0["Likeliness ↓ / Impact →"]:::axis
            h1["1<br/>Negligible"]:::axis
            h2["2<br/>Low"]:::axis
            h3["3<br/>Medium"]:::axis
            h4["4<br/>High"]:::axis
            h5["5<br/>Critical"]:::axis
            h0 ~~~ h1 ~~~ h2 ~~~ h3 ~~~ h4 ~~~ h5
        end
        subgraph row5[" "]
            direction LR
            l5["5<br/>Very High"]:::axis
            r51["5<br/>Moderate"]:::moderate
            r52["10<br/>High"]:::high
            r53["15<br/>High"]:::high
            r54["20<br/>Critical"]:::critical
            r55["25<br/>Critical"]:::critical
            l5 ~~~ r51 ~~~ r52 ~~~ r53 ~~~ r54 ~~~ r55
        end
        subgraph row4[" "]
            direction LR
            l4["4<br/>High"]:::axis
            r41["4<br/>Low"]:::low
            r42["8<br/>Moderate"]:::moderate
            r43["12<br/>High"]:::high
            r44["16<br/>High"]:::high
            r45["20<br/>Critical"]:::critical
            l4 ~~~ r41 ~~~ r42 ~~~ r43 ~~~ r44 ~~~ r45
        end
        subgraph row3[" "]
            direction LR
            l3["3<br/>Possible"]:::axis
            r31["3<br/>Low"]:::low
            r32["6<br/>Moderate"]:::moderate
            r33["9<br/>Moderate"]:::moderate
            r34["12<br/>High"]:::high
            r35["15<br/>High"]:::high
            l3 ~~~ r31 ~~~ r32 ~~~ r33 ~~~ r34 ~~~ r35
        end
        subgraph row2[" "]
            direction LR
            l2["2<br/>Unlikely"]:::axis
            r21["2<br/>Low"]:::low
            r22["4<br/>Low"]:::low
            r23["6<br/>Moderate"]:::moderate
            r24["8<br/>Moderate"]:::moderate
            r25["10<br/>High"]:::high
            l2 ~~~ r21 ~~~ r22 ~~~ r23 ~~~ r24 ~~~ r25
        end
        subgraph row1[" "]
            direction LR
            l1["1<br/>Negligible"]:::axis
            r11["1<br/>Low"]:::low
            r12["2<br/>Low"]:::low
            r13["3<br/>Low"]:::low
            r14["4<br/>Low"]:::low
            r15["5<br/>Moderate"]:::moderate
            l1 ~~~ r11 ~~~ r12 ~~~ r13 ~~~ r14 ~~~ r15
        end
    end
    header ~~~ row5 ~~~ row4 ~~~ row3 ~~~ row2 ~~~ row1

    classDef axis fill:#e2e8f0,stroke:#475569,color:#0f172a,font-weight:bold;
    classDef low fill:#dcfce7,stroke:#16a34a,color:#14532d;
    classDef moderate fill:#fef9c3,stroke:#ca8a04,color:#713f12;
    classDef high fill:#ffedd5,stroke:#ea580c,color:#7c2d12;
    classDef critical fill:#fee2e2,stroke:#dc2626,color:#7f1d1d,font-weight:bold;
```

## 3. Risk Acceptance Criteria
* **Low (1–5):** Risk is within appetite. Acceptable; no mandatory remediation needed.
* **Medium (6–12):** Risk owner must evaluate; treatment required if simple controls exist.
* **High / Critical (13–25):** Exceeds risk appetite.

## 4. Baseline Conditions for Assessments
Risk assessment must be conducted prior granting authorisation to action exception request for Northwind Health AI use policy, under the following baseline condition:

"Prior to major system changes, deployments, or architecture alterations"

# Ensure Consistency: Design the assessment process to yield consistent, valid, and comparable results over repeated executions.

Evidence-Based Rationale & Documentation
* **Mandatory Justification:** Every assigned Likeliness and Impact score must be accompanied by a documented rationale.
* **Documented Assumptions:** Any assumptions regarding existing controls, asset boundaries, or operational environments must be explicitly recorded in the Risk Register.

# Identify Risks: Identify risks related to the loss of security within the ISMS scope, and assign risk owners to each.

## 1. Asset Inventory

The Asset register models of the exception requests projected free tier Ai system that is designed to deliver automated reminders to patients containing ePHI. The Asset inventory can be found [here](https://github.com/nickq1986/GRC-Analyst/blob/main/documents/Northwinds%20Health_Asset_Register.md) 

## 2. Vulnerability Findind
From the register the current vulnerability findings are:

- A005 — Free-tier AI writing assistant: Northwind SSO is not used; no BAA is executed; and the free-tier terms allow inputs to be used to improve the vendor’s models.
- A006 — AI data improvement process: ePHI may be retained and used for model improvement, with no BAA executed.
- A007 — AI database software: It caches ePHI, but the register doesn’t state the cache’s access, protection, retention or deletion controls. Record this as needs validation, not a confirmed vulnerability.
- A009 — Message delivery platform: It processes ePHI, but the register says no BAA is required. Validate the platform’s role and whether that status is correct before calling it a vulnerability.
- A010 — Patient delivery destinations: The owner and safeguards are unspecified. That’s an information gap to investigate; unknown SSO alone doesn’t establish a vulnerability for patient destinations.

## 3. Threat Modelling 

The diagram maps the identified LINDDUN threats to the ePHI prompt, vendor storage, and patient reminder flows. Threats remain open for subsequent risk assessment; severity and risk scores are not assigned here.

```mermaid
flowchart LR
    subgraph NW["Northwind Health"]
        DB[("Patient database<br/>ePHI source")]
        SSO["Northwind identity provider<br/>SSO"]
        M["Marketing team<br/>4 staff"]

        DB -->|"Patient and appointment details"| M
        SSO -->|"SSO for Northwind users"| M
    end

    AI["Free-tier AI writing assistant<br/>Unmanaged vendor account<br/>Not connected to Northwind SSO<br/>No BAA; inputs may improve vendor models"]
    V[("Vendor data store<br/>Model improvement / training")]

    subgraph DELIVERY["Reminder delivery platform — trust-boundary location to confirm"]
        DP["Appointment reminder delivery<br/>Safeguards and BAA applicability to validate"]
    end

    P["Patient<br/>Message destination / device"]

    M -->|"T01–T04: ePHI prompt — first name,<br/>appointment type, clinic and date (A005)"| AI
    AI -->|"Personalized reminder draft returned<br/>to Marketing; may contain ePHI"| M
    AI -->|"T10–T14: inputs may be retained<br/>or used for model improvement (A006);<br/>cache controls require validation (A007)"| V
    M -->|"Reminder content and recipient details"| DP
    DP -->|"T05–T09: reminder sent; channel,<br/>destination and delivery records unspecified"| P

    subgraph LINDDUN["LINDDUN threat annotations — 17 threats, Open; scores TBD"]
        direction TB
        TAI["AI prompt flow (A005–A006)<br/>T01 Linkability — repeated prompts may form a patient profile<br/>T02 Identifiability — prompt attributes identify the patient<br/>T03 Disclosure — identifiable ePHI goes to the free-tier vendor<br/>T04 Non-compliance — policy/privacy obligations may be breached"]
        TV["Vendor storage (A006–A007)<br/>T10 Linkability — records may connect appointments over time<br/>T11 Identifiability — stored prompts/cache may retain identifiers<br/>T12 Non-repudiation — records may evidence an appointment<br/>T13 Detectability — data/model behavior may reveal patient inclusion<br/>T14 Disclosure — cached or retained ePHI may be exposed"]
        TR["Reminder delivery and receipt (A009–A010)<br/>T05 Linkability — reminders may reveal a care pattern<br/>T06 Identifiability — content/records may identify patient and care<br/>T07 Non-repudiation — delivery records may evidence a care relationship<br/>T08 Detectability — notification may reveal clinic involvement<br/>T09 Disclosure — shared or incorrect destination may receive ePHI"]
        TP["Patient awareness<br/>T15 Unawareness — patients may not know a vendor processes reminder data;<br/>notice status needs validation"]
        TDP["Delivery platform (A009)<br/>T16 Disclosure — ePHI safeguards are not established<br/>T17 Non-compliance — BAA applicability is unresolved"]
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
```












Analyze Risks: Assess potential consequences, evaluate the realistic likelihood of occurrence, and determine overall risk levels.

Evaluate & Prioritize Risks: Compare analyzed risks against established risk criteria and prioritize them for risk treatment.

Document the Process: Retain documented information covering the entire risk assessment workflow.



