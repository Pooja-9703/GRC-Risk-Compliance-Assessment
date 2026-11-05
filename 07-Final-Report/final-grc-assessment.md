# Comprehensive Cybersecurity Risk & Compliance Assessment Report

**Target Organization:** ShopPulse Retail Solutions Inc.  
**Engagement Type:** Simulated Junior GRC Analyst Portfolio Project  
**Framework Baselines:** ISO/IEC 27001:2022 | NIST Cybersecurity Framework (CSF) 2.0 | ISO 31000 / NIST SP 800-30  
**Author:** Junior Cybersecurity GRC Analyst Candidate  
**Date:** September 2026  
**Version:** 1.2 (Final Synchronized Deliverable)  

---

## 1. Executive Summary

### Executive Business Context
**ShopPulse Retail Solutions Inc.** is a growing small-to-medium-sized direct-to-consumer (D2C) and business-to-business (B2B) e-commerce retailer operating a cloud-native web platform hosted on Amazon Web Services (AWS). This simulated **Governance, Risk, and Compliance (GRC)** assessment evaluates the company's cybersecurity risk posture, technology infrastructure, business data flows, and alignment with international security standards.

### Overall Security Posture Summary
The assessment evaluated **10 primary technology assets**, **10 realistic threat scenarios**, **13 key ISO/IEC 27001:2022 Annex A controls**, and mapped capabilities across the **six core functions of NIST CSF 2.0**.

ShopPulse maintains several foundational security strengths:
* Customer payment processing is integrated via Stripe Elements iFrames, significantly reducing internal PCI DSS scope by avoiding raw payment card storage on company servers.
* Web application communications are strictly encrypted using TLS 1.3 in transit.
* Production databases reside in private cloud subnets with encrypted storage at rest (AWS KMS AES-256).
* Corporate email logins require mandatory Multi-Factor Authentication (MFA).

However, significant security governance and operational control gaps leave ShopPulse vulnerable to credential compromise, cloud data exposure, and undetected incident persistence.

### Key Risk Assessment Metrics
* **Total Risks Evaluated:** 10 Scenarios (`RSK-01` through `RSK-10`)
* **Inherent Risk Distribution:** 1 Critical (10%), 9 High (90%)
* **Current Residual Risk Distribution:** 0 Critical (0%), 5 High (50%), 5 Medium (50%), 0 Low (0%)
* **ISO 27001 Implementation Maturity:** 1 Implemented (8%), 8 Partially Implemented (61%), 4 Not Implemented (31%)

```text
Current Residual Risk Severity Breakdown
┌────────────────────────────────────────────────────────┐
│ [Critical: 0%]  None                                   │
│ [High: 50%]     RSK-01, RSK-02, RSK-03, RSK-05, RSK-06  │
│ [Medium: 50%]   RSK-04, RSK-07, RSK-08, RSK-09, RSK-10  │
└────────────────────────────────────────────────────────┘
```

### Top Priority Management Action Items
1. **Immediate (0–30 Days):** Enforce mandatory Multi-Factor Authentication (MFA) on all AWS IAM accounts, transition to centralized SSO with short-lived tokens, and apply cloud storage access controls (`ACT-01`, `ACT-02`).
2. **Medium-Term (31–90 Days):** Deploy Web Application Firewall (WAF) rules, implement HTTP Content Security Policy (CSP) headers, establish requirement-based security log retention and centralized monitoring, refactor code to parameterized database queries, enforce MDM endpoint disk encryption, and publish written Information Security Policies (`ACT-03` to `ACT-08`).
3. **Long-Term (91–180 Days):** Perform a Business Impact Analysis (BIA) for cross-region disaster recovery and formalize risk-based Third-Party Risk Management (TPRM) (`ACT-09`, `ACT-10`).

---

## 2. Organization Overview

**ShopPulse Retail Solutions Inc.** employs 45 full-time staff and 15 contractors, operating from a corporate headquarters in Austin, Texas, alongside a distributed remote workforce. Physical merchandise fulfillment is outsourced to two third-party logistics (3PL) warehouses in Texas and Ohio.

