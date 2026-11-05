# Deliverable 2: Cybersecurity Risk Register & Detailed Risk Evaluations

**Organization:** ShopPulse Retail Solutions Inc.  
**Assessor:** Junior GRC Analyst (Simulated Engagement)  
**Scoring Model:** 5x5 Semi-Quantitative Matrix (Inherent vs. Residual Risk)  
**Version:** 1.4 (Final Micro-Correction & Scope Alignment)  

---

## 1. Risk Register Overview & Evaluation Guidelines

This document presents the formal **Cybersecurity Risk Register** for ShopPulse Retail Solutions Inc. Every risk is derived from the approved organizational profile, technology stack, and operational context.

### Key Assessment Principles Applied
1. **Inherent vs. Residual Risk Distinction:** 
   * **Inherent Risk:** The level of risk assessed before considering the effectiveness of existing security controls.
   * **Residual Risk:** The remaining level of risk assessed after considering the effectiveness of existing baseline security controls.
2. **Scoring Justification Requirement:** Every assigned Likelihood (1–5) and Impact (1–5) score is accompanied by a documented or explicitly qualified analytical justification grounded in current-state observations, assumptions, verification conditions, and business impact parameters.
3. **Ground Truth Labeling:** No fake external audit results or unverified facts are presented as documented evidence. All items explicitly demarcate:
   * `[Documented Current State]`: Operational facts supported by existing project documents.
   * `[Assumption]`: Logical analytical deductions based on tech stack.
   * `[Risk Condition to be Verified]`: Unconfirmed vulnerability or potential gap requiring verification.
   * `[Evidence Required]`: Specific documentation/artifacts required to verify control effectiveness in an audit.

---

## 2. Master Risk Register Table

