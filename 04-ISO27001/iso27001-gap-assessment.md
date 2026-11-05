# Deliverable 3: ISO/IEC 27001:2022 Simulated Gap Assessment

**Organization:** ShopPulse Retail Solutions Inc.  
**Assessor:** Junior GRC Analyst (Simulated Engagement)  
**Framework Baseline:** ISO/IEC 27001:2022 Annex A Controls  
**Assessment Type:** Portfolio / Simulated Gap Assessment (Non-Certification)  
**Version:** 1.2 (Final Quality Alignment & Evidence Discipline)  

---

## 1. Executive Summary & Assessment Methodology

> **Important Audit Context & Disclosure:** This assessment is a simulated portfolio engagement conducted for academic and career demonstration purposes. It is based strictly on documented current-state information, technology stack specifications, and operational assumptions defined in Phase 1. It does **NOT** claim that an actual formal audit, site inspection, or empirical evidence testing occurred, nor does it claim formal ISO/IEC 27001:2022 certification for ShopPulse Retail Solutions Inc.

### Methodology & Control Selection
This gap assessment evaluates ShopPulse's current security posture against a curated subset of **13 key controls from ISO/IEC 27001:2022 Annex A**, covering all four control themes: **Organizational (A.5)**, **People (A.6)**, **Physical (A.7)**, and **Technological (A.8)**.

### Implementation Status Definitions
* **Implemented:** Control is supported by documented technical architecture and operational baseline controls.
* **Partially Implemented:** Control exists informally, requires operational compliance verification, or is deployed unevenly across systems/departments.
* **Not Implemented:** Control is completely absent or non-operational.
* **Not Applicable (N/A):** Control falls outside the defined assessment boundary based on organizational scope rationale.

### Control Priority Derivation Methodology
Control Priority (**High**, **Medium**, **Low**, **N/A**) is directly derived from the **highest Residual Risk Rating** of its mapped Risk IDs from the Phase 2 Risk Register (`RSK-01` through `RSK-10`):
* **High Priority:** Control directly mitigates a **High Residual Risk** (e.g., `RSK-01`, `RSK-02`, `RSK-03`, `RSK-05`, `RSK-06`, Residual Score 10–15).
* **Medium Priority:** Control directly mitigates a **Medium Residual Risk** (e.g., `RSK-04`, `RSK-07`, `RSK-08`, `RSK-09`, `RSK-10`, Residual Score 6–9).
* **Low Priority:** Control mitigates Low Residual Risks or has a documented baseline implementation where operational compliance requires verification.
* **N/A:** Control is out of scope.

---

## 2. ISO/IEC 27001:2022 Control Assessment Matrix

| Control Ref | Control Theme | Control Name & Objective | Implementation Status | Related Risk ID | Related Asset ID | Control Priority & Derivation Rationale | Responsible Owner |
| :--- | :--- | :--- | :---: | :---: | :---: | :---: | :--- |
| **A.5.1** | Organizational | **Policies for Information Security:** Maintain management direction for information security. | **Not Implemented** | RSK-10 | AST-01 to AST-10 | **Medium** (Derived from RSK-10 Residual Medium) | IT Manager / HR |
| **A.5.15** | Organizational | **Access Control:** Ensure authorized user access and prevent unauthorized access. | **Partially Implemented** | RSK-01, RSK-06 | AST-05, AST-02 | **High** (Derived from RSK-01 Residual High and RSK-06 Residual High) | CTO / IT Manager |
| **A.5.19** | Organizational | **Information Security in Supplier Relationships:** Maintain security in vendor relationships. | **Not Implemented** | RSK-07 | AST-08, AST-09 | **Medium** (Derived from RSK-07 Residual Medium) | Operations Manager |
| **A.5.23** | Organizational | **Information Security for Use of Cloud Services:** Specify and manage security for cloud services. | **Partially Implemented** | RSK-01, RSK-02 | AST-05, AST-02 | **High** (Derived from RSK-02 Residual High and RSK-01 Residual High) | Lead DevOps Engineer |
| **A.6.8** | People | **Information Security Awareness & Training:** Educate personnel on security responsibilities. | **Not Implemented** | RSK-04 | AST-03, AST-06 | **Medium** (Derived from RSK-04 Residual Medium) | HR Generalist |
| **A.7.4** | Physical | **Physical Security Monitoring:** Detect physical security intrusions in facilities. | **Partially Implemented** | N/A | AST-03 | **Low** (Documented Scope Baseline; Subject to Verification) | Operations Manager |
| **A.8.5** | Technological | **Secure Authentication:** Ensure users and systems are authenticated securely. | **Partially Implemented** | RSK-01, RSK-04 | AST-05, AST-06 | **High** (Derived from RSK-01 Residual High) | IT Manager / CTO |
| **A.8.7** | Technological | **Protection Against Malware:** Ensure systems and endpoints are protected against malware. | **Partially Implemented** | N/A | AST-03 | **Low** (Baseline Implemented; Operational Compliance Requires Verification) | IT Manager |
| **A.8.8** | Technological | **Management of Technical Vulnerabilities:** Prevent exploitation of software vulnerabilities. | **Partially Implemented** | RSK-03 | AST-01, AST-04 | **High** (Derived from RSK-03 Residual High) | Lead Software Engineer |
| **A.8.9** | Technological | **Configuration Management:** Establish and monitor security configurations. | **Partially Implemented** | RSK-02 | AST-05 | **High** (Derived from RSK-02 Residual High) | Lead DevOps Engineer |
| **A.8.12** | Technological | **Data Leakage Prevention:** Detect and prevent unauthorized disclosure of sensitive data. | **Partially Implemented** | RSK-08 | AST-03 | **Medium** (Derived from RSK-08 Residual Medium) | Lead Software Eng / IT |
| **A.8.16** | Technological | **Monitoring Activities:** Detect anomalous behavior and potential security incidents. | **Not Implemented** | RSK-05 | AST-01, AST-05 | **High** (Derived from RSK-05 Residual High) | IT Manager / DevOps |
| **A.8.24** | Technological | **Use of Cryptography:** Ensure effective encryption for data transit and storage. | **Implemented** | RSK-03, RSK-06 | AST-01, AST-02 | **Low** (Baseline Implemented; Low Residual Risk) | Lead Software Engineer |