| Department | Headcount | Primary Operational Responsibility | Key Technology Systems |
| :--- | :---: | :--- | :--- |
| **Executive Management** | 3 | Strategic leadership, financial oversight, governance | Corporate Email, Financial Ledgers |
| **Engineering & IT** | 8 | Platform development, cloud infrastructure, IT support | AWS Cloud, GitHub Enterprise, Jamf/Intune |
| **E-Commerce & Supply Chain** | 10 | Order fulfillment, inventory management, 3PL sync | 3PL WMS Integration API |
| **Marketing & Growth** | 8 | Customer acquisition, digital ad campaigns, analytics | Google Workspace, Analytics SaaS |
| **Customer Support** | 12 | Customer inquiries, ticket resolution, order lookup | Zendesk SaaS |
| **Finance & HR** | 4 | Accounting, payroll, personnel management | QuickBooks Online, Payroll SaaS |

> **Security Governance Structure:** ShopPulse does not employ a dedicated Chief Information Security Officer (CISO) or full-time security team. Cybersecurity responsibilities are informally shared between the **IT Manager** and the **Lead DevOps Engineer**.

---

## 3. Assessment Scope & Objectives

### In-Scope Operational Boundaries
* All production cloud infrastructure hosted in ShopPulse AWS accounts (US-East-1 region).
* E-Commerce Web Storefront, customer portal, and production RDS PostgreSQL database.
* Corporate employee endpoint fleet (45 laptops: macOS and Windows 11 Pro).
* Third-party SaaS tools (Google Workspace, Zendesk, QuickBooks Online, GitHub Enterprise).
* Critical API integration touchpoints (Stripe Payment Gateway, 3PL Warehouse API).

### Out-of-Scope Boundaries
* Physical security controls of outsourced 3PL fulfillment warehouse facilities (governed by 3PL contract SLAs).
* Stripe PCI DSS physical and application data center infrastructure.

### Primary Engagement Objectives
1. Perform an asset inventory classification based on business impact levels across Confidentiality, Integrity, and Availability.
2. Conduct a cybersecurity risk assessment identifying threats, vulnerabilities, and business impacts.
3. Evaluate control maturity against ISO/IEC 27001:2022 Annex A control objectives.
4. Map cybersecurity capabilities and gaps to the core functions of NIST CSF 2.0.
5. Deliver a Risk Treatment Plan and prioritized 0–180 day Remediation Roadmap.

---

## 4. Assessment Methodology

The assessment utilizes a semi-quantitative **5x5 Risk Matrix** aligned with international risk standards (**ISO 31000** and **NIST SP 800-30 Rev. 1**).

$$\text{Risk Score} = \text{Likelihood Rating (1--5)} \times \text{Impact Rating (1--5)}$$

### Scoring Scale Definitions
* **Likelihood (1–5):** 1 (Rare), 2 (Unlikely), 3 (Possible), 4 (Likely), 5 (Almost Certain).
* **Impact (1–5):** 1 (Negligible), 2 (Minor), 3 (Moderate), 4 (Major), 5 (Catastrophic) across Financial, Operational, Regulatory, and Reputational vectors.

### Severity Rating Thresholds

| Risk Score Range | Severity Level | Escalation & Response Guidance |
| :---: | :--- | :--- |
| **17 – 25** | **Critical** | Immediate executive escalation; remediation required within 0–30 days. |
| **10 – 16** | **High** | Prompt management attention; formal remediation within 31–90 days. |
| **5 – 9** | **Medium** | Planned operational remediation within 91–180 days. |
| **1 – 4** | **Low** | Acceptable operational risk; monitor during routine maintenance cycles. |

---

## 5. Asset & Data Overview

ShopPulse operates **10 primary technology assets** categorized under four data classification tiers:

