# Deliverable 7: Prioritized Security Remediation Roadmap

**Organization:** ShopPulse Retail Solutions Inc.  
**Assessor:** Junior GRC Analyst (Simulated Engagement)  
**Derivation:** Derived strictly from Phase 5 Risk Treatment Plan (`RSK-01` to `RSK-10`)  
**Version:** 1.1 (Updated Control Terminology & Governance Objectives)  

---

## 1. Executive Overview & Roadmap Strategy

> **Portfolio & Ground-Truth Disclaimer:** This document represents a simulated security remediation roadmap created for portfolio demonstration purposes. It outlines a proposed 0–180 day implementation schedule based on documented risk priorities and governance objectives. It does **not** imply that formal executive approvals, vendor contract modifications, or technical deployment milestones have actually been executed.

The **Prioritized Security Remediation Roadmap** translates the Risk Treatment Plan into a practical, phased implementation schedule for **ShopPulse Retail Solutions Inc.**

Remediation activities are organized into **Three Phased Tranches** based on residual risk severity, business impact, and technical implementation dependencies:

```text
Remediation Schedule Phasing
├── Phase 1: 0–30 Days  (Short-Term)  ──► ACT-01 (IAM MFA/SSO), ACT-02 (Storage Guardrails)
├── Phase 2: 31–90 Days (Medium-Term) ──► ACT-03 (Web App Hardening), ACT-04 (Training), ACT-05 (Logs/SIEM), 
│                                          ACT-06 (DB SQLi/Secrets), ACT-07 (Disk Encryption), ACT-08 (Policies)
└── Phase 3: 91–180 Days (Long-Term)  ──► ACT-09 (TPRM/Vendor Keys), ACT-10 (BIA/DR Replication)
```

---

## 2. Master Remediation Roadmap Table

| Action ID | Timeframe | Related Risk ID | Action Title & Description | Business & Security Objective | Priority | Responsible Role | ISO 27001 Mapping | NIST CSF 2.0 Mapping | Technical & Governance Dependencies | Expected Security Outcome | Status |
| :--- | :---: | :---: | :--- | :--- | :---: | :--- | :---: | :---: | :--- | :--- | :---: |
| **ACT-01** | **0–30 Days** | RSK-01 | **AWS IAM MFA Enforcement & SSO Migration:** Enforce mandatory MFA on all IAM accounts; rotate static keys; configure SSO with temporary tokens. | Eliminate static un-MFA'd cloud administrator credential compromise. | **Critical** | CTO / IT Manager | A.5.15, A.8.5 | PR.AA-01 | AWS IAM Admin Console access; Google Workspace IdP link. | Complete elimination of long-lived un-MFA'd static cloud access keys. | Proposed |
| **ACT-02** | **0–30 Days** | RSK-02 | **AWS Storage Guardrails & Access Control Configuration:** Enable Account-Level Block Public Access across all S3 buckets; deploy automated drift monitoring rules. | Prevent unauthorized public S3 access through appropriate access controls and cloud guardrails. | **High** | Lead DevOps Engineer | A.5.23, A.8.9 | ID.AM-01, PR.PS-01 | AWS Cloud account root administrative permissions. | Automated cloud guardrails preventing unauthorized public S3 bucket access. | Proposed |
| **ACT-03** | **31–90 Days** | RSK-03 | **Web Application Hardening & Vulnerability Management:** Deploy WAF rules, configure strict HTTP CSP headers, and integrate Dependabot SAST scanning. | Reduce web application and client-side injection risk through vulnerability management, secure configuration, and web application protections. | **High** | Lead Software Engineer | A.8.8, A.8.24 | ID.RA-01, PR.PS-01 | AWS ALB load balancer access; GitHub Actions pipeline edit rights. | Automated dependency vulnerability patching and web application injection protection. | Proposed |
| **ACT-04** | **31–90 Days** | RSK-04 | **Workforce Security Awareness Training & Cyber Insurance Evaluation:** Launch web-based phishing training platform; evaluate cyber insurance options. | Reduce employee susceptibility to spear-phishing and evaluate risk-financing coverage for wire fraud. | **Medium** | HR Generalist / IT Manager | A.6.8, A.8.5 | PR.AT-01 | Employee roster list; executive risk appetite guidelines. | Trained hybrid workforce and executive evaluation of risk-financing coverage. | Proposed |
| **ACT-05** | **31–90 Days** | RSK-05 | **Immutable Log Archiving & Centralized Security Alerting:** Configure 365-day log retention; aggregate logs; route real-time alerts to Slack/PagerDuty. | Ensure forensic audit trail availability and reduce incident detection dwell time. | **High** | IT Manager / Lead DevOps | A.8.16 | DE.CM-01, DE.AE | ACT-02 storage policy; cloud log stream configuration. | 365-day immutable log storage and real-time alert escalation channels. | Proposed |
| **ACT-06** | **31–90 Days** | RSK-06 | **Database Code Refactoring & Automated Secrets Rotation:** Replace raw SQL queries with parameterized statements; migrate DB keys to secrets manager. | Eliminate application-layer SQL injection vectors and plain-text container database credentials. | **High** | Lead Software Eng / CTO | A.5.15, A.8.12 | ID.RA-01, PR.DS-01 | Source code repository write access; secrets manager service provisioning. | Fully parameterized query architecture and automated database password rotation. | Proposed |
| **ACT-07** | **31–90 Days** | RSK-08 | **Endpoint Full-Disk Encryption Policy Enforcement:** Mandate FileVault/BitLocker disk encryption across all 45 laptops via MDM profiles. | Prevent physical data extraction from stolen or lost employee workstations. | **Medium** | IT Manager | A.8.12 | ID.AM-01, PR.DS-01 | Jamf Pro / Microsoft Intune MDM tenant administrative access. | 100% verified full-disk encryption enforcement across all corporate endpoints. | Proposed |
| **ACT-08** | **31–90 Days** | RSK-10 | **Information Security Policy Suite Publication:** Draft, approve, and publish core security policies (AUP, Access, Data Handling); mandate sign-off. | Establish formal security governance and define clear operational boundaries for staff. | **Medium** | IT Manager / HR Generalist | A.5.1 | GV.PO-01 | Executive CTO/CEO approval; internal document portal publishing. | Executive-approved security policy suite with documented employee sign-offs. | Proposed |
| **ACT-09** | **91–180 Days** | RSK-07 | **Third-Party Risk Management (TPRM) & Integration Key Rotation:** Establish vendor vetting policy; store API keys in secret manager; rotate annually. | Mitigate third-party supply chain compromise and unmonitored vendor API access. | **Medium** | Operations Manager / IT | A.5.19 | GV.SC-01 | Vendor inventory contract list; secret manager configuration. | Formalized vendor SOC 2 review process and annual API key rotation schedule. | Proposed |
| **ACT-10** | **91–180 Days** | RSK-09 | **Business Impact Analysis (BIA) & Disaster Recovery Replication:** Perform BIA to set RTO/RPO; enable cross-region database replication; conduct drill. | Ensure rapid business recovery and operational resilience during cloud region outages. | **Medium** | Lead DevOps Engineer | A.5.23 | GV.RM-01, RC.RP-01 | Executive BIA approval; secondary AWS region (US-West-2) setup. | Executive-approved RTO/RPO targets and validated cross-region DR failover. | Proposed |