---

## 3. Detailed Control Evaluation Breakdown

### 1. Control A.5.1 — Policies for Information Security
* **Control Theme:** Organizational Controls
* **Control Objective:** Define management direction and support for information security in accordance with business requirements and regulations.
* **Implementation Status:** **Not Implemented**
* **Documented Current State:** Verbal security instructions are communicated to staff during onboarding. No formal written security policies exist.
* **Assessment Basis & Observations:** Review of company documentation confirmed no written Acceptable Use Policy (AUP), Access Control Policy, or Data Classification Standard.
* **Evidence Required for Verification:** Formal Information Security Policy document, executive approval memo, annual employee policy sign-off logs.
* **Gap Identified:** Absence of written security governance leaves employees without clear operational boundaries, increasing Shadow IT adoption.
* **Related Risk ID:** `RSK-10`
* **Control Priority Rationale:** **Medium** — Directly addresses `RSK-10` (Residual Score 9 / Medium).
* **Recommended Improvement:** Draft, approve, and publish a core Information Security Policy suite (AUP, Access Control, Data Protection).
* **Responsible Owner:** IT Manager / HR Generalist

---

### 2. Control A.5.15 — Access Control
* **Control Theme:** Organizational Controls
* **Control Objective:** Ensure user access to assets is authorized and restricted based on business and security requirements (Least Privilege).
* **Implementation Status:** **Partially Implemented**
* **Documented Current State:** Google Workspace access uses role-based groups. AWS IAM is used for cloud administration; some developer IAM users may rely on long-lived access keys, and access-review practices require verification.
* **Assessment Basis & Observations:** No AWS IAM credential report or access-review records were available for this simulated assessment. IAM access-key age, MFA enforcement, and access-review status require verification through an AWS IAM credential report and applicable IAM policy review.
* **Evidence Required for Verification:** AWS IAM JSON policy definitions, quarterly access review logs, secrets management architecture diagram.
* **Gap Identified:** Potentially excessive privileges, long-lived credentials, and incomplete access-review practices require verification and may increase credential theft exposure.
* **Related Risk ID:** `RSK-01`, `RSK-06`
* **Control Priority Rationale:** **High** — Directly addresses `RSK-01` (Residual Score 15 / High) and `RSK-06` (Residual Score 10 / High).
* **Recommended Improvement:** Implement mandatory quarterly access reviews, enforce AWS IAM temporary credentials via SSO, and migrate DB secrets to AWS Secrets Manager.
* **Responsible Owner:** CTO / IT Manager

---