| Asset ID | Asset Name | Asset Type | Data Classification | CIA Impact (C-I-A) | Overall Criticality | Primary Business Dependency |
| :--- | :--- | :--- | :--- | :---: | :---: | :--- |
| **AST-01** | E-Commerce Web Storefront | Software / App | Internal | M-H-H | **Critical** | AWS ECS, RDS Database, Stripe API |
| **AST-02** | Production RDS PostgreSQL DB | Data / Database | Confidential | H-H-H | **Critical** | Customer PII & Order History |
| **AST-03** | Corporate Endpoint Fleet (45 Laptops) | Endpoints | Confidential | H-M-M | **High** | Staff Workstations & Remote Access |
| **AST-04** | GitHub Private Code Repositories | Software / Repo | Restricted | H-H-M | **High** | Application Source Code & CI/CD |
| **AST-05** | AWS IAM & Cloud Control Plane | Cloud Infra | Restricted | H-H-H | **Critical** | Cloud Infrastructure Governance |
| **AST-06** | Google Workspace Suite | SaaS / Email | Confidential | H-M-M | **High** | Corporate Communications & Files |
| **AST-07** | Stripe Payment Gateway API | SaaS / Payment | Restricted | H-H-H | **Critical** | Credit Card Checkout Tokenization |
| **AST-08** | 3PL Warehouse Management API | Third-Party API | Internal | M-H-M | **High** | Automated Order Dispatch Sync |
| **AST-09** | Zendesk Support System | SaaS / Support | Confidential | M-M-M | **Medium** | Customer Support Tickets |
| **AST-10** | QuickBooks Online & Payroll | SaaS / Finance | Confidential | H-H-M | **High** | Corporate Financial Ledgers & Payroll |

> **Regulatory & Compliance Context Note:** Payment processing is integrated via Stripe Elements iFrames to minimize internal PCI DSS scope. Asset criticality ratings reflect business impact rather than strict CIA mechanical sums.

---

## 6. Risk Assessment Summary

The risk evaluation identified ten primary risk scenarios (`RSK-01` to `RSK-10`). Baseline controls mitigate raw inherent risk, but significant residual exposure remains across cloud access control, security monitoring, and web application hardening.

| Risk ID | Asset ID | Threat Scenario | Inherent (L×I) | Inherent Rating | Existing Baseline Controls | Residual (L×I) | Residual Rating | Primary Treatment |
| :--- | :--- | :--- | :---: | :---: | :--- | :---: | :---: | :---: |
| **RSK-01** | AST-05 | Compromise of static developer AWS IAM access keys via phishing or leak. | 4 × 5 | **20 (Critical)** | Console IP restriction via AWS Client VPN. | 3 × 5 | **15 (High)** | **Mitigate** |
| **RSK-02** | AST-02, AST-05 | Potential misconfiguration and public exposure of S3 backup buckets. | 3 × 5 | **15 (High)** | AWS SSE-S3 encryption; AWS GuardDuty enabled. | 2 × 5 | **10 (High)** | **Mitigate** |
| **RSK-03** | AST-01, AST-07 | Threat actor exploits XSS or potentially vulnerable application dependencies to manipulate the checkout page and attempt to capture user inputs prior to Stripe payment-field submission. | 4 × 4 | **16 (High)** | Stripe Elements iFrame isolation; TLS 1.3 encryption. | 3 × 4 | **12 (High)** | **Mitigate** |
| **RSK-04** | AST-03, AST-06 | Spear-phishing targeting remote workforce for email credentials. | 4 × 3 | **12 (High)** | Google Workspace enforced MFA; spam filtering. | 3 × 3 | **9 (Medium)** | **Mitigate** |
| **RSK-05** | AST-01, AST-05 | Insufficient security incident logging & real-time alert monitoring. | 4 × 4 | **16 (High)** | GuardDuty enabled; CloudWatch logs retained for 14 days. | 3 × 4 | **12 (High)** | **Mitigate** |
| **RSK-06** | AST-02, AST-01 | Threat actor exploits an unauthenticated backend API route or potential injection weakness in legacy reporting modules to exfiltrate customer PII from the production database. | 3 × 5 | **15 (High)** | RDS in private VPC subnet; KMS storage encryption. | 2 × 5 | **10 (High)** | **Mitigate** |
| **RSK-07** | AST-08, AST-09 | Third-party vendor breach or compromise of shared 3PL integration API keys. | 3 × 3 | **9 (Medium)** | HTTPS API transport; 3PL NAT IP whitelisting. | 2 × 3 | **6 (Medium)** | **Mitigate** |
| **RSK-08** | AST-03 | Data exposure risk via unenforced endpoint disk encryption on laptops. | 4 × 3 | **12 (High)** | MDM enrollment; remote wipe capability; startup password. | 2 × 3 | **6 (Medium)** | **Mitigate** |
| **RSK-09** | AST-02, AST-01 | Prolonged downtime risk from limited disaster recovery readiness. | 3 × 4 | **12 (High)** | Automated daily RDS snapshots; snapshot retention, restoration procedures, recovery objectives, and restoration testing require verification. | 2 × 4 | **8 (Medium)** | **Mitigate** |
| **RSK-10** | AST-01 to AST-10 | Employee security misconfigurations due to lack of written policies. | 4 × 3 | **12 (High)** | Verbal onboarding instructions; password length rule (8+ chars). | 3 × 3 | **9 (Medium)** | **Mitigate** |

