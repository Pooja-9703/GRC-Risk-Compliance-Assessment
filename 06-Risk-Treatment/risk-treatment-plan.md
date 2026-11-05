# Deliverable 5: Risk Treatment Plan

**Organization:** ShopPulse Retail Solutions Inc.  
**Assessor:** Junior GRC Analyst (Simulated Engagement)  
**Derivation:** Derived strictly from Phase 2 Risk Register (`RSK-01` to `RSK-10`)  
**Version:** 1.3 (Final Quality-Control Alignment with Locked Deliverables 1–4)  

---

## 1. Executive Context & Risk Treatment Strategy

> **Portfolio & Ground-Truth Disclaimer:** This document represents a simulated GRC Risk Treatment Plan created for portfolio demonstration purposes. It defines proposed risk treatment strategies, governance objectives, and implementation examples based on documented current-state information. It does **not** imply that formal executive approvals, commercial insurance policy procurements, external audits, penetration tests, or technical remediations have actually been executed.

### Four Standard Primary Treatment Approaches
1. **Mitigate (Control):** Implement technical, administrative, or operational safeguards to reduce risk likelihood and/or business impact.
2. **Accept:** Formally acknowledge and accept residual risk when mitigation costs exceed potential impact, or where risk falls within organizational tolerance.
3. **Transfer (Risk Financing):** Shift financial liability to a third party (e.g., commercial cyber liability insurance or contractual vendor SLAs).
4. **Avoid:** Eliminate the risk by discontinuing the risky business process or technology.

> **Methodology Note on Primary Decisions & Risk Financing:** Each risk is assigned a single **Primary Treatment Decision**. Where supplementary risk-financing (e.g. evaluating cyber liability insurance) or management residual risk acceptance applies, these are documented as risk-financing measures or residual-risk acceptance decisions within the narrative justification.

> **Methodology Note on Expected Post-Treatment Residual Risk:** Post-treatment residual risk is independently reassessed using the same 5×5 likelihood/impact matrix used in the Risk Register. A proposed treatment may reduce likelihood, impact, or both only where the control is reasonably expected to change the relevant risk dimension. Expected post-treatment scores are planning estimates for this simulated engagement and are not measured results.

---

## 2. Master Risk Treatment Plan Table