| Risk ID | Asset ID | Business Process | Threat Scenario | Vulnerability / Weakness | Existing Baseline Controls | Inherent L × I | Inherent Score | Risk Condition to be Verified / Gaps | Residual L × I | Residual Score | Risk Treatment | Risk Owner | Priority |
| :--- | :--- | :--- | :--- | :--- | :--- | :---: | :---: | :--- | :---: | :---: | :--- | :--- | :---: |
| **RSK-01** | AST-05 | Cloud Administration | Compromise of static developer access keys via phishing or leak. | AWS IAM MFA enforcement policy and coverage require verification. | AWS Client VPN is used for engineer access to AWS VPC resources; AWS console access controls require verification. | 4 × 5 | **20 (Critical)** | Some developer IAM users may rely on long-lived access keys; IAM MFA enforcement and access-key age/rotation status require verification through an IAM credential report. | 3 × 5 | **15 (High)** | Mitigate | CTO / IT Manager | **High** |
| **RSK-02** | AST-02, AST-05 | Backup & Storage | Unintended public exposure of AWS S3 buckets containing business exports or backup-related data. | S3 public-access configuration and bucket policies may not be consistently enforced across relevant buckets. | AWS SSE-S3 encryption; AWS GuardDuty provides threat detection capabilities for supported AWS activity; S3 public-access configuration and bucket policies require separate verification. | 3 × 5 | **15 (High)** | Potential bucket ACL misconfiguration; needs verification via Block Public Access export. | 2 × 5 | **10 (High)** | Mitigate | Lead DevOps Engineer | **High** |
| **RSK-03** | AST-01, AST-07 | Checkout & Payment | Threat actor exploits XSS or potentially vulnerable application dependencies to manipulate the checkout web page DOM, attempting to capture user inputs prior to Stripe iFrame form submission. | Web application dependency management and security controls require verification. | Stripe Elements hosts card-entry fields through Stripe-controlled components, reducing the exposure of cardholder data to ShopPulse application infrastructure; TLS 1.3 encryption. | 4 × 4 | **16 (High)** | Dependency vulnerability status, CSP headers, and other web application security controls require verification. SAQ type requires PCI DSS v4.0 validation. | 3 × 4 | **12 (High)** | Mitigate | Lead Software Engineer | **High** |
| **RSK-04** | AST-03, AST-06 | Corporate Comms | Spear-phishing targets staff for email credential harvesting. | Security awareness training requirements and completion status are not verified. | Google Workspace enforced MFA; spam filtering. Customer support representatives routinely handle inbound external emails, increasing exposure to phishing attempts. | 4 × 3 | **12 (High)** | Security awareness training requirements and completion status are not verified. | 3 × 3 | **9 (Medium)** | Mitigate | IT Manager / HR | **Medium** |
| **RSK-05** | AST-01, AST-02, AST-05 | Security Monitoring | Attacker gains persistent cloud access without detection. | CloudWatch logs retained for 14 days; no centralized SIEM. | GuardDuty is enabled; alert routing and escalation procedures require verification. | 4 × 4 | **16 (High)** | Short log retention (14 days); lack of security alert routing/SIEM. | 3 × 4 | **12 (High)** | Mitigate | IT Manager / DevOps | **High** |
| **RSK-06** | AST-02, AST-01 | Customer Data | Threat actor exploits an unauthenticated backend API route or a potential injection weakness in legacy reporting modules to exfiltrate customer PII in the production database. | Legacy reporting components may contain raw SQL queries, and database credential storage practices require verification. | RDS in private VPC subnet; KMS storage encryption. | 3 × 5 | **15 (High)** | Potential raw SQL queries in legacy reporting components; database credential storage practices require verification. | 2 × 5 | **10 (High)** | Mitigate | Lead Software Eng / CTO | **High** |
| **RSK-07** | AST-08, AST-09 | Fulfillment & Support | Third-party vendor breach compromises shared API keys. | Formal third-party security review and assurance-documentation requirements are not established. | HTTPS API transport; 3PL endpoint access controls require verification. Static/hardcoded integration API keys require verification. | 3 × 3 | **9 (Medium)** | Hardcoded API keys; formal third-party security review process is not established. | 2 × 3 | **6 (Medium)** | Mitigate | Operations Manager | **Medium** |
| **RSK-08** | AST-03 | Remote Operations | Data Exposure Risk from Stolen or Lost Corporate Laptops with Unverified Disk Encryption. | Full-disk encryption (FileVault/BitLocker) policy enforcement unverified. | MDM remote wipe capability; password login required. | 4 × 3 | **12 (High)** | Potential unencrypted drive state; requires Jamf/Intune compliance verification report. | 2 × 3 | **6 (Medium)** | Mitigate | IT Manager | **Medium** |
| **RSK-09** | AST-02, AST-01 | Business Continuity | Cloud outage or database corruption paralyzes storefront. | No formal Business Continuity / Disaster Recovery (BC/DR) plan exists; RDS snapshot restoration procedures and recovery testing require verification. | Automated daily RDS snapshots are configured; backup retention and restoration procedures require verification. RDS availability features may provide resilience depending on deployed configuration; actual Multi-AZ configuration requires verification. | 3 × 4 | **12 (High)** | Single-region backup dependency; untested RTO/RPO targets. | 2 × 4 | **8 (Medium)** | Mitigate | Lead DevOps Engineer | **Medium** |
| **RSK-10** | AST-01 to AST-10 | Governance | Staff use unvetted SaaS (Shadow IT) or reuse weak passwords. | Absence of written Information Security Policy framework. | Verbal onboarding instructions; password length rules. In a growing distributed workforce, reliance on verbal security instructions may contribute to inconsistent policy interpretation and unvetted SaaS usage. | 4 × 3 | **12 (High)** | Lack of written security policies (AUP, Access Control, Data Classification). | 3 × 3 | **9 (Medium)** | Mitigate | IT Manager / HR | **Medium** |

---

## 3. Detailed Risk Breakdown & Score Justifications