---

## 7. Top Risk Findings

### Finding 1: Static AWS IAM Access Keys & Unverified MFA Enforcement (`RSK-01`)
* **Risk Level:** **High Residual Risk (Score 15)**
* **Root Cause:** Some developer IAM users may rely on long-lived static access keys. IAM MFA enforcement policy and coverage require verification, and static keys bypass console IP restrictions.
* **Business Impact:** Potential cloud administrative access compromise, unauthorized configuration changes, or cloud data exposure.

### Finding 2: Short Log Retention & Unverified Security Alert Routing (`RSK-05`)
* **Risk Level:** **High Residual Risk (Score 12)**
* **Root Cause:** Default CloudWatch log retention is limited to 14 days, and GuardDuty alert routing, triage, and escalation procedures require verification.
* **Business Impact:** Reduced capability to conduct historical incident investigations or detect persistent intruder activity.

### Finding 3: Application Dependency Hardening & DOM Tampering Exposure (`RSK-03`)
* **Risk Level:** **High Residual Risk (Score 12)**
* **Root Cause:** Potential application dependency vulnerabilities or DOM tampering risks prior to Stripe iFrame form submission require automated scanning and protective headers.
* **Business Impact:** Potential manipulation of the checkout page attempting to capture user input prior to payment tokenization.

---

## 8. ISO/IEC 27001:2022 Gap Assessment Summary

Evaluating ShopPulse against 13 Annex A controls revealed a **Control Maturity Gap** characterized by informal technical controls and absent administrative governance.

```text
ISO 27001:2022 Implementation Status Summary
┌────────────────────────────────────────────────────────┐
│ Implemented (8%):            A.8.24                    │
│ Partially Implemented (61%): A.5.15, A.5.23, A.7.4,    │
│                              A.8.5, A.8.7, A.8.8,      │
│                              A.8.9, A.8.12             │
│ Not Implemented (31%):       A.5.1, A.5.19, A.6.8, A.8.16│
└────────────────────────────────────────────────────────┘
```

| Control Ref | Control Theme | Control Name | Status | Key Identified Gap | Priority |
| :--- | :--- | :--- | :---: | :--- | :---: |
| **A.5.1** | Organizational | Policies for Information Security | **Not Implemented** | Absence of written Information Security Policies (AUP, Access, Data). | Medium |
| **A.5.15** | Organizational | Access Control | **Partially Implemented** | IAM MFA enforcement coverage and key management require verification. | High |
| **A.5.19** | Organizational | Supplier Security Relationships | **Not Implemented** | Absence of risk-based Third-Party Risk Management (TPRM) policy. | Medium |
| **A.5.23** | Organizational | Security for Cloud Services | **Partially Implemented** | Account-level S3 block public access guardrails require verification. | High |
| **A.6.8** | People | Security Awareness & Training | **Not Implemented** | Formal security awareness and anti-phishing training require verification. | Medium |
| **A.7.4** | Physical | Physical Security Monitoring | **Partially Implemented** | Headquarter office physical access controls active; 3PL facilities outsourced. | Low |
| **A.8.5** | Technological | Secure Authentication | **Partially Implemented** | Centralized SSO and MFA enforcement for cloud administration require verification. | High |
| **A.8.7** | Technological | Protection Against Malware | **Partially Implemented** | Endpoint OS anti-malware active via Jamf/Intune MDM; verification needed. | Low |
| **A.8.8** | Technological | Vulnerability Management | **Partially Implemented** | Automated dependency scanning and SAST in CI/CD pipelines require verification. | High |
| **A.8.9** | Technological | Configuration Management | **Partially Implemented** | Automated cloud configuration drift monitoring requires verification. | High |
| **A.8.12** | Technological | Data Leakage Prevention | **Partially Implemented** | Full-disk encryption policy enforcement on laptops requires MDM verification. | Medium |
| **A.8.16** | Technological | Monitoring Activities | **Not Implemented** | 14-day log retention; alert routing and escalation require verification. | High |
| **A.8.24** | Technological | Use of Cryptography | **Implemented** | TLS 1.3 in transit; RDS KMS AES-256 at rest; password hashing implemented. | Low |