| Risk ID | Risk Description | Inherent Risk | Existing Baseline Controls | Residual Risk | Primary Treatment Decision | Treatment Justification & Governance Rationale | Recommended Controls & Action Objectives | ISO 27001 Mapping | NIST CSF 2.0 Mapping | Risk Owner | Priority | Target Timeframe | Expected Post-Treatment Residual Risk | Status |
| :--- | :--- | :---: | :--- | :---: | :---: | :--- | :--- | :---: | :---: | :--- | :---: | :---: | :---: | :---: |
| **RSK-01** | Compromise of static developer AWS IAM access keys via phishing or leak. | **20 (Critical)** | Console IP restriction via AWS Client VPN. | **15 (High)** | **Mitigate** | Static API keys bypass VPN console restriction; enforcing MFA and transitioning developers to centralized SSO with short-lived credentials is expected to substantially reduce exposure associated with long-lived static access keys. | Enforce IAM policy mandating MFA for all AWS accounts; transition developers to centralized SSO with short-lived tokens. | A.5.15, A.8.5 | PR.AA-01 | CTO / IT Manager | **High** | **0–30 Days** | **3 (1×3) / Low** | Proposed |
| **RSK-02** | Potential misconfiguration and public exposure of S3 backup buckets. | **15 (High)** | AWS SSE-S3 encryption; AWS GuardDuty enabled. | **10 (High)** | **Mitigate** | S3 resources may contain business exports or backup-related data; SSE-S3 does not block public ACL requests. Account-level Block Public Access substantially reduces the likelihood of accidental public exposure of S3 resources. | Enable AWS Account-Level Block Public Access guardrail; deploy automated configuration drift monitoring rules. | A.5.23, A.8.9 | ID.AM-01, PR.PS-01 | Lead DevOps Engineer | **High** | **0–30 Days** | **2 (1×2) / Low** | Proposed |
| **RSK-03** | Threat actor exploits XSS or potentially vulnerable application dependencies to manipulate the checkout page and attempt to capture user inputs prior to Stripe payment-field submission. | **16 (High)** | Stripe Elements iFrame isolation; TLS 1.3 encryption. | **12 (High)** | **Mitigate** | Stripe iFrame isolates card data, but parent DOM tampering remains a potential threat scenario. Deploying WAF rules, strict CSP headers, and automated dependency scanning provides defensive safeguards. | Deploy Web Application Firewall (WAF) rules; configure strict HTTP Content Security Policy (CSP) headers; integrate automated SAST/dependency scanning. | A.8.8, A.8.24 | ID.RA-01, PR.PS-01 | Lead Software Engineer | **High** | **31–90 Days** | **4 (2×2) / Low** | Proposed |
| **RSK-04** | Spear-phishing targeting remote workforce for email credentials. | **12 (High)** | Google Workspace enforced MFA; spam filtering. | **9 (Medium)** | **Mitigate** | Primary decision is to **Mitigate** human vulnerability via security awareness training. Evaluate appropriate commercial Cyber Liability Insurance as a risk-financing measure for BEC fraud. | Deploy security awareness training platform with quarterly simulated phishing tests; evaluate cyber liability insurance coverage with financial advisors. | A.6.8, A.8.5 | PR.AT-01 | IT Manager / HR | **Medium** | **31–90 Days** | **6 (2×3) / Medium** | Proposed |
| **RSK-05** | Insufficient security incident logging & real-time alert monitoring. | **16 (High)** | GuardDuty enabled; CloudWatch logs retained for 14 days. | **12 (High)** | **Mitigate** | 14-day log retention limits forensic audit trails and delays breach discovery. Define security-log retention based on operational and compliance needs, centralize logs, and establish alert routing. | Define security-log retention based on operational and compliance requirements; centralize security-relevant logs; establish alert routing, triage, and escalation channels. | A.8.16 | DE.CM-01 | IT Manager / DevOps | **High** | **31–90 Days** | **3 (1×3) / Low** | Proposed |
| **RSK-06** | Threat actor exploits an unauthenticated backend API route or potential injection weakness in legacy reporting modules to exfiltrate customer PII from the production database. | **15 (High)** | RDS in private VPC subnet; KMS storage encryption. | **10 (High)** | **Mitigate** | Private subnets block direct DB access, but potential injection weaknesses or unverified credential storage practices represent application-layer risk. Reviewing credential storage and parameterized queries mitigates exposure. | Replace identified raw SQL queries with parameterized database access patterns appropriate to the application's technology stack; review credential storage and enforce secrets management rotation; conduct periodic code audits. | A.5.15 | ID.RA-01, PR.DS-01 | Lead Software Eng / CTO | **High** | **31–90 Days** | **2 (1×2) / Low** | Proposed |
| **RSK-07** | Third-party vendor breach or compromise of shared 3PL integration API keys. | **9 (Medium)** | HTTPS API transport; 3PL NAT IP whitelisting. | **6 (Medium)** | **Mitigate** | Primary decision is to **Mitigate** static key exposure via key rotation and TPRM process. Management formally **Accepts** residual vendor breach risk covered by 3PL SLAs. | Establish a risk-based Third-Party Risk Management (TPRM) process requiring appropriate security assurance evidence for critical vendors, such as SOC 2, ISO 27001, security questionnaires, contractual controls, or equivalent evidence where applicable; store vendor API keys in secret manager; execute annual key rotation. | A.5.19 | GV.SC-01 | Operations Manager | **Medium** | **91–180 Days** | **6 (2×3) / Medium** | Proposed |
| **RSK-08** | Data exposure risk via unenforced endpoint disk encryption on laptops. | **12 (High)** | MDM enrollment; remote wipe capability; startup password. | **6 (Medium)** | **Mitigate** | Remote wipe requires an online connection; an unencrypted offline drive can be read physically. Enforcement via MDM policy is intended to mandate full-disk encryption across managed devices. | Enforce mandatory FileVault (macOS) and BitLocker (Windows 11) full-disk encryption policies via MDM; mandate compliance reporting. | A.8.12 | ID.AM-01, PR.DS-01 | IT Manager | **Medium** | **31–90 Days** | **2 (1×2) / Low** | Proposed |
| **RSK-09** | Prolonged downtime risk from limited disaster recovery readiness. | **12 (High)** | Automated daily RDS snapshots; snapshot retention, restoration procedures, recovery objectives, and restoration testing require verification. | **8 (Medium)** | **Mitigate** | Single-region backup storage leaves ShopPulse vulnerable to broad cloud region outages or logical database corruption. Mitigation requires conducting a formal Business Impact Analysis (BIA) to establish defensible RTO and RPO objectives, configuring cross-region backup replication based on BIA results and recovery requirements, and conducting regular restoration drills. | Perform Business Impact Analysis (BIA) to define RTO/RPO requirements; configure cross-region backup replication based on BIA results; conduct annual BC/DR restoration drill. | A.5.23 | GV.RM-01, RC.RP-01 | Lead DevOps Engineer | **Medium** | **91–180 Days** | **6 (2×3) / Medium** | Proposed |
| **RSK-10** | Employee security misconfigurations due to lack of written policies. | **12 (High)** | Verbal onboarding instructions; password length rule (8+ chars). | **9 (Medium)** | **Mitigate** | Verbal instructions in a 45-person company cause Shadow IT and policy confusion. Written security governance defines clear operational rules. | Draft, approve, and publish comprehensive Information Security Policy suite (AUP, Access Control, Data Protection); mandate annual employee sign-off. | A.5.1 | GV.PO-01 | IT Manager / HR | **Medium** | **31–90 Days** | **6 (2×3) / Medium** | Proposed |

