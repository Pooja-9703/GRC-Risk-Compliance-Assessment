# Organizational Profile & Assessment Scope

**Target Organization:** ShopPulse Retail Solutions Inc.  
**Assessment Date:** September 2026  
**Lead Assessor:** Junior GRC Analyst (Simulated Engagement)  
**Version:** 1.2 (Updated Profile & Scope Alignment)

---

## 1. Company Overview

**ShopPulse Retail Solutions Inc.** is a growing small-to-medium-sized direct-to-consumer (D2C) and business-to-business (B2B) e-commerce retailer based in Austin, Texas. Founded in 2021, the company specializes in high-end customized apparel, accessories, and promotional lifestyle goods. 

ShopPulse operates a primary e-commerce web storefront for consumer sales alongside a custom B2B bulk-ordering customer portal. Physical inventory is stored across two outsourced third-party logistics (3PL) fulfillment centers located in Texas and Ohio.

* **Industry:** E-Commerce / Specialty Online Retail
* **Headquarters:** Austin, TX (Single corporate office; hybrid remote workforce)
* **Organization Size:** Growing small-to-medium-sized organization
* **Target Audience:** North American consumers & mid-market commercial clients
* **Regulatory Context:** US State Data Privacy Laws (CCPA/CPRA, Texas Data Privacy and Security Act). Payment card processing is offloaded via third-party architecture; exact PCI DSS Self-Assessment Questionnaire (SAQ) classification (e.g., SAQ A vs. SAQ A-EP) requires formal confirmation against PCI DSS v4.0 eligibility criteria and payment flow validation.

---

## 2. Organization Size & Department Structure

ShopPulse employs **45 full-time staff** and engages approximately **15 ongoing contract workers** (primarily support agents and digital marketing contractors) as part of its growing small-to-medium-sized e-commerce organization.

```text
ShopPulse Organizational Hierarchy
├── Executive Management (3) — CEO, CFO, CTO
├── Engineering & IT Operations (8) — IT Manager (1), Software Engineers (5), DevOps/Cloud Engineers (2)
├── E-Commerce Operations & Supply Chain (10) — Logistics Managers, Inventory Leads
├── Marketing & Digital Growth (8) — Growth Leads, Content Creators, SEO Analysts
├── Customer Support (12) — Support Lead (1), Tier-1/Tier-2 Support Agents (11)
└── Finance & Human Resources (4) — Accounting Manager (1), HR Generalist (1), Operations Analysts (2)
```

> **Note on Security Governance:** ShopPulse does not have a dedicated Chief Information Security Officer (CISO) or full-time security staff. Cybersecurity responsibilities are informally delegated to the **IT Manager** and the **Lead DevOps Engineer**.

---

## 3. Business Model & Core Business Processes

ShopPulse generates revenue through high-volume e-commerce transactions. Operational resilience and customer trust depend directly on six core business processes:

1. **Customer Checkout & Payment Processing:** E-commerce customer catalog browsing, cart management, and payment execution (credit cards, Apple Pay, PayPal).
2. **Order Fulfillment & 3PL Logistics Sync:** Real-time API communication between the e-commerce backend and 3PL fulfillment warehouse management systems (WMS).
3. **Customer Account & Portal Management:** Customer authentication, order history lookup, corporate B2B credit line applications, and self-service address updates.
4. **Digital Marketing & Customer Analytics:** Tracked email campaigns, promotional promo code issuance, user behavior analytics, and ad conversion tracking.
5. **Corporate Financial Operations & Payroll:** Merchant payout reconciliation, vendor invoicing, inventory accounting, and employee bi-weekly payroll.
6. **Remote Workforce & Endpoint Management:** Employee provisioning, remote VPN/SaaS access management, email communication, and internal file sharing.

---

## 4. Technology & IT Environment

The technology environment is modern and cloud-native, designed to handle variable web traffic spikes during holiday shopping seasons.

```text
                             [ Web Traffic / Users ]
                                        │
                                        ▼
                             [ AWS Cloud Infrastructure ]
                  ┌─────────────────────┼─────────────────────┐
                  │                                           │
         [ Application Load Balancer ]              [ Amazon S3 Buckets ]
                  │                                 (Static Assets & Backups)
                  ▼                                           │
        [ ECS Container Fleet ] ──────────────────────────────┘
      (React Frontend / Node Backend)
                  │
        ┌─────────┴─────────┐
        ▼                   ▼
[ AWS RDS PostgreSQL ]  [ Stripe API ] (Payment Gateway)
(Customer PII & Orders)     │
                            ▼
                    [ 3PL WMS API ] (Order Dispatch)
```

### Key Infrastructure Components
* **Cloud Platform:** AWS (US-East-1 primary region). Uses ECS (Elastic Container Service) for web containers, ALB (Application Load Balancer), and S3 for media storage and automated DB backups.
* **Database:** AWS RDS PostgreSQL instance housing customer account records, transaction histories, hashed password credentials, and order status data. RDS availability configuration, including Multi-AZ deployment, requires verification.
* **Payment Architecture:** Uses Stripe Elements (iFrame embedding) to significantly reduce internal PCI DSS scope by keeping raw cardholder data off ShopPulse servers. The specific SAQ determination requires formal merchant payment flow validation against PCI DSS v4.0 criteria.
* **Identity & Access Management:** Google Workspace provides corporate identity and SSO for selected SaaS applications. AWS IAM manages cloud access through a combination of IAM users and roles; Some developer IAM users may rely on long-lived static access keys. AWS IAM MFA enforcement and coverage require verification.
* **Employee Endpoints:** 45 corporate laptops (mix of macOS and Windows 11 Pro). Managed via SaaS MDM (Jamf for Mac, Microsoft Intune for Windows).
* **Remote Connectivity:** AWS Client VPN (OpenVPN protocol) for developer access to private VPC subnets.
* **Logging & Monitoring:** Default AWS CloudWatch metrics and container logs (retained for 14 days). No centralized SIEM or security operational logging tool currently deployed.