---

## 9. NIST CSF 2.0 Assessment Summary

The alignment matrix maps ShopPulse capabilities across the **Six Core Functions** of NIST CSF 2.0:

| NIST Function | Subcategory Code | Title / Focus Area | Current Posture & Identified Gap | Related Risk | Priority |
| :--- | :--- | :--- | :--- | :---: | :---: |
| **GOVERN** | `GV.PO-01` | Policy Framework | Absence of written Information Security Policy suite. | RSK-10 | Medium |
| **GOVERN** | `GV.RM-01` | Risk Strategy | Informal risk reviews without continuous risk policy. | RSK-09, RSK-10 | Medium |
| **GOVERN** | `GV.SC-01` | Supply Chain Risk | Lack of formal risk-based TPRM process and vendor assurance evidence. | RSK-07 | Medium |
| **IDENTIFY** | `ID.AM-01` | Asset Management | Cloud asset tagging and endpoint encryption enforcement require verification. | RSK-02, RSK-08 | Medium |
| **IDENTIFY** | `ID.RA-01` | Vulnerability Scanning | GitHub repositories lack automated dependency scanning and SAST. | RSK-03, RSK-06 | High |
| **PROTECT** | `PR.AA-01` | Identity & Access Control | AWS IAM is used for cloud admin; static keys and MFA coverage require verification. | RSK-01 | High |
| **PROTECT** | `PR.AT-01` | Awareness & Training | Security awareness and anti-phishing training completion status require verification. | RSK-04 | Medium |
| **PROTECT** | `PR.DS-01` | Data Security | Endpoint full-disk encryption enforcement requires verification in MDM. | RSK-06, RSK-08 | High |
| **PROTECT** | `PR.PS-01` | Platform Security | Deployment of WAF rules, CSP headers, and S3 block public access requires verification. | RSK-02, RSK-03 | High |
| **DETECT** | `DE.CM-01` | Continuous Monitoring | CloudWatch retention limited to 14 days; alert routing requires verification. | RSK-05 | High |
| **RESPOND** | `RS.MA-01` | Incident Management | No written Incident Response Plan (IRP) or defined escalation roles. | RSK-05, RSK-10 | High |
| **RECOVER** | `RC.RP-01` | Recovery Planning | Single-region backup reliance; DR recovery objectives and testing require verification. | RSK-09 | Medium |

---

## 10. Risk Treatment Summary

All 10 risks are assigned a **Primary Treatment Decision (`Mitigate`)**. Supplementary risk-financing and residual risk acceptance decisions are defined as follows:

1. **Risk Mitigation (Technical & Administrative Safeguards):** Applied to all technical control gaps (`RSK-01` to `RSK-10`) to lower likelihood and impact.
2. **Risk Financing (Cyber Liability Insurance Evaluation):** Evaluated under `RSK-04` (Spear-Phishing/BEC) to evaluate financial exposure from BEC fraud.
3. **Residual Risk Acceptance (Vendor Contract SLAs):** Applied under `RSK-07` (3PL Vendor API Keys), where residual third-party breach exposure outside ShopPulse direct control is managed based on 3PL contractual inventory SLAs.

---

## 11. Prioritized Remediation Roadmap

Remediation activities are structured into three phased implementation tranches:

```text
Remediation Schedule Phasing
├── Phase 1: 0–30 Days  (Short-Term)  ──► IAM MFA, Centralized SSO & S3 Block Public Access
├── Phase 2: 31–90 Days (Medium-Term) ──► WAF, CSP, Log Retention, Parameterized Queries, Policies & MDM FDE
└── Phase 3: 91–180 Days (Long-Term)  ──► Strategic Governance, TPRM & Disaster Recovery BIA
```