### RSK-01: AWS IAM Access Control & MFA Enforcement Risk
* **Asset & Process:** `AST-05` (AWS Cloud Control Plane) | Infrastructure Administration
* **Threat Scenario:** Malicious actor acquires developer access keys via phishing or source code leak.
* **Vulnerability:** AWS IAM MFA enforcement policy and coverage require verification.
* **Documented Current State & Verification Condition:** `[Risk Condition to be Verified]` Some developer IAM users may rely on long-lived access keys; IAM MFA enforcement and access-key age/rotation status require verification through an IAM credential report.
* **Inherent Risk Justification:** **Likelihood = 4 (Likely)** — Static AWS access keys without MFA are heavily targeted via public code repo leaks and phishing. **Impact = 5 (Catastrophic)** — Full AWS control plane compromise allows complete resource destruction, ransomware, or mass customer data deletion. **Inherent Score = 20 (Critical)**.
* **Existing Baseline Controls:** AWS Client VPN is used for engineer access to AWS VPC resources; AWS console access controls require verification.
* **Residual Risk Justification:** **Likelihood = 3 (Possible)** — Existing network access controls reduce some avenues for unauthorized administrative access, but leaked API keys can still be used outside the VPN boundary. The effectiveness of IAM-specific controls require verification. **Impact = 5 (Catastrophic)** — Potential impact remains extreme. **Residual Score = 15 (High)**.
* **Priority Alignment:** **High** (Standardized to match Residual Rating High).
* **Evidence Required for Audit Verification:** `aws iam generate-credential-report` output, IAM JSON policy enforcement documents, AWS Config compliance rules.

---

### RSK-02: Potential Misconfiguration & Unintended Public Exposure of AWS S3 Buckets
* **Asset & Process:** `AST-02` (RDS Database), `AST-05` (AWS Cloud Infra) | Backup & Storage Management
* **Threat Scenario:** Unintended public exposure of AWS S3 buckets containing business exports or backup-related data.
* **Vulnerability:** S3 public-access configuration and bucket policies may not be consistently enforced across relevant buckets.
* **Documented Current State & Verification Condition:** `[Risk Condition to be Verified]` S3 Block Public Access configuration and bucket policies require verification via AWS API exports.
* **Inherent Risk Justification:** **Likelihood = 3 (Possible)** — Automated scanner tools continuously probe S3 namespace patterns. **Impact = 5 (Catastrophic)** — Exposure of customer-related exports or backup data stored in an improperly configured S3 bucket could result in unauthorized disclosure of customer PII. **Inherent Score = 15 (High)**.
* **Existing Baseline Controls:** AWS SSE-S3 default server-side encryption is active (protects physical disk theft at AWS datacenters). AWS GuardDuty provides threat detection capabilities for supported AWS activity; S3 public-access configuration and bucket policies require separate verification.
* **Residual Risk Justification:** **Likelihood = 2 (Unlikely)** — Existing AWS threat-detection capabilities provide some additional visibility, but the effectiveness of S3 public-access controls and alert routing remains subject to verification. **Impact = 5 (Catastrophic)** — Data breach consequence remains catastrophic. **Residual Score = 10 (High)**.
* **Priority Alignment:** **High** (Matches Residual Rating High).
* **Evidence Required for Audit Verification:** AWS CLI `get-public-access-block` export for all S3 buckets, S3 bucket policy JSON files.

---

### RSK-03: Web Application Vulnerabilities (XSS / DOM Tampering) Impacting Payment Page
* **Asset & Process:** `AST-01` (Web Storefront), `AST-07` (Stripe Payment Gateway) | Checkout & Payment Processing
* **Threat Scenario:** Threat actor exploits XSS or potentially vulnerable application dependencies to manipulate the checkout web page DOM, attempting to capture user inputs prior to Stripe iFrame form submission.
* **Vulnerability:** Web application dependency management and security controls require verification.
* **Documented Current State & Verification Condition:** Storefront built on React/Node.js on AWS ECS. `[Risk Condition to be Verified]` Dependency vulnerability status, CSP headers, and other web application security controls require verification.
* **PCI DSS Scope Context:** Stripe Elements hosts card-entry fields through Stripe-controlled components, reducing the exposure of cardholder data to ShopPulse application infrastructure. The exact applicable Self-Assessment Questionnaire (e.g., SAQ A vs SAQ A-EP) requires formal confirmation against PCI DSS v4.0 eligibility criteria.
* **Inherent Risk Justification:** **Likelihood = 4 (Likely)** — Public e-commerce web applications face incessant automated vulnerability scans and exploit attempts. **Impact = 4 (Major)** — Skimming or DOM tampering damages brand reputation and triggers significant PCI DSS compliance or contractual consequences. **Inherent Score = 16 (High)**.
* **Existing Baseline Controls:** Stripe Elements iFrame isolation; TLS 1.3 protects transit.
* **Residual Risk Justification:** **Likelihood = 3 (Possible)** — iFrame architecture prevents direct backend card recording, but parent page DOM manipulation remains possible without strict CSP headers. **Impact = 4 (Major)** — Significant reputational and legal impact. **Residual Score = 12 (High)**.
* **Priority Alignment:** **High** (Matches Residual Rating High).
* **Evidence Required for Audit Verification:** `npm audit` report, Content Security Policy (CSP) HTTP header response inspection, AWS ALB security policy configuration, formal PCI DSS v4.0 SAQ eligibility worksheet.