---

## 5. Types of Data Handled & Data Classification

ShopPulse handles four primary categories of sensitive organizational data:

| Data Category | Examples | Primary Location | Data Classification | Regulatory Context |
| :--- | :--- | :--- | :--- | :--- |
| **Customer PII** | Full names, shipping/billing addresses, email addresses, phone numbers, password hashes (Bcrypt). | AWS RDS PostgreSQL, Zendesk CRM | **Confidential** | CCPA/CPRA, Texas Data Privacy and Security Act |
| **Payment Data** | Stripe payment tokens, last four digits of payment cards, merchant transaction references. | Stripe (Tokenized), AWS RDS (Tokens/Last 4) | **Restricted** | PCI DSS (Scope evaluated based on payment architecture) |
| **Employee & HR Data** | Social Security Numbers (SSNs), tax forms (W-2/1099), direct deposit banking details, salary records. | QuickBooks Payroll, HR Drive | **Confidential** | US State Privacy Laws, Financial Privacy Regulations |
| **Corporate Operational Data** | Web application source code, supplier pricing contracts, inventory forecasts, API integration keys. | GitHub Private Repos, AWS Secrets Manager, Google Drive | **Internal / Restricted** | Commercial Trade Secret & Proprietary Governance |

> **PCI DSS Scope Note:** PCI DSS scope applies to systems, processes, and data flows based on the actual payment architecture rather than simply because a data item is financial. Stripe tokenization prevents Primary Account Numbers (PANs) from traversing internal servers.

---

## 6. Important Assets & Third-Party Dependencies

### Key Internal Assets
* `AST-01`: E-Commerce Web Storefront & Customer Portal (AWS ECS)
* `AST-02`: Production Database (AWS RDS PostgreSQL)
* `AST-03`: Corporate Endpoint Fleet (45 Laptops: macOS / Windows 11)
* `AST-04`: Application Source Code & CI/CD Pipeline (GitHub Enterprise)
* `AST-05`: Cloud Infrastructure Management Environment (AWS IAM / Console)

### Critical Third-Party Services & Dependencies
* `VND-01` **Stripe Payment Gateway:** Handles credit card processing, payment tokenization, and fraud prevention.
* `VND-02` **Amazon Web Services (AWS):** Core cloud infrastructure host (compute, database, network, storage).
* `VND-03` **Zendesk Support SaaS:** Handles customer service communications, ticketing, and support history.
* `VND-04` **3PL Logistics Provider(s):** Provides warehouse management and order fulfillment API integration.
* `VND-05` **Google Workspace:** Corporate email, document collaboration, and internal communication (Google Meet/Chat).

---

## 7. Current Security Posture & Assumptions

### Current Controls (Baseline Strengths)
* All web application traffic is strictly encrypted using TLS 1.3 in transit.
* Payment tokenization via Stripe Elements reduces internal PCI DSS scope by avoiding raw payment card storage on internal servers.
* Google Workspace requires Multi-Factor Authentication (MFA) for corporate email logins.
* Production databases run in private subnets with network security groups blocking direct public internet access.
* Daily automated snapshot backups of AWS RDS are configured.

### Known Weaknesses & Operational Realities (Gaps)
* **No Formal Security Governance:** Lack of dedicated security staff; no documented Information Security Policy framework.
* **IAM & MFA Gaps:** Some developer IAM users may rely on long-lived static access keys. AWS IAM MFA enforcement and coverage require verification.
* **Patching & Vulnerability Management:** Dependency vulnerability scanning is informal; no scheduled vulnerability assessment cadence is documented.
* **Insufficient Logging & Monitoring:** AWS CloudWatch logs are retained for 14 days; no centralized SIEM or security operational logging platform is currently deployed.1
* **Third-Party Risk Management (TPRM):** Third-party vendor security posture and assurance evidence are not systematically reviewed before onboarding.
* **Incident Response & DR:** No documented Incident Response Plan (IRP) or disaster recovery testing standard exists.

---

## 8. Assessment Scope & Objectives

### In-Scope Boundaries
* All production cloud environments hosted within ShopPulse AWS accounts (US-East-1).
* E-Commerce Web Application, API endpoints, and RDS Database infrastructure.
* Corporate employee endpoint laptops (macOS and Windows 11).
* Key vendor integrations (Stripe, 3PL API, Zendesk, Google Workspace).
* Administrative workflows, password policies, and access management practices.

### Out-of-Scope
* Physical security of 3PL fulfillment warehouse locations (managed by 3PL vendor contract).
* Stripe's underlying infrastructure and payment-processing environment are outside ShopPulse's assessment boundary. Relevant Stripe compliance and assurance documentation would be treated as third-party evidence where applicable.

### Assessment Objectives
1. Perform an asset inventory classification based on CIA impact levels.
2. Conduct a structured cybersecurity risk assessment identifying realistic threats, vulnerabilities, and business impacts.
3. Assess control maturity against ISO/IEC 27001:2022 framework control objectives.
4. Map identified risks and security controls to the 6 core functions of NIST CSF 2.0.
5. Deliver a practical Risk Treatment Plan, executive GRC assessment report, and prioritized 0-180 day Remediation Roadmap.
