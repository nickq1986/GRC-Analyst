# Northwind Health LINDDUN Threat Model

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
