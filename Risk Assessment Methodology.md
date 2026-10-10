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

# Risk Identification
Identify Risks: Identify risks related to the loss of security within the ISMS scope, and assign risk owners to each.

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

Threats were identified using the  [Northwind LINDDUN threat model](documents/Threat%20Model.md), as follows: 

1. T01 — Linkability: Repeated ePHI prompts may be linked into a patient profile.
2. T02 — Identifiability: Prompt details may identify the patient.
3. T03 — Disclosure: Identifiable ePHI is disclosed to the free-tier AI vendor.
4. T04 — Non-compliance: Free-tier processing may conflict with policy or privacy obligations.
5. T05 — Linkability: Repeated reminders or metadata may reveal a patient’s care pattern.
6. T06 — Identifiability: Reminder content or records may identify the patient and care context.
7. T07 — Non-repudiation: Delivery records may evidence a patient’s care relationship.
8. T08 — Detectability: A notification may reveal clinic involvement.
9. T09 — Disclosure: A shared or incorrect destination may receive ePHI.
10. T10 — Linkability: Training data may link prompts across appointments.
11. T11 — Identifiability: Stored prompts or cached data may retain patient identifiers.
12. T12 — Non-repudiation: Retained prompts or records may evidence an appointment.
13. T13 — Detectability: Vendor data or model behavior may reveal that patient data was included.
14. T14 — Disclosure: Cached or retained ePHI may be exposed from vendor storage.
15. T15 — Unawareness: Patients may not know a vendor processes reminder data; notice status needs checking.
16. T16 — Disclosure: The reminder platform’s ePHI safeguards are not established.
17. T17 — Non-compliance: Whether a BAA is required for the reminder platform is unresolved.


## Risk Identification Methodology

The risk identification process follows the standard security formulation:

Risk = (Vulnerability + Threats)

The vulnerability-to-threat mapping table is in the [Risk Identification Methodology document](documents/Risk%20Identification%20Methodology.md). For each vulnerability, the table links the relevant threat IDs, describes those threats, and gives one overall risk statement combining the vulnerability. The Overall risk statements were assigned to a Risk-Id as follows: 

- R-001 — Free-tier AI writing assistant: If Marketing uses the free tier with identifiable appointment data, ePHI could be disclosed to the vendor and retained or used for model improvement without Northwind’s approved safeguards, potentially exposing patient-care relationships and causing policy or privacy non-compliance.
- R-002 — AI data improvement process: If the vendor retains ePHI for model improvement, data from multiple appointments could be linked or inferred in vendor-controlled storage or models, increasing the chance of identifying patients or exposing their care information outside Northwind’s control.
- R-003 — AI database software/cache: If cached ePHI lacks effective access, protection, retention, or deletion safeguards, identifiers and appointment details could persist and be exposed. The register does not establish whether these safeguards are absent, so this risk requires validation.
- R-004 — Message delivery platform: If the delivery platform lacks appropriate safeguards, or a required BAA is absent, reminder content, metadata, or delivery records could reveal patient-care information to others and create privacy or contractual non-compliance. The platform’s role and BAA applicability need confirmation.
- R-005 — Patient delivery destinations: If a destination is shared, outdated, or incorrect, or a notification is visible to others, reminders or delivery metadata could reveal a patient’s identity and care relationship to an unintended recipient. Destination ownership and safeguards are unspecified.









Analyze Risks: Assess potential consequences, evaluate the realistic likelihood of occurrence, and determine overall risk levels.

Evaluate & Prioritize Risks: Compare analyzed risks against established risk criteria and prioritize them for risk treatment.

Document the Process: Retain documented information covering the entire risk assessment workflow.