---

## 3. Phased Implementation Breakdown

### Phase 1: 0–30 Days (Immediate High-Priority Actions)
* **Focus:** Eliminate immediate critical security vulnerabilities in cloud identity access and data storage guardrails.
* **Key Deliverables:**
  1. `ACT-01`: Deploy AWS IAM policy enforcing mandatory MFA for all cloud access; rotate stale developer access keys >90 days old; initialize transition to AWS IAM Identity Center (SSO).
  2. `ACT-02`: Enable AWS Account-Level Block Public Access across the cloud tenant to prevent unauthorized public storage bucket access through appropriate access controls and cloud guardrails.

---

### Phase 2: 31–90 Days (Core Technical & Policy Remediation)
* **Focus:** Harden web application defenses, centralize security logging, enforce endpoint encryption, and establish written security governance policies.
* **Key Deliverables:**
  1. `ACT-03`: Provision Web Application Firewall (WAF) rules, configure strict HTTP CSP headers, and integrate automated dependency security scanning to reduce web application and client-side injection risk.
  2. `ACT-04`: Launch web-based security awareness training platform and evaluate commercial cyber liability insurance coverage with financial advisors.
  3. `ACT-05`: Establish 365-day log retention in immutable storage and configure real-time alert routing to Slack/PagerDuty channels.
  4. `ACT-06`: Refactor legacy raw SQL database queries to parameterized statements and migrate database passwords to a secret manager with 90-day automatic rotation.
  5. `ACT-07`: Enforce mandatory FileVault (macOS) and BitLocker (Windows 11) full-disk encryption policies via Jamf/Intune MDM.
  6. `ACT-08`: Publish executive-approved Information Security Policy suite (AUP, Access Control, Data Protection) and collect employee sign-offs.

---

### Phase 3: 91–180 Days (Strategic Governance, DR & Supply Chain Controls)
* **Focus:** Establish long-term supply chain risk management, perform Business Impact Analysis, and validate cross-region cloud disaster recovery capabilities.
* **Key Deliverables:**
  1. `ACT-09`: Formulate Third-Party Risk Management (TPRM) procedure requiring annual SOC 2 reviews for vendors and enforce annual integration API key rotation.
  2. `ACT-10`: Conduct executive Business Impact Analysis (BIA) to establish defensible RTO and RPO targets, configure cross-region RDS snapshot replication to AWS US-West-2, and execute an annual mock disaster recovery restoration drill.