---

### RSK-04: Phishing & Social Engineering Targeting Remote Workforce
* **Asset & Process:** `AST-03` (Employee Endpoints), `AST-06` (Google Workspace) | Corporate Communications
* **Threat Scenario:** Adversary sends targeted spear-phishing emails to support or finance staff to steal Google Workspace login credentials.
* **Vulnerability:** Security awareness training requirements and completion status are not verified.
* **Documented Current State:** Google Workspace enforced MFA is enabled. Customer support representatives routinely handle inbound external emails, increasing exposure to phishing attempts. `[Risk Condition to be Verified]` Security awareness training requirements and completion status are not verified.
* **Inherent Risk Justification:** **Likelihood = 4 (Likely)** — Support representatives handle frequent external email communications. **Impact = 3 (Moderate)** — Email compromise allows unauthorized access to internal Google Drive docs and Zendesk tickets. **Inherent Score = 12 (High)**.
* **Existing Baseline Controls:** Google Workspace mandatory MFA blocks basic credential replay attacks; standard automated spam filter active.
* **Residual Risk Justification:** **Likelihood = 3 (Possible)** — Standard MFA reduces simple password theft, but adversary-in-the-middle (AiTM) phishing kits can capture session tokens. **Impact = 3 (Moderate)** — Limited to employee mailbox and cloud drive context. **Residual Score = 9 (Medium)**.
* **Priority Alignment:** **Medium** (Matches Residual Rating Medium).
* **Evidence Required for Audit Verification:** Google Workspace admin console security settings, DMARC/DKIM DNS record lookup, security training sign-off logs.

---

### RSK-05: Insufficient Security Incident Logging & Real-Time Monitoring
* **Asset & Process:** `AST-01` (Web Application), `AST-02` (RDS Database), `AST-05` (AWS Infrastructure) | Security Operations & Incident Response
* **Threat Scenario:** An attacker establishes unauthorized access within the cloud environment and remains undetected for weeks or months due to short log retention and lack of centralized log analysis.
* **Vulnerability:** AWS CloudWatch log retention is set to 14 days. No centralized SIEM is implemented.
* **Documented Current State:** Logs are generated independently across ECS, ALB, and RDS. CloudWatch logs retained for 14 days. No centralized log aggregator exists.
* **Inherent Risk Justification:** **Likelihood = 4 (Likely)** — Absence of log monitoring allows routine reconnaissance and initial access to proceed completely unnoticed. **Impact = 4 (Major)** — Inability to perform timely forensic analysis increases breach duration, compliance penalties, and customer churn. **Inherent Score = 16 (High)**.
* **Existing Baseline Controls:** GuardDuty is enabled; alert routing and escalation procedures require verification.
* **Residual Risk Justification:** **Likelihood = 3 (Possible)** — GuardDuty catches major threat signatures, but 14-day log deletion destroys evidence required to determine breach blast radius. **Impact = 4 (Major)** — Legal and operational impact of delayed discovery remains high. **Residual Score = 12 (High)**.
* **Priority Alignment:** **High** (Matches Residual Rating High).
* **Evidence Required for Audit Verification:** CloudWatch log group configuration export showing retention periods, GuardDuty alert destination settings.

---

