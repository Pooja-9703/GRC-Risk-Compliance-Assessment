# Deliverable 4: NIST Cybersecurity Framework (CSF) 2.0 Mapping & Assessment

**Organization:** ShopPulse Retail Solutions Inc.  
**Assessor:** Junior GRC Analyst (Simulated Engagement)  
**Framework Baseline:** NIST Cybersecurity Framework (CSF) v2.0 (Official Standard)  
**Assessment Type:** Portfolio / Simulated Control Mapping  
**Version:** 1.1 (Verified against Official NIST CSF 2.0 Reference)  

---

## 1. Executive Summary & Official NIST CSF 2.0 Architecture

This assessment maps the cybersecurity posture, documented baseline controls, risk register items (`RSK-01` to `RSK-10`), and ISO 27001 gap findings for **ShopPulse Retail Solutions Inc.** directly to the **NIST Cybersecurity Framework (CSF) 2.0**.

Every Function, Category, and Subcategory identifier in this deliverable has been verified against the official NIST CSF 2.0 taxonomy released by the National Institute of Standards and Technology (NIST).

### The Six Core Functions of NIST CSF 2.0
1. **GOVERN (GV):** Establish and monitor the organization's cybersecurity risk management strategy, governance policies, and supply chain oversight.
2. **IDENTIFY (ID):** Determine current cybersecurity risks to systems, assets, data, and capabilities.
3. **PROTECT (PR):** Use safeguards to prevent or reduce cybersecurity risks.
4. **DETECT (DE):** Find and analyze possible cybersecurity attacks and adverse events.
5. **RESPOND (RS):** Take action regarding a detected cybersecurity incident.
6. **RECOVER (RC):** Restore assets and operations affected by a cybersecurity incident.

> **Audit & Ground-Truth Disclaimer:** This mapping is a simulated portfolio assessment synthesizing documented current-state information, technical specifications, and risk evaluations from Phases 1–3. Unverified conditions are explicitly labeled as assumptions, conditions to be verified, or evidence requirements rather than confirmed audit findings.

---

## 2. Official NIST CSF 2.0 Master Assessment & Mapping Matrix