---

## 3. Detailed Treatment Justification & Action Plans

### RSK-01: Access Control & IAM Key Management
* **Risk Context:** `AST-05` (AWS Control Plane) | Inherent Score: 20 (Critical) | Residual Score: 15 (High)
* **Primary Treatment Decision:** **Mitigate**
* **Justification:** AWS IAM is the root management boundary for cloud infrastructure. Relying on IP restrictions for console logins leaves programmatic API access keys vulnerable to phishing or source code leaks. Enforcing MFA and transitioning developers to centralized SSO with short-lived credentials is expected to substantially reduce exposure associated with long-lived static access keys.
* **Action Objectives:**
  1. Enforce IAM policy requiring MFA for all IAM user access within 14 days.
  2. Audit developer access keys and establish key rotation/deactivation procedures for long-lived keys.
  3. Configure centralized Single Sign-On (SSO) integrated with corporate directory (e.g. AWS IAM Identity Center via Google Workspace) for short-lived token generation.
* **Expected Post-Treatment Residual Risk Evaluation:** **3 (1×3) / Low** — *Planning Estimate:* Enforcing MFA and temporary credentials is expected to substantially reduce static credential exposure subject to implementation and verification.
* **Target Completion:** 0–30 Days (Immediate Priority) | **Owner:** CTO / IT Manager

---

### RSK-02: Public Storage Bucket Protection
* **Risk Context:** `AST-02` (RDS Database), `AST-05` (AWS Cloud Infra) | Inherent Score: 15 (High) | Residual Score: 10 (High)
* **Primary Treatment Decision:** **Mitigate**
* **Justification:** S3 resources may contain business exports or backup-related data. Server-side encryption protects physical disk storage at datacenters but does not block web access if bucket ACLs permit public reading. Account-level Block Public Access provides a centralized guardrail to substantially reduce the likelihood of accidental public storage bucket misconfigurations.
* **Action Objectives:**
  1. Enable Account-Level "Block Public Access" guardrails across the primary cloud account.
  2. Deploy continuous configuration drift monitoring rules (e.g. AWS Config or open-source IaC linters) for automated S3 compliance enforcement.
  3. Audit storage bucket policy configurations to verify that public access is restricted.
* **Expected Post-Treatment Residual Risk Evaluation:** **2 (1×2) / Low** — *Planning Estimate:* Account-level block guardrails substantially reduce the likelihood of public storage bucket misconfigurations.
* **Target Completion:** 0–30 Days (Immediate Priority) | **Owner:** Lead DevOps Engineer

---

### RSK-03: Web Application & Checkout Form Hardening
* **Risk Context:** `AST-01` (Web Storefront), `AST-07` (Stripe Integration) | Inherent Score: 16 (High) | Residual Score: 12 (High)
* **Primary Treatment Decision:** **Mitigate**
* **Justification:** Stripe Elements iFrames isolate card data collection from internal servers. However, DOM tampering on the parent checkout page remains a potential threat scenario if application or dependency vulnerabilities exist. Deploying web application firewalls, strict Content Security Policy (CSP) headers, and automated dependency scanning provides defensive safeguards.
* **Action Objectives:**
  1. Provision a Web Application Firewall (WAF) attached to the load balancer with OWASP Top 10 rule sets (e.g. AWS WAF, Cloudflare).
  2. Implement strict HTTP Content Security Policy (CSP) headers restricting script execution sources to trusted domains.
  3. Integrate automated dependency scanning and SAST tools into build pipelines.
* **Expected Post-Treatment Residual Risk Evaluation:** **4 (2×2) / Low** — *Planning Estimate:* WAF rules, CSP headers, and automated dependency patching are expected to mitigate DOM script injection exposure.
* **Target Completion:** 31–90 Days | **Owner:** Lead Software Engineer

