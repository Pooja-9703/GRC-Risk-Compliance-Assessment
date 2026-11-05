# Deliverable 1: Asset Inventory & Classification Methodology

**Organization:** ShopPulse Retail Solutions Inc.  
**Assessor:** Junior GRC Analyst (Simulated Engagement)  
**Version:** 1.2 (Updated Criticality Methodology & Regulatory Context)  

---

## 1. Asset Classification Methodology

Assets at ShopPulse Retail Solutions Inc. are categorized and valued based on their role in supporting core business processes, regulatory compliance obligations, and potential impact on business continuity if compromised.

### Data Classification Categories
* **Public:** Information intended for public consumption (e.g., public marketing catalog, public store product pricing).
* **Internal:** Non-sensitive operational data intended for internal staff use (e.g., internal operating procedures, meeting notes, public storefront application structure).
* **Confidential:** Sensitive business or personal data protected by privacy laws or commercial interest (e.g., Customer PII, employee payroll records, internal communications).
* **Restricted:** Highly sensitive data where compromise would cause severe financial, legal, or operational impact (e.g., AWS IAM administrator credentials, Stripe API secret keys, application source code).

### Impact Level Ratings (CIA Triad)
Each asset is evaluated against **Confidentiality (C)**, **Integrity (I)**, and **Availability (A)** using a 3-tier impact scale:
* **Low (L):** Unauthorized disclosure, modification, or destruction has limited minor impact.
* **Medium (M):** Compromise causes noticeable operational disruption or moderate financial/regulatory consequence.
* **High (H):** Compromise causes severe business paralysis, major regulatory fines (e.g., CCPA/PCI), or catastrophic financial loss.

### Criticality Level Determination Methodology
Overall Asset Criticality is determined using the asset's business importance, potential enterprise impact, dependency on critical business processes, and CIA impact ratings. CIA ratings inform the assessment but are not mechanically converted into Overall Criticality.

* **Critical:** Assets whose compromise, loss, or prolonged unavailability could cause severe enterprise-wide impact, materially disrupt revenue-generating operations, or compromise privileged control over critical infrastructure.
* **High:** Assets whose compromise could cause significant operational, financial, privacy, or security impact but would not independently cause enterprise-wide disruption.
* **Medium:** Assets supporting important business functions where reasonable workarounds or alternative processes exist.
* **Low:** Assets with limited business impact and readily available alternatives.

---

## 2. Asset Inventory Table

| Asset ID | Asset Name | Asset Type | Description & Purpose | Asset Owner | Business Function | Data Classification | Regulatory / Compliance Context | Confidentiality Impact | Integrity Impact | Availability Impact | Overall Criticality | Environment / Location | Dependencies |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :---: | :---: | :---: | :---: | :--- | :--- |
| **AST-01** | E-Commerce Web Storefront & Portal | Software / App | Customer-facing web application (React/Node.js) hosting storefront catalog and B2B ordering portal. | Lead DevOps Engineer | Order Placement & Catalog Browsing | Internal | Privacy / Application Security | Medium | High | High | **Critical** | AWS ECS (US-East-1) | AST-02, AST-05, AST-07 |
| **AST-02** | Production RDS PostgreSQL Database | Data / Database | Primary relational database storing user accounts, order history, and customer PII. | Lead DevOps Engineer | Customer Data & Transaction Records | Confidential | CCPA/CPRA; Texas Data Privacy and Security Act | High | High | High | **Critical** | AWS RDS Private Subnet | AST-05 |
| **AST-03** | Employee Corporate Endpoint Fleet | Hardware / Endpoints | 45 corporate laptops (macOS & Windows 11) used by staff for remote work. | IT Manager | Daily Staff Workstations & Administrative Access | Confidential | Privacy / Endpoint Security | High | Medium | Medium | **High** | Distributed Remote Workstations | AST-05, AST-06 |
| **AST-04** | GitHub Private Repositories & CI/CD | Software / Repo | Proprietary source code repositories, deployment scripts, and GitHub Actions pipelines. | Lead Software Engineer | Software Development & Deployment | Restricted | Security Governance / Intellectual Property Protection | High | High | Medium | **High** | GitHub Cloud (SaaS) | AST-01, AST-05 |
| **AST-05** | AWS IAM & Cloud Control Plane | Cloud Infra | Centralized AWS administrative access and configuration layer governing IAM identities, roles, access keys, VPC networking, security groups, and related cloud resources. | IT Manager / CTO | Infrastructure Management & Access Control | Restricted | Security Governance / Access Control | High | High | High | **Critical** | AWS Cloud (Global/US-East-1) | None |
| **AST-06** | Google Workspace Suite | SaaS / Email | Corporate email (`@shoppulse.com`), Google Drive files, and internal chat. | IT Manager | Internal Corporate Comms & Document Storage | Confidential | Privacy / Corporate Information Protection | High | Medium | Medium | **High** | Google Cloud (SaaS) | AST-03 |
| **AST-07** | Stripe Payment Gateway API Integration | SaaS / Payment | Payment processing integration using Stripe Elements iFrames for card checkout. | CTO / Finance Lead | Payment Processing & Tokenization | Restricted | PCI DSS | High | High | High | **Critical** | Stripe Cloud (Third-Party API) | AST-01 |
| **AST-08** | 3PL Warehouse Management System API | Third-Party API | API link to 3PL logistics provider for shipping label generation and inventory sync. | Operations Manager | Order Fulfillment & Inventory Management | Internal | Third-Party Risk Management | Medium | High | Medium | **High** | 3PL Partner Cloud | AST-01 |
| **AST-09** | Zendesk Customer Support System | SaaS / Support | Ticketing platform housing customer support inquiries and order history notes. | Customer Support Lead | Customer Service & Inquiries | Confidential | Privacy / Customer Data Protection | Medium | Medium | Medium | **Medium** | Zendesk Cloud (SaaS) | AST-06 |
| **AST-10** | QuickBooks Online & Payroll System | SaaS / Finance | Cloud accounting platform storing corporate financial ledgers and employee payroll details. | Accounting Manager | Accounting, Invoicing & Payroll | Confidential | Privacy / Financial and HR Data Protection | High | High | Medium | **High** | Intuit Cloud (SaaS) | AST-06 |

---

## 3. Scope Notes & Assessment Rationale

1. **PCI-DSS Scope Rationale:** `AST-07` utilizes Stripe Elements iFrame integration. Customer payment card numbers are collected directly within Stripe-hosted iFrame fields. This architecture significantly reduces internal PCI DSS scope by preventing cardholder data from entering or residing on ShopPulse servers. The exact applicable Self-Assessment Questionnaire (e.g., SAQ A vs. SAQ A-EP) requires formal confirmation against PCI DSS v4.0 eligibility criteria and merchant payment flow validation. Web application integrity (`AST-01`) remains important because client-side compromise or malicious modification of payment-related page components could affect the security of the payment flow.
2. **Endpoint Management Baseline:** `AST-03` endpoint inventory reflects 45 active corporate laptops enrolled in MDM (Jamf/Intune). Remote staff connect to SaaS resources via web browser, while engineers connect to `AST-05` AWS VPC subnets via AWS Client VPN. Centralized disk-encryption enforcement across all 45 devices is treated as a risk condition requiring verification via MDM compliance reports.