### RSK-06: Customer PII Data Breach via Vulnerable API or SQL Injection
* **Asset & Process:** `AST-02` (RDS Database), `AST-01` (Web Application) | Customer Account Management
* **Threat Scenario:** Threat actor exploits an unauthenticated backend API route or a potential injection weakness in legacy reporting modules to exfiltrate customer PII in the production database.
* **Vulnerability:** `[Risk Condition to be Verified]` Legacy reporting components may contain raw SQL queries, and database credential storage practices require verification.
* **Documented Current State:** Production RDS database stores customer PII records. Application uses Sequelize ORM, but legacy reporting components require security code verification.
* **Inherent Risk Justification:** **Likelihood = 3 (Possible)** — E-commerce APIs are publicly accessible and continuously audited by external web crawlers. **Impact = 5 (Catastrophic)** — Exfiltration of customer PII triggers statutory penalties, mandatory breach notification costs, and severe reputational damage. **Inherent Score = 15 (High)**.
* **Existing Baseline Controls:** RDS PostgreSQL instance runs in a private VPC subnet without public IP routing. Data at rest encrypted via KMS AES-256.
* **Residual Risk Justification:** **Likelihood = 2 (Unlikely)** — Private subnet network security group prevents direct public internet database access on port 5432. However, application-layer SQLi or API abuse can still bypass network boundaries. **Impact = 5 (Catastrophic)** — Data exposure severity remains catastrophic. **Residual Score = 10 (High)**.
* **Priority Alignment:** **High** (Matches Residual Rating High).
* **Evidence Required for Audit Verification:** Backend source code audit for parameterized queries, AWS VPC Subnet routing tables, RDS KMS encryption verification.

---

### RSK-07: Unmonitored Third-Party Vendor Access & Shared Integration Keys
* **Asset & Process:** `AST-08` (3PL API), `AST-09` (Zendesk SaaS) | Fulfillment & Customer Support
* **Threat Scenario:** Compromise of 3PL logistics partner or support SaaS vendor allows unauthorized access to ShopPulse API keys and order management workflows.
* **Vulnerability:** `[Risk Condition to be Verified]` Static/hardcoded integration API keys require verification. Formal third-party security review and assurance-documentation requirements are not established.
* **Documented Current State:** No formal Third-Party Risk Management (TPRM) policy exists.
* **Inherent Risk Justification:** **Likelihood = 3 (Possible)** — Third-party supply chain compromise is a frequent attack vector in retail tech stacks. **Impact = 3 (Moderate)** — Compromised API key enables fraudulent order creation, shipping address manipulation, or customer ticket tampering. **Inherent Score = 9 (Medium)**.
* **Existing Baseline Controls:** HTTPS API transport; 3PL endpoint access controls require verification. Static/hardcoded integration API keys require verification.
* **Residual Risk Justification:** **Likelihood = 2 (Unlikely)** — Encrypted HTTPS transport and operational vendor interfaces reduce probability of direct key capture, though key storage policies require verification. **Impact = 3 (Moderate)** — Impact is contained to fulfillment and support operations. **Residual Score = 6 (Medium)**.
* **Priority Alignment:** **Medium** (Matches Residual Rating Medium).
* **Evidence Required for Audit Verification:** 3PL API key configuration, endpoint access-control configuration, vendor security review documentation, and applicable integration architecture/configuration records.

---

### RSK-08: Data Exposure Risk from Stolen or Lost Corporate Laptops with Unverified Disk Encryption
* **Asset & Process:** `AST-03` (Employee Corporate Endpoints) | Remote Workforce Operations
* **Threat Scenario:** An employee laptop is stolen or misplaced while traveling, allowing offline physical access to locally stored files if full-disk encryption is not enforced.
* **Vulnerability:** Full-disk encryption (FileVault / BitLocker) policy enforcement is unverified across all devices in MDM.
* **Documented Current State:** 45 corporate laptops (macOS and Windows 11) are enrolled in Jamf/Intune MDM. Disk encryption setting exists in MDM, but centralized policy enforcement reports require audit verification.
* **Inherent Risk Justification:** **Likelihood = 4 (Likely)** — Laptop loss or theft occurs regularly across remote workforces. **Impact = 3 (Moderate)** — Theft of an unencrypted hard drive exposes local downloads, cached credentials, and internal customer exports. **Inherent Score = 12 (High)**.
* **Existing Baseline Controls:** MDM enrollment enables remote device lock and wipe commands upon connection to the internet. User account password required on startup.
* **Residual Risk Justification:** **Likelihood = 2 (Unlikely)** — MDM remote wipe reduces window of exposure once device boots online. **Impact = 3 (Moderate)** — Exposure limited to single workstation files. **Residual Score = 6 (Medium)**.
* **Priority Alignment:** **Medium** (Matches Residual Rating Medium).
* **Evidence Required for Audit Verification:** Jamf Pro / Intune endpoint compliance report detailing FileVault / BitLocker enforcement status for all 45 devices.