| Action ID | Target Timeframe | Action Title & Description | Responsible Role | Priority | ISO 27001 | NIST CSF 2.0 |
| :--- | :---: | :--- | :--- | :---: | :---: | :---: |
| **ACT-01** | **0–30 Days** | **AWS IAM MFA Enforcement & SSO Migration:** Enforce mandatory IAM MFA; rotate static keys; configure centralized SSO with short-lived tokens. | CTO / IT Manager | **High** | A.5.15, A.8.5 | PR.AA-01 |
| **ACT-02** | **0–30 Days** | **AWS Storage Guardrails & Access Control Configuration:** Enable Account-Level Block Public Access across S3 buckets; deploy configuration drift monitoring rules. | Lead DevOps Engineer | **High** | A.5.23, A.8.9 | ID.AM-01, PR.PS-01 |
| **ACT-03** | **31–90 Days** | **Web Application Hardening & Vulnerability Management:** Deploy WAF rules, configure strict HTTP CSP headers, and integrate automated SAST/dependency scanning. | Lead Software Engineer | **High** | A.8.8, A.8.24 | ID.RA-01, PR.PS-01 |
| **ACT-04** | **31–90 Days** | **Workforce Security Awareness Training & Cyber Insurance Evaluation:** Launch web-based awareness training platform; evaluate commercial cyber liability insurance options. | HR Generalist / IT | **Medium** | A.6.8, A.8.5 | PR.AT-01 |
| **ACT-05** | **31–90 Days** | **Requirement-Based Log Retention & Centralized Security Alerting:** Define security-log retention requirements; aggregate logs; establish alert routing and escalation channels. | IT Manager / DevOps | **High** | A.8.16 | DE.CM-01 |
| **ACT-06** | **31–90 Days** | **Database Code Refactoring & Automated Secrets Rotation:** Replace raw SQL queries with parameterized statements; migrate database credentials to secrets manager with automated rotation. | Lead Software Eng / CTO | **High** | A.5.15 | ID.RA-01, PR.DS-01 |
| **ACT-07** | **31–90 Days** | **Endpoint Full-Disk Encryption Policy Enforcement:** Enforce mandatory FileVault and BitLocker disk encryption across laptops via MDM policies. | IT Manager | **Medium** | A.8.12 | ID.AM-01, PR.DS-01 |
| **ACT-08** | **31–90 Days** | **Information Security Policy Suite Publication:** Draft, approve, and publish core security policies (AUP, Access Control, Data Protection); mandate annual employee sign-off. | IT Manager / HR | **Medium** | A.5.1 | GV.PO-01 |
| **ACT-09** | **91–180 Days** | **Third-Party Risk Management (TPRM) & Integration Key Rotation:** Establish risk-based TPRM process; store API keys in secret manager; execute annual key rotation. | Operations Manager / IT | **Medium** | A.5.19 | GV.SC-01 |
| **ACT-10** | **91–180 Days** | **Business Impact Analysis (BIA) & Disaster Recovery Replication:** Perform BIA to set RTO/RPO; evaluate and configure cross-region backup replication; conduct drill. | Lead DevOps Engineer | **Medium** | A.5.23 | GV.RM-01, RC.RP-01 |

---

## 12. Management Recommendations

Executive leadership at ShopPulse Retail Solutions Inc. should approve the following strategic recommendations:
1. **Authorize Immediate IAM Identity Safeguards:** Require all cloud administrative access to utilize MFA and short-lived credentials within 30 days.
2. **Establish Written Security Governance:** Formally approve the Information Security Policy suite to define employee operational boundaries.
3. **Invest in Detection & Resilience Infrastructure:** Establish requirement-based security log retention, centralized security monitoring, and authorize a Business Impact Analysis (BIA) for disaster recovery planning.

---

## 13. Assumptions, Limitations & Portfolio Disclaimer

> **IMPORTANT PORTFOLIO DISCLAIMER:**  
> This GRC assessment report is a **simulated portfolio project** created by a Computer Science student targeting entry-level Cybersecurity Analyst and GRC Analyst roles.  
> 
> * **Fictional Entity:** ShopPulse Retail Solutions Inc. is a fictional e-commerce organization.
> * **Non-Audit Declaration:** This deliverable does **not** represent an actual audit, formal ISO 27001 certification, PCI DSS attestation of compliance, or commercial consulting engagement.
> * **Ground-Truth Basis:** All findings, risk scores, and recommendations are derived strictly from documented current-state specifications and analytical assumptions defined within this portfolio project.
