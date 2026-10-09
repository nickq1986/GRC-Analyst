# Northwinds Health Asset Register

_Converted from the workbook tabs._

## Asset Inventory

| Asset ID | Asset Name | Asset Category | Owner/Location/Dept | Business Purpose | Storing/Processing ePHi | BAA Required (Outside of trust boundary) | BAA Executed | SSO |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| A001 | Patient Database | Information | Head of Clinical Operations | Value, Confidentiality, Integity and compliance of ePHI | Yes | No | No | Yes |
| A002 | Patient Database Software | Software/SaaS | Chief Information Officer (CIO) | Database engine contintuity the system is patched, secure, stable, and properly licensed. | Yes | No | No | Yes |
| A003 | On-Premises Identity Provider ( SSO) | Software/SaaS | Head of Infrastructure | Automates single-point user authentication, enforces MFA/access policies | No | Yes | Yes | yes |
| A004 | Marketing Team | Human | Chief Marketing Officer | Public Outreach | Yes | No | No | NA |
| A005 | Enterprise AI tier | Software / SaaS | Third-party vendor | Prompt includes patient name, appointment type, clinic, and date; restricted ePHI | Yes | Yes | No | No |
| A006 | AI Database/Improvemet Process | Information | Third-party vendor | Inputs containing ePHI may be stored and used to train and improve vendor models | Yes | Yes | No | NA |
| A007 | AI Database Software | Sofware/SaaS | Third-party vendor | Ephemeral session caching ,processing to deliver API responses | Yes | Yes | No | NA |
| A008 | Enterprise AI tier | Information | Third-party vendor | Would process customer data under the stated enterprise terms | Yes | Yes | Yes | Yes |
| A009 | Message Deliver Platform | Software / SaaS | Clinic/healthcare provider: | Personalized appointment reminders contain ePHI | Yes | No | No | Yes |
| A010 | Patient delivery destinations | Human /Software/Hardware | Not Specified | Receive clinic messages | Yes | No | No | Unknown |

## Classification Table

| Classification | Highly Confidential | Confidential | Internal Use Only | Public |
| --- | --- | --- | --- | --- |
| Labeling | Must be labeled as Highly Confidential on all pages | Must be labeled as Confidential on all relevant pages | For Internal Use Only label on internal documents | No special labeling required |
| Storage | Stored in secure locations with restricted access | Stored in locked cabinets or password-protected files | Stored in regular cabinets or shared directories | No special storage requirements |
| Transmission | Encrypted transmission required via secure channels | Password protection required when sharing | Can be transmitted within the organization without encryption | Can be shared freely via email or other channels |
| Access Control | Access limited to senior management or specific roles | Access limited to authorized employees | Accessible to all employees | Accessible by the public |
| Disposal | Must be shredded or securely deleted | Must be deleted securely or physically destroyed | Can be discarded in regular waste after review | No special disposal requirements |
| Backup | Encrypted backups required | Regular encrypted backups | Regular backups stored with basic protection | No special backup requirements |

## Value table

| Value (Criticality) | Description |
| --- | --- |
| High | Asset is crucial to the organization; loss may cause severe damage |
| Medium | Asset is important, but the organization can still function without it |
| Low | Asset has low impact on operations; minimal damage if lost |