| NIST Function | Official Category & Subcategory Code | Category & Subcategory Title (NIST CSF 2.0) | Documented Current State & Ground Truth Status | Existing Baseline Controls | Identified Gap & Condition to be Verified | Related Risk ID | Related Asset ID | ISO 27001 Mapping | Recommended Improvement | Priority | Responsible Owner |
| :--- | :--- | :--- | :--- | :--- | :--- | :---: | :---: | :---: | :--- | :---: | :--- |
| **GOVERN** | `GV.PO-01` | **Policy:** Organizational cybersecurity policy is established & communicated. | Verbal onboarding instructions provided to new hires. | Basic password length rule (8+ chars). | Absence of formal written Information Security Policy suite (AUP, Access Control, Data Protection). | RSK-10 | AST-01 to AST-10 | A.5.1 | Draft, approve, and publish core written security policy suite. | **Medium** | IT Manager / HR |
| **GOVERN** | `GV.RM-01` | **Risk Management Strategy:** Risk management objectives established & agreed to. | Ad-hoc risk evaluations during major software deployments. | Informal IT review prior to software release. | Absence of documented risk assessment policy or continuous risk evaluation cadence. | RSK-09, RSK-10 | AST-01 to AST-10 | A.5.1 | Formalize annual cybersecurity risk assessment methodology and register review. | **Medium** | CTO / IT Manager |
| **GOVERN** | `GV.SC-01` | **Cybersecurity Supply Chain Risk Management:** Supply chain risk management program established. | Third-party SaaS tools onboarded informally by department heads. | HTTPS API transport; 3PL endpoint access controls require verification. | Lack of formal Third-Party Risk Management (TPRM) policy or vendor security review procedures. | RSK-07 | AST-08, AST-09 | A.5.19 | Establish a risk-based Third-Party Risk Management procedure requiring security due diligence and periodic assurance review for critical and high-risk suppliers. Evidence may include security questionnaires, contractual security requirements, SOC 2 reports, ISO certifications, penetration-test summaries, or equivalent assurance documentation where applicable. | **Medium** | Operations Manager |
| **IDENTIFY** | `ID.AM-01` | **Asset Management:** Inventories of hardware managed by organization are maintained. | Corporate laptops managed in MDM; cloud assets tagged informally. | Jamf / Intune MDM inventory tracking. | AWS cloud resource tagging and asset lifecycle classification policies require enforcement. | RSK-02, RSK-08 | AST-01 to AST-10 | A.8.9 | Enforce mandatory AWS resource tagging policies and automated asset discovery. | **Medium** | IT Manager / DevOps |
| **IDENTIFY** | `ID.RA-01` | **Risk Assessment:** Vulnerabilities in assets are identified, validated, & recorded. | Informal manual code reviews prior to application release. | Basic OS patching managed via Jamf/Intune MDM. | GitHub repositories lack automated SAST and dependency vulnerability scanners. | RSK-03, RSK-06 | AST-01, AST-04 | A.8.8 | Integrate automated Dependabot and SAST scanners into GitHub Actions CI/CD. | **High** | Lead Software Engineer |
| **PROTECT** | `PR.AA-01` | **Identity Management & Access Control:** Identities & credentials managed. | Google Workspace uses MFA. AWS IAM is used for cloud administration; some developer IAM users may rely on long-lived static access keys, and IAM MFA enforcement and coverage require verification. | AWS Client VPN used for engineer VPC access; console access controls require verification. | AWS IAM MFA enforcement and coverage, access-key usage, and access-review practices require verification. | RSK-01 | AST-05 | A.5.15, A.8.5 | Enforce IAM policy mandating MFA for all AWS accounts; evaluate transition to AWS IAM Identity Center (SSO). | **High** | CTO / IT Manager |
| **PROTECT** | `PR.AT-01` | **Awareness & Training:** Personnel provided awareness & training. | Verbal onboarding instructions provided to new hires. | Google Workspace anti-spam filters. | Formal security awareness and anti-phishing training requirements and completion status require verification. | RSK-04 | AST-03, AST-06 | A.6.8 | Deploy web-based security awareness platform with quarterly simulated phishing tests. | **Medium** | HR Generalist / IT |
| **PROTECT** | `PR.DS-01` | **Data Security:** Data-at-rest confidentiality, integrity, & availability protected. | Production RDS database storage is encrypted at rest using AWS KMS. Endpoint full-disk encryption enforcement requires verification across corporate laptops. | RDS KMS database storage encryption; Stripe Elements iFrame payment scope reduction. | Full-disk encryption enforcement requires verification across corporate laptops. | RSK-06, RSK-08 | AST-02, AST-03 | A.8.12, A.8.24 | Enforce mandatory FileVault/BitLocker encryption policies across all 45 corporate laptops through MDM and verify 100% compliance. | **High** | IT Manager / DevOps |
| **PROTECT** | `PR.PS-01` | **Platform Security:** Configuration management practices established & applied. | Application is hosted on AWS ECS with an ALB, and relevant application security and dependency-management controls require verification. | AWS ALB security groups; private RDS subnet routing. | Application dependency security controls and web-application protection mechanisms require verification and may leave the storefront exposed to exploitation or client-side manipulation. | RSK-02, RSK-03 | AST-01, AST-05 | A.8.8, A.8.9 | Deploy AWS WAF with OWASP Top 10 rules, configure strict HTTP CSP headers, and enable automated dependency scanning. | **High** | Lead Software Eng / DevOps |
| **DETECT** | `DE.CM-01` | **Continuous Monitoring:** Networks & services monitored to find adverse events. | Amazon GuardDuty is enabled. Alert routing, monitoring ownership, triage procedures, and escalation require verification. CloudWatch logs retained for 14 days. | AWS GuardDuty enabled; AWS CloudWatch logs retained for 14 days. | Security monitoring and response workflows for GuardDuty findings are not sufficiently documented; CloudWatch logs expire after 14 days without centralized SIEM. | RSK-05 | AST-01, AST-02, AST-05 | A.8.16 | Define security-log retention requirements based on operational, investigation, and applicable compliance needs; extend relevant CloudWatch log retention accordingly, centralize security-relevant logs, and establish alert routing and escalation. | **High** | IT Manager / DevOps |
| **RESPOND** | `RS.MA-01` | **Incident Management:** Incidents initiated & managed upon detection. | Ad-hoc incident troubleshooting performed by IT Manager. | Basic AWS backup snapshots available. | No documented Incident Response Plan (IRP) or assigned incident response team roles. | RSK-05, RSK-10 | AST-01 to AST-10 | A.5.1 | Draft formal Incident Response Plan (IRP) with severity levels and contact matrices. | **High** | CTO / IT Manager |
| **RECOVER** | `RC.RP-01` | **Recovery Plan Execution:** Recovery portion of IR plans executed once initiated. | Daily RDS PostgreSQL snapshots are configured. Snapshot retention, restoration procedures, recovery objectives, and restoration testing require verification. | Automated daily RDS snapshots configured. | Formal disaster recovery readiness and restoration testing have not been established or verified. | RSK-09 | AST-01, AST-02 | A.5.23 | Define recovery objectives and backup retention requirements, evaluate cross-region backup or replication based on business continuity needs, and conduct a documented restoration test. | **Medium** | Lead DevOps Engineer |