---

### RSK-09: Prolonged Downtime Risk from Limited Disaster Recovery Readiness
* **Asset & Process:** `AST-02` (RDS Database), `AST-01` (Web Storefront) | Business Continuity & Operations
* **Threat Scenario:** Major AWS cloud region outage or database corruption event halts e-commerce operations, with no validated recovery procedure available.
* **Vulnerability:** No formal Business Continuity / Disaster Recovery (BC/DR) plan exists; RDS snapshot restoration procedures and recovery testing require verification.
* **Documented Current State:** Automated daily RDS snapshots are configured; backup retention and restoration procedures require verification. RDS availability features may provide resilience depending on deployed configuration; actual Multi-AZ configuration requires verification.
* **Inherent Risk Justification:** **Likelihood = 3 (Possible)** — Cloud service degradation or human administrative error occurs periodically. **Impact = 4 (Major)** — Extended storefront downtime (>24 hrs) during peak sales periods results in substantial revenue loss and customer defection. **Inherent Score = 12 (High)**.
* **Existing Baseline Controls:** Automated daily AWS RDS snapshots.
* **Residual Risk Justification:** **Likelihood = 2 (Unlikely)** — AWS RDS automated snapshots provide database restoration recovery baseline. However, single-region dependency leaves a vulnerability during broad region outages or logical database corruption. **Impact = 4 (Major)** — Business downtime impact remains severe. **Residual Score = 8 (Medium)**.
* **Priority Alignment:** **Medium** (Matches Residual Rating Medium).
* **Evidence Required for Audit Verification:** AWS RDS automated backup configuration settings, formal BC/DR Plan document, disaster recovery drill test reports.

---

### RSK-10: Employee Security Misconfigurations Due to Lack of Documented Information Security Policies
* **Asset & Process:** All Assets (`AST-01` through `AST-10`) | Corporate Security Governance
* **Threat Scenario:** Employees inadvertently adopt unapproved SaaS applications (Shadow IT), share sensitive customer lists via personal cloud storage, or reuse personal passwords for corporate access.
* **Vulnerability:** Absence of documented security policies (Acceptable Use Policy, Access Control Policy, Data Handling Policy).
* **Documented Current State:** ShopPulse has no written Information Security Policy framework. Security rules are communicated verbally during onboarding. In a growing distributed workforce, reliance on verbal security instructions may contribute to inconsistent policy interpretation and unvetted SaaS usage.
* **Inherent Risk Justification:** **Likelihood = 4 (Likely)** — In a growing distributed workforce, reliance on verbal security instructions may contribute to inconsistent policy interpretation and unvetted SaaS usage. **Impact = 3 (Moderate)** — Unintentional data exposure, privacy compliance gaps, and inconsistent access offboarding. **Inherent Score = 12 (High)**.
* **Existing Baseline Controls:** Verbal onboarding walkthroughs; Google Workspace basic password length enforcement (minimum 8 characters).
* **Residual Risk Justification:** **Likelihood = 3 (Possible)** — Password complexity controls mitigate brute-force attacks, but lack of written governance policies leaves Shadow IT and data handling risks active. **Impact = 3 (Moderate)** — Operational and compliance impact remains moderate. **Residual Score = 9 (Medium)**.
* **Priority Alignment:** **Medium** (Matches Residual Rating Medium).
* **Evidence Required for Audit Verification:** Written Information Security Policy suite, annual employee policy acknowledgment logs, HR onboarding documentation.