### 3. Control A.5.19 — Information Security in Supplier Relationships
* **Control Theme:** Organizational Controls
* **Control Objective:** Establish processes to manage cybersecurity risks associated with third-party vendors and service providers.
* **Implementation Status:** **Not Implemented**
* **Documented Current State:** Vendors (Stripe, Zendesk, 3PL) are onboarded by department leads without IT security review or formal vendor risk evaluations.
* **Assessment Basis & Observations:** No vendor risk assessment questionnaire or Third-Party Risk Management (TPRM) documentation exists.
* **Evidence Required for Verification:** Applicable vendor security questionnaires, contractual security requirements, independent assurance reports or certifications, penetration-test summaries, and other relevant supplier assurance documentation.
* **Gap Identified:** Lack of vendor vetting creates supply chain vulnerabilities and unmonitored API integration exposure.
* **Related Risk ID:** `RSK-07`
* **Control Priority Rationale:** **Medium** — Directly addresses `RSK-07` (Residual Score 6 / Medium).
* **Recommended Improvement:** Establish a risk-based Third-Party Risk Management procedure requiring security due diligence and periodic assurance review for critical and high-risk suppliers. Evidence may include security questionnaires, contractual security requirements, SOC 2 reports, ISO certifications, penetration-test summaries, or equivalent assurance documentation where applicable.
* **Responsible Owner:** Operations Manager / IT Manager

---

### 4. Control A.5.23 — Information Security for Use of Cloud Services
* **Control Theme:** Organizational Controls
* **Control Objective:** Manage security parameters and configurations for cloud infrastructure and SaaS applications.
* **Implementation Status:** **Partially Implemented**
* **Documented Current State:** AWS infrastructure is administered through AWS cloud configuration and infrastructure management processes. Security baseline configuration and enforcement across relevant AWS services require verification.
* **Assessment Basis & Observations:** The completeness and enforcement of AWS security baselines, including S3 public-access controls and IAM security settings, require configuration-level verification.
* **Evidence Required for Verification:** AWS Config dashboard exports, S3 public access block policies, AWS IAM policy review exports.
* **Gap Identified:** Inconsistent or unverified cloud security guardrails may contribute to S3 storage misconfiguration and insufficient enforcement of cloud access controls.
* **Related Risk ID:** `RSK-01`, `RSK-02`
* **Control Priority Rationale:** **High** — Directly addresses `RSK-02` (Residual Score 10 / High) and `RSK-01` (Residual Score 15 / High).
* **Recommended Improvement:** Establish and continuously monitor AWS security baselines, including account-level S3 Block Public Access and appropriate cloud-security configuration monitoring. Evaluate AWS Security Hub or an equivalent solution where appropriate.
* **Responsible Owner:** Lead DevOps Engineer

---

### 5. Control A.6.8 — Information Security Awareness, Education and Training
* **Control Theme:** People Controls
* **Control Objective:** Ensure employees understand information security threats, responsibilities, and reporting channels.
* **Implementation Status:** **Not Implemented**
* **Documented Current State:** Employees receive informal verbal security advice during onboarding. No structured cybersecurity training is conducted.
* **Assessment Basis & Observations:** No formal security awareness training program or phishing simulation capability is documented in the current-state information available for this simulated assessment.
* **Evidence Required for Verification:** Security awareness platform training completion reports, phishing simulation success metric logs.
* **Gap Identified:** High employee vulnerability to spear-phishing and credential harvesting attacks.
* **Related Risk ID:** `RSK-04`
* **Control Priority Rationale:** **Medium** — Directly addresses `RSK-04` (Residual Score 9 / Medium).
* **Recommended Improvement:** Procure a web-based security awareness platform and launch mandatory annual training with quarterly phishing tests.
* **Responsible Owner:** HR Generalist / IT Manager

---

### 6. Control A.7.4 — Physical Security Monitoring
* **Control Theme:** Physical Controls
* **Control Objective:** Monitor physical premises to prevent unauthorized physical access or damage to assets.
* **Implementation Status:** **Partially Implemented**
* **Documented Scope Rationale:** ShopPulse does not operate data centers or physical production infrastructure. Physical security of 3PL warehouse facilities is managed through supplier relationships. ShopPulse-controlled office premises and employee endpoints remain within the organizational environment, while AWS physical infrastructure is operated by the cloud provider. The effectiveness and scope of physical security monitoring applicable to ShopPulse-controlled premises require verification.
* **Assessment Basis & Observations:** No detailed physical security monitoring evidence for ShopPulse-controlled premises was available for this simulated assessment.
* **Evidence Required for Verification:** Applicable office physical-security procedures, access-control records, visitor-management procedures, security monitoring arrangements, and relevant supplier/cloud-provider assurance documentation.
* **Gap Identified:** Physical security monitoring arrangements for ShopPulse-controlled premises are not sufficiently documented or verified within the current assessment.
* **Related Risk ID:** N/A
* **Control Priority Rationale:** **Low** — Control has a documented baseline implementation, although operational compliance requires verification.
* **Recommended Improvement:** Document physical security responsibilities for ShopPulse-controlled premises and review relevant supplier/cloud-provider physical-security assurance through supplier management.
* **Responsible Owner:** Operations Manager