---

### RSK-04: Phishing Mitigation & Cyber Insurance Evaluation
* **Risk Context:** `AST-03` (Endpoints), `AST-06` (Google Workspace) | Inherent Score: 12 (High) | Residual Score: 9 (Medium)
* **Primary Treatment Decision:** **Mitigate**
* **Justification:** Technical controls (Google Workspace MFA) mitigate automated credential replay, but adversary-in-the-middle (AiTM) phishing kits can capture session cookies. Human vulnerability is **Mitigated** through continuous awareness training. As a supplementary **risk-financing measure**, management will evaluate commercial Cyber Liability Insurance coverage tailored to organizational risk appetite and financial exposure.
* **Action Objectives:**
  1. Deploy a web-based security awareness training platform (e.g. KnowBe4, Ninjio) with mandatory annual modules.
  2. Conduct unannounced quarterly simulated phishing campaigns; mandate retraining for repeat clickers.
  3. Evaluate appropriate commercial Cyber Liability Insurance coverage options with executive management and financial advisors.
* **Expected Post-Treatment Residual Risk Evaluation:** **6 (2×3) / Medium** — *Planning Estimate / Residual Risk Retained as Medium:* Human susceptibility to sophisticated phishing attacks cannot be entirely eliminated by training, retaining meaningful residual exposure that requires ongoing monitoring.
* **Target Completion:** 31–90 Days | **Owner:** IT Manager / HR Generalist

---

### RSK-05: Centralized Logging & Alert Monitoring
* **Risk Context:** `AST-01`, `AST-02`, `AST-05` (Cloud Environment) | Inherent Score: 16 (High) | Residual Score: 12 (High)
* **Primary Treatment Decision:** **Mitigate**
* **Justification:** The 14-day default log retention period limits forensic audit trails and delays breach discovery. Define security-log retention based on operational, investigation, and applicable compliance requirements; centralize security-relevant logs; and establish alert routing, monitoring ownership, triage, and escalation channels.
* **Action Objectives:**
  1. Define security-log retention requirements based on operational, investigation, and compliance needs, extending CloudWatch log retention accordingly in immutable storage.
  2. Establish centralized security log aggregation and monitoring.
  3. Route high-severity security detection alerts to established security escalation channels.
* **Expected Post-Treatment Residual Risk Evaluation:** **3 (1×3) / Low** — *Planning Estimate:* Centralized log archiving and alert escalation enable timely incident detection and forensic analysis.
* **Target Completion:** 31–90 Days | **Owner:** IT Manager / Lead DevOps Engineer

---

### RSK-06: Database PII Protection & Secrets Management
* **Risk Context:** `AST-02` (RDS Database), `AST-01` (Web App) | Inherent Score: 15 (High) | Residual Score: 10 (High)
* **Primary Treatment Decision:** **Mitigate**
* **Justification:** Private subnets isolate database network traffic, but potential injection weaknesses or unverified credential storage practices represent application-layer risk. Review database credential storage practices and migrate credentials to an approved secrets-management solution where required, with automated rotation based on defined security requirements, while parameterizing database access.
* **Action Objectives:**
  1. Review database access patterns and replace identified raw SQL queries with parameterized database access patterns appropriate to the application's technology stack.
  2. Review database credential storage practices and migrate credentials to an approved secrets-management solution (e.g., AWS Secrets Manager) with automated rotation based on defined security requirements.
  3. Schedule periodic static code analysis and web application security assessments.
* **Expected Post-Treatment Residual Risk Evaluation:** **2 (1×2) / Low** — *Planning Estimate:* Parameterized queries and automated database secrets rotation substantially reduce application-layer database exposure.
* **Target Completion:** 31–90 Days | **Owner:** Lead Software Engineer / CTO

---

### RSK-07: Third-Party Vendor Security & API Key Management
* **Risk Context:** `AST-08` (3PL API), `AST-09` (Zendesk SaaS) | Inherent Score: 9 (Medium) | Residual Score: 6 (Medium)
* **Primary Treatment Decision:** **Mitigate**
* **Justification:** NAT IP whitelisting restricts 3PL API key execution to authorized cloud outbound IPs. Primary mitigation involves establishing a Third-Party Risk Management (TPRM) process and rotating integration keys annually via a secret manager. Executive Management formally **Accepts** the residual risk of vendor-side operational downtime, as physical inventory SLA indemnification is contractually covered under 3PL agreements.
* **Action Objectives:**
  1. Establish a risk-based Third-Party Risk Management (TPRM) process requiring appropriate security assurance evidence for critical vendors, such as SOC 2, ISO 27001, security questionnaires, contractual controls, or equivalent evidence where applicable.
  2. Store third-party integration keys in a secret management system and execute annual key rotation.
  3. Formally document Executive Acceptance of residual vendor operational downtime risks covered under vendor contract SLAs.
