# GRC-Analyst
A fictional GRC case study assessing an AI policy exception request involving patient data at a healthcare SaaS company. It demonstrates evaluating ePHI classification, risk scoring, compliance decisions, and drafting clear stakeholder communication in a regulated environment.

# Scenario

𝐍𝐨𝐫𝐭𝐡𝐰𝐢𝐧𝐝 𝐇𝐞𝐚𝐥𝐭𝐡, a 120-person US healthcare SaaS company that stores patient data (ePHI) for around 400 clinics.

𝐓𝐢𝐜𝐤𝐞𝐭 𝐟𝐫𝐨𝐦 𝐲𝐨𝐮𝐫 𝐦𝐚𝐧𝐚𝐠𝐞𝐫:

> "Marketing want an exception to our AI policy. Can you assess it and recommend a decision? Please draft the reply to the Head of Marketing too."
𝐓𝐡𝐞 𝐫𝐞𝐪𝐮𝐞𝐬𝐭 (𝐟𝐫𝐨𝐦 𝐭𝐡𝐞 𝐇𝐞𝐚𝐝 𝐨𝐟 𝐌𝐚𝐫𝐤𝐞𝐭𝐢𝐧𝐠)

> "We'd like to use a free AI writing assistant to personalise appointment reminder messages. The team would paste in the patient's first name, appointment type, clinic, and date. It would save us around 10 hours a week. Can we get an exception?"
𝐍𝐨𝐫𝐭𝐡𝐰𝐢𝐧𝐝 𝐩𝐨𝐥𝐢𝐜𝐲 𝐞𝐱𝐜𝐞𝐫𝐩𝐭

> 𝐀𝐜𝐜𝐞𝐩𝐭𝐚𝐛𝐥𝐞 𝐔𝐬𝐞 𝐏𝐨𝐥𝐢𝐜𝐲, 𝟒.𝟑: ePHI must not be entered into any system that has not been approved by Security and covered by a Business Associate Agreement (BAA) where required.

𝐖𝐡𝐚𝐭 𝐲𝐨𝐮 𝐤𝐧𝐨𝐰 𝐚𝐛𝐨𝐮𝐭 𝐭𝐡𝐞 𝐭𝐨𝐨𝐥
- The free tier's terms allow user inputs to be used to improve the vendor's models
- No BAA is available on the free tier
- An enterprise tier exists at $30 per user per month: it includes a BAA, no training on customer data, SSO, and audit logs
- The marketing team has four people


𝐘𝐨𝐮𝐫 𝐝𝐞𝐥𝐢𝐯𝐞𝐫𝐚𝐛𝐥𝐞𝐬

1. 𝐈𝐬 𝐭𝐡𝐢𝐬 𝐞𝐏𝐇𝐈? Answer yes or no and explain why.
2. 𝐒𝐜𝐨𝐫𝐞 𝐭𝐡𝐞 𝐫𝐢𝐬𝐤 of approving the request as written, using Likelihood × Impact on a 1-5 scale, with one sentence justifying each number.
3. 𝐘𝐨𝐮𝐫 𝐝𝐞𝐜𝐢𝐬𝐢𝐨𝐧: approve, deny, or approve with conditions. If conditions, list them.
4. 𝐘𝐨𝐮𝐫 𝐫𝐞𝐩𝐥𝐲 𝐭𝐨 𝐭𝐡𝐞 𝐇𝐞𝐚𝐝 𝐨𝐟 𝐌𝐚𝐫𝐤𝐞𝐭𝐢𝐧𝐠: 200 words maximum, no jargon, and offer a way forward rather than just a "no."
𝐵𝑜𝑛𝑢𝑠 𝑝𝑜𝑖𝑛𝑡 𝑓𝑜𝑟 𝑡ℎ𝑒 𝑏𝑒𝑠𝑡 𝑖𝑑𝑒𝑎 𝑡ℎ𝑎𝑡 𝑠𝑜𝑙𝑣𝑒𝑠 𝑀𝑎𝑟𝑘𝑒𝑡𝑖𝑛𝑔'𝑠 𝑝𝑟𝑜𝑏𝑙𝑒𝑚 𝑤𝑖𝑡ℎ𝑜𝑢𝑡 𝑎𝑛𝑦 𝑝𝑎𝑡𝑖𝑒𝑛𝑡 𝑑𝑎𝑡𝑎 𝑙𝑒𝑎𝑣𝑖𝑛𝑔 𝑁𝑜𝑟𝑡ℎ𝑤𝑖𝑛𝑑 𝑎𝑡 𝑎𝑙𝑙.

 𝐒𝐮𝐛𝐦𝐢𝐬𝐬𝐢𝐨𝐧 𝐅𝐨𝐫𝐦𝐚𝐭 
 
Path: [GRC]

1. [The combination of patient's first name, appointment type, clinic, and date is ePHI. Sections 164.514(b) of the HIPPA privacy rule, otherwise known as the "Safe Harbour" method for de-identification mandates the removal of 18 types of identifiers. The marketing teams exception request inclusion of the patients name strictly violates identifier number 1 (Names) and the inclusion of patients appointment date strictly violates identifier 3 (All elements of dates) of the 18 identifiers laid out by Sections 164.514(b).]

2. **OWASP Threat Dragon data flow diagram**

```mermaid
flowchart LR
  subgraph NW["Northwind Health trust boundary"]
    M["Marketing Team<br/>4 staff"]
    SSO["Northwind Identity Provider<br/>(SSO)"]
    DB[("Patient Database<br/>ePHI source")]
    DB -->|"ePHI access"| M
    SSO -->|"SSO authentication"| M
  end

  AI["AI Writing Assistant<br/>Free tier · outside Northwind control"]
  V[("Vendor data store<br/>Inputs may train models")]
  M ==>|"ePHI: first name, appointment date,<br/>clinic, and appointment type<br/>Unmanaged account bypasses SSO"| AI
  AI ==>|"Data retained / used for model training"| V

  classDef northwind fill:#eef6ff,stroke:#4f7fb2,color:#172033,stroke-width:2px;
  classDef external fill:#fff5ee,stroke:#d58a4a,color:#172033,stroke-width:2px;
  classDef risk fill:#fff1f0,stroke:#c2413b,color:#7f1d1d,stroke-width:3px;
  class M,SSO,DB northwind;
  class AI external;
  class V risk;
  linkStyle 2,3 stroke:#c2413b,stroke-width:3px,color:#7f1d1d;
```

*Fictional scenario based on the supplied Threat Dragon JSON. The diagram shows the requested ePHI flow reaching the free AI assistant through an unmanaged account that bypasses SSO, and the vendor's potential use of inputs for model training.*