---

### 7. Control A.8.5 — Secure Authentication
* **Control Theme:** Technological Controls
* **Control Objective:** Implement strong, risk-appropriate authentication mechanisms (e.g. Multi-Factor Authentication).
* **Implementation Status:** **Partially Implemented**
* **Documented Current State:** MFA is enforced on Google Workspace. AWS IAM MFA enforcement and coverage require verification, particularly for administrative and developer access.
* **Assessment Basis & Observations:** No AWS IAM credential report or equivalent MFA compliance evidence was available for this simulated assessment. AWS IAM MFA enforcement and coverage require verification through IAM policy review and credential reporting.
* **Evidence Required for Verification:** AWS IAM MFA policy JSON document, Google Workspace admin security settings export.
* **Gap Identified:** Insufficiently verified MFA enforcement for cloud administration access may increase exposure to credential theft.
* **Related Risk ID:** `RSK-01`, `RSK-04`
* **Control Priority Rationale:** **High** — Directly addresses `RSK-01` (Residual Score 15 / High).
* **Recommended Improvement:** Enforce IAM policy mandating MFA for all AWS account logins; mandate FIDO2/WebAuthn keys for administrative roles.
* **Responsible Owner:** IT Manager / CTO

---

### 8. Control A.8.7 — Protection Against Malware
* **Control Theme:** Technological Controls
* **Control Objective:** Protect systems, endpoints, and data against malicious software infection.
* **Implementation Status:** **Partially Implemented**
* **Documented Current State:** Corporate endpoints (`AST-03`) use native macOS and Windows security controls managed through Jamf/Intune MDM.
* **Assessment Basis & Observations:** Documented endpoint architecture indicates the use of native OS security controls. Centralized verification of anti-malware configuration, definition status, and enforcement across all corporate endpoints requires MDM compliance evidence.
* **Evidence Required for Verification:** Jamf Pro / Intune endpoint compliance reports showing active anti-malware protection and update status across applicable corporate devices.
* **Gap Identified:** Centralized verification of endpoint anti-malware configuration and compliance is not established in the available assessment evidence.
* **Related Risk ID:** N/A — assessed from documented endpoint security baseline.
* **Control Priority Rationale:** **Low** — Control has a documented baseline implementation, although operational compliance requires verification.
* **Recommended Improvement:** Maintain automatic OS anti-malware definition update policies via MDM and verify operational compliance telemetry.
* **Responsible Owner:** IT Manager

---

### 9. Control A.8.8 — Management of Technical Vulnerabilities
* **Control Theme:** Technological Controls
* **Control Objective:** Identify, evaluate, and patch technical software vulnerabilities in a timely manner.
* **Implementation Status:** **Partially Implemented**
* **Documented Current State:** Endpoint OS patching is managed via MDM. Application code and npm dependency vulnerabilities are reviewed informally without automated scanning.
* **Assessment Basis & Observations:** GitHub repositories lack automated dependency security scanning (Dependabot/Snyk); no scheduled penetration testing.
* **Evidence Required for Verification:** CI/CD vulnerability scan logs, Dependabot alert reports, third-party penetration test reports.
* **Gap Identified:** Un-scanned web dependencies create exposure to known software exploits and DOM tampering.
* **Related Risk ID:** `RSK-03`
* **Control Priority Rationale:** **High** — Directly addresses `RSK-03` (Residual Score 12 / High).
* **Recommended Improvement:** Enable GitHub Dependabot automated dependency alerts and integrate SAST tools into GitHub Actions pipelines.
* **Responsible Owner:** Lead Software Engineer

---