* **Expected Post-Treatment Residual Risk Evaluation:** **6 (2×3) / Medium** — *Planning Estimate / Residual Risk Retained as Medium:* Supply chain security risks stemming from external vendor breaches remain partially outside ShopPulse's direct operational control, retaining a Medium residual risk level.
* **Target Completion:** 91–180 Days | **Owner:** Operations Manager / IT Manager

---

### RSK-08: Endpoint Full-Disk Encryption Enforcement
* **Risk Context:** `AST-03` (Employee Laptops) | Inherent Score: 12 (High) | Residual Score: 6 (Medium)
* **Primary Treatment Decision:** **Mitigate**
* **Justification:** MDM remote wipe capability is ineffective if a stolen device remains offline. Enforcement via MDM policy is intended to mandate full-disk encryption across managed devices, rendering drive contents unreadable if physical storage is accessed offline.
* **Action Objectives:**
  1. Enforce mandatory FileVault (macOS) and BitLocker (Windows 11) full-disk encryption policies across corporate endpoints via MDM.
  2. Escrow disk encryption recovery keys securely within the MDM cloud tenant.
  3. Configure MDM compliance rules to restrict non-compliant endpoints from accessing corporate Google Workspace data.
* **Expected Post-Treatment Residual Risk Evaluation:** **2 (1×2) / Low** — *Planning Estimate:* Enforcing full-disk encryption substantially reduces the exposure of data on lost or stolen endpoints.
* **Target Completion:** 31–90 Days | **Owner:** IT Manager

---

### RSK-09: Disaster Recovery & Business Continuity Assurance
* **Risk Context:** `AST-02` (RDS Database), `AST-01` (Web Storefront) | Inherent Score: 12 (High) | Residual Score: 8 (Medium)
* **Primary Treatment Decision:** **Mitigate**
* **Justification:** Single-region backup storage leaves ShopPulse vulnerable to broad cloud region outages or logical database corruption. Mitigation requires conducting a formal Business Impact Analysis (BIA) to establish defensible RTO and RPO objectives, configuring cross-region backup replication based on BIA results and recovery requirements, and conducting regular restoration drills.
* **Action Objectives:**
  1. Perform a formal Business Impact Analysis (BIA) with executive leadership to define Recovery Time Objectives (RTO) and Recovery Point Objectives (RPO) aligned with business recovery requirements.
  2. Configure cross-region backup replication based on the results of the Business Impact Analysis (BIA) and defined recovery requirements.
  3. Formalize a Business Continuity / Disaster Recovery (BC/DR) Plan and conduct an annual mock disaster recovery restoration drill.
* **Expected Post-Treatment Residual Risk Evaluation:** **6 (2×3) / Medium** — *Planning Estimate / Residual Risk Retained as Medium:* Catastrophic cloud-wide infrastructure outages or major regional disasters retain a Medium residual risk level even with tested recovery plans.
* **Target Completion:** 91–180 Days | **Owner:** Lead DevOps Engineer

---

### RSK-10: Information Security Policy Framework
* **Risk Context:** All Assets (`AST-01` to `AST-10`) | Inherent Score: 12 (High) | Residual Score: 9 (Medium)
* **Primary Treatment Decision:** **Mitigate**
* **Justification:** Informal verbal rules in a growing 45-person organization lead to operational confusion, Shadow IT adoption, and inconsistent data protection. Written security policies establish clear governance and compliance boundaries.
* **Action Objectives:**
  1. Draft a comprehensive Information Security Policy suite consisting of: Acceptable Use Policy (AUP), Access Control Policy, Data Classification & Handling Policy, and Password Policy.
  2. Obtain formal executive approval from CTO and CEO.
  3. Publish policies on internal document portal and collect digital sign-off acknowledgments from all staff.
* **Expected Post-Treatment Residual Risk Evaluation:** **6 (2×3) / Medium** — *Planning Estimate / Residual Risk Retained as Medium:* Written policies establish clear operational boundaries, but human non-compliance or accidental employee oversights retain a Medium residual risk level.
* **Target Completion:** 31–90 Days | **Owner:** IT Manager / HR Generalist