---

## 3. Function-by-Function Assessment Findings

### 1. GOVERN (GV) — Operational Governance & Risk Oversight
* **Current Posture:** ShopPulse operates with an informal governance model. While basic technical configurations are handled by the DevOps team, there is an absence of formal written policies, structured risk management procedures, or vendor security oversight.
* **Key Gaps:**
  * **Policy Framework (`GV.PO-01`):** Absence of written Acceptable Use, Access Control, and Data Protection policies (`RSK-10`).
  * **Supply Chain Management (`GV.SC-01`):** Third-party vendors (3PL, Zendesk) onboarded without formal security review procedures (`RSK-07`).
* **Priority Recommendations:** Draft and publish an executive-approved Information Security Policy suite and establish a risk-based Third-Party Risk Management (TPRM) workflow.

---

### 2. IDENTIFY (ID) — Asset Discovery & Risk Identification
* **Current Posture:** Asset tracking is partially implemented. Endpoint laptops are inventoried in MDM (Jamf/Intune), but AWS cloud resource tagging and vulnerability management are performed reactively.
* **Key Gaps:**
  * **Vulnerability Assessment (`ID.RA-01`):** GitHub source code repositories and third-party npm packages lack automated vulnerability scanning (`RSK-03`).
* **Priority Recommendations:** Integrate automated Dependabot and SAST tools directly into GitHub Actions CI/CD deployment pipelines.

---

### 3. PROTECT (PR) — Safeguards & Access Controls
* **Current Posture:** Technical safeguards are partially effective (TLS 1.3 encryption in transit, Stripe Elements payment scope reduction, RDS KMS database storage encryption). However, identity and access control practices require verification.
* **Key Gaps:**
  * **Identity & Access Control (`PR.AA-01`):** AWS IAM MFA enforcement and coverage, access-key usage, and access-review practices require verification (`RSK-01`).
  * **Security Awareness (`PR.AT-01`):** Formal security awareness and anti-phishing training requirements and completion status require verification (`RSK-04`).
  * **Platform Security (`PR.PS-01`):** Application dependency security controls and web application protection mechanisms require verification (`RSK-03`).
* **Priority Recommendations:** Enforce mandatory IAM MFA policies, evaluate transition to AWS IAM Identity Center (SSO), launch annual employee security awareness training, and evaluate AWS WAF with strict HTTP CSP headers.

---

### 4. DETECT (DE) — Security Monitoring & Anomaly Detection
* **Current Posture:** Detection capabilities require strengthening. While Amazon GuardDuty is enabled, alert routing and triage procedures require verification. AWS CloudWatch logs are retained for 14 days without log centralization.
* **Key Gaps:**
  * **Continuous Monitoring (`DE.CM-01`):** Short 14-day log retention limits forensic analysis capability; absence of centralized log aggregation or alert routing permits threat persistence (`RSK-05`).
* **Priority Recommendations:** Define log retention requirements based on operational and compliance needs, extend relevant CloudWatch log retention, centralize security-relevant logs, and establish alert routing and escalation.

---

### 5. RESPOND (RS) — Incident Response Readiness
* **Current Posture:** Response capabilities are reactive. In the event of a security incident, the IT Manager handles troubleshooting ad-hoc without formal procedures or predefined roles.
* **Key Gaps:**
  * **Incident Execution (`RS.MA-01`):** No documented Incident Response Plan (IRP), severity classification matrix, or communications protocol exists (`RSK-05`, `RSK-10`).
* **Priority Recommendations:** Formulate a practical Incident Response Plan (IRP) defining severity levels, escalation trees, and external breach notification requirements.

---

### 6. RECOVER (RC) — Business Continuity & Disaster Recovery
* **Current Posture:** Recovery mechanisms rely on automated daily AWS RDS PostgreSQL snapshots.
* **Key Gaps:**
  * **Recovery Planning (`RC.RP-01`):** Snapshot retention, restoration procedures, recovery objectives, and restoration testing require verification (`RSK-09`).
* **Priority Recommendations:** Define recovery objectives and backup retention requirements, evaluate cross-region backup or replication based on business continuity needs, and conduct a documented restoration test.