### 10. Control A.8.9 — Configuration Management
* **Control Theme:** Technological Controls
* **Control Objective:** Establish, document, monitor, and enforce secure baseline configurations for IT systems.
* **Implementation Status:** **Partially Implemented**
* **Documented Current State:** AWS cloud resources require defined and consistently enforced security configurations. S3 public-access configuration and bucket policies require verification across relevant buckets.
* **Assessment Basis & Observations:** No configuration-drift monitoring evidence was available for this simulated assessment. S3 security configuration should be verified through AWS configuration exports and applicable policy records.
* **Evidence Required for Verification:** AWS CLI S3 public access block exports, AWS Config rule evaluation reports.
* **Gap Identified:** Absence of verified configuration monitoring may allow security configuration drift or inconsistent S3 access controls.
* **Related Risk ID:** `RSK-02`
* **Control Priority Rationale:** **High** — Directly addresses `RSK-02` (Residual Score 10 / High).
* **Recommended Improvement:** Implement AWS Config rules to monitor and automatically remediate non-compliant S3 storage configurations.
* **Responsible Owner:** Lead DevOps Engineer

---

### 11. Control A.8.12 — Data Leakage Prevention (DLP)
* **Control Theme:** Technological Controls
* **Control Objective:** Detect and prevent unauthorized extraction or leakage of sensitive data across cloud infrastructure, databases, and physical endpoints.
* **Implementation Status:** **Partially Implemented**
* **Documented Current State:** Sensitive data protection relies on database KMS AES-256 storage encryption and Stripe Elements payment iFrames. Current endpoint encryption enforcement status requires verification across all corporate laptops.
* **Detailed Risk Mapping Rationale:** Application to `RSK-08`: A.8.12 is relevant to preventing unauthorized disclosure of sensitive information stored or cached on corporate endpoints, particularly in the event of lost or stolen devices.
* **Assessment Basis & Observations:** MDM telemetry reports are required to verify full-disk encryption compliance across all 45 corporate laptops.
* **Evidence Required for Verification:** Jamf Pro / Intune endpoint compliance export verifying 100% full-disk encryption enforcement, RDS KMS key policies.
* **Gap Identified:** Potential data leakage from stolen endpoint hard drives due to unverified disk encryption enforcement.
* **Related Risk ID:** `RSK-08`
* **Control Priority Rationale:** **Medium** — Directly addresses `RSK-08` (Residual Score 6 / Medium).
* **Recommended Improvement:** Enforce mandatory FileVault/BitLocker encryption policies across all corporate laptops through MDM and verify 100% compliance.
* **Responsible Owner:** Lead Software Eng / IT

---

### 12. Control A.8.16 — Monitoring Activities
* **Control Theme:** Technological Controls
* **Control Objective:** Collect, retain, analyze, and monitor log events to detect unauthorized security activity.
* **Implementation Status:** **Not Implemented**
* **Documented Current State:** System logs are stored independently in CloudWatch with a 14-day default retention. No central log aggregator or SIEM exists.
* **Assessment Basis & Observations:** CloudWatch logs expire after 14 days without centralized long-term security log aggregation or automated SIEM alert parsing.
* **Evidence Required for Verification:** CloudWatch log retention policy configuration JSON, SIEM integration telemetry logs.
* **Gap Identified:** Inability to perform timely incident detection or historical forensic analysis due to short log retention and lack of log monitoring.
* **Related Risk ID:** `RSK-05`
* **Control Priority Rationale:** **High** — Directly addresses `RSK-05` (Residual Score 12 / High).
* **Recommended Improvement:** Define security-log retention requirements based on investigation, operational, and compliance needs; extend relevant CloudWatch log retention accordingly, centralize security-relevant logs, and establish alert routing and escalation.
* **Responsible Owner:** IT Manager / Lead DevOps Engineer

---

### 13. Control A.8.24 — Use of Cryptography
* **Control Theme:** Technological Controls
* **Control Objective:** Ensure proper use of encryption algorithms and key management to protect data confidentiality and integrity.
* **Implementation Status:** **Implemented**
* **Documented Current State:** Web application traffic is protected using TLS 1.3. Production RDS database storage is encrypted at rest using AWS KMS.
* **Assessment Basis & Observations:** Assessment is based on the documented architectural baseline. Formal verification would require reviewing applicable TLS configuration, certificate configuration, AWS KMS key policies, and application authentication/storage controls.
* **Evidence Required for Verification:** TLS certificate export & AWS KMS key policy JSON.
* **Gap Identified:** None identified under current operational baseline.
* **Related Risk ID:** `RSK-03`, `RSK-06`
* **Control Priority Rationale:** **Low** — Baseline control implemented; low residual risk exposure.
* **Recommended Improvement:** Maintain annual KMS key rotation and modern cipher suite configurations.
* **Responsible Owner:** Lead Software Engineer
