# Cybersecurity Risk & Compliance Assessment: ShopPulse Retail Solutions Inc.

> **Project Type:** Simulated Junior GRC Analyst Portfolio Project  
> **Author:** Pooja Dheeraj Sindhu  
> **Frameworks:** ISO/IEC 27001:2022 | NIST Cybersecurity Framework (CSF) v2.0 | ISO 31000 / NIST SP 800-30 Rev. 1

---

## Executive Overview & Project Objective

This repository contains a realistic, end-to-end **Governance, Risk, and Compliance (GRC)** assessment conducted for **ShopPulse Retail Solutions Inc.**, a fictional mid-sized e-commerce organization.

The objective of this project is to demonstrate practical entry-level GRC competency across **asset classification**, **cybersecurity risk assessment**, **ISO/IEC 27001:2022 gap analysis**, **NIST CSF 2.0 mapping**, **risk treatment planning**, and **executive security reporting**.

---

## Organizational & Technology Context

* **Company Profile:** ShopPulse Retail Solutions Inc. is a direct-to-consumer (D2C) and B2B apparel retailer based in Austin, TX (~45 employees + 15 contractors; 2 outsourced 3PL warehouses).
* **Cloud Architecture:** Hosted on AWS (US-East-1) using ECS containers, RDS PostgreSQL multi-AZ database, and S3 storage.
* **Payment Architecture:** Integrates Stripe Elements iFrames for card checkout, significantly reducing internal PCI DSS scope by preventing cardholder data from landing on company servers.
* **Security Governance:** No dedicated CISO; cybersecurity responsibilities informally shared between the IT Manager and Lead DevOps Engineer.

---

## Assessment Methodology & Scope

* **Risk Scoring Model:** 5x5 Semi-Quantitative Risk Matrix ($\text{Risk Score} = \text{Likelihood 1--5} \times \text{Impact 1--5}$).
* **Assessment Scope:** AWS cloud infrastructure, web storefront backend, RDS PostgreSQL database, 45 corporate endpoint laptops, third-party SaaS tools (Google Workspace, Zendesk), and integration APIs (Stripe, 3PL WMS).
* **Ground-Truth Labeling:** Every finding explicitly distinguishes `[Documented Current State]`, `[Assumptions]`, `[Conditions to be Verified]`, and `[Evidence Required]`.

---

## Deliverables & Repository Navigation

All assessment deliverables are organized cleanly within this repository:

| Deliverable | Description & Focus Area | Format Links |
| :--- | :--- | :--- |
| **01 — Organization Profile** | Company background, tech stack, data flows, CIA ratings, PCI DSS scope notes. | [organization-profile.md](file:///C:/Users/Lenovo/.gemini/antigravity/scratch/GRC-Risk-Compliance-Assessment/01-Organization-Profile/organization-profile.md) |
| **02 — Asset Inventory** | 10 classified assets (`AST-01` to `AST-10`) with CIA impact levels & criticality. | [asset-inventory.md](file:///C:/Users/Lenovo/.gemini/antigravity/scratch/GRC-Risk-Compliance-Assessment/02-Asset-Inventory/asset-inventory.md) \| [.csv](file:///C:/Users/Lenovo/.gemini/antigravity/scratch/GRC-Risk-Compliance-Assessment/02-Asset-Inventory/asset-inventory.csv) |
| **03 — Risk Register** | 10 risk evaluations (`RSK-01` to `RSK-10`) comparing Inherent vs. Residual Risk. | [risk-register.md](file:///C:/Users/Lenovo/.gemini/antigravity/scratch/GRC-Risk-Compliance-Assessment/03-Risk-Assessment/risk-register.md) \| [.csv](file:///C:/Users/Lenovo/.gemini/antigravity/scratch/GRC-Risk-Compliance-Assessment/03-Risk-Assessment/risk-register.csv) |
| **04 — ISO 27001 Gap Assessment** | Simulated gap analysis of 13 Annex A controls across Organizational, People, & Tech themes. | [iso27001-gap-assessment.md](file:///C:/Users/Lenovo/.gemini/antigravity/scratch/GRC-Risk-Compliance-Assessment/04-ISO27001/iso27001-gap-assessment.md) \| [.csv](file:///C:/Users/Lenovo/.gemini/antigravity/scratch/GRC-Risk-Compliance-Assessment/04-ISO27001/iso27001-gap-assessment.csv) |
| **05 — NIST CSF 2.0 Mapping** | Posture alignment across the 6 Functions of official NIST CSF 2.0. | [nist-csf-assessment.md](file:///C:/Users/Lenovo/.gemini/antigravity/scratch/GRC-Risk-Compliance-Assessment/05-NIST-CSF/nist-csf-assessment.md) \| [.csv](file:///C:/Users/Lenovo/.gemini/antigravity/scratch/GRC-Risk-Compliance-Assessment/05-NIST-CSF/nist-csf-assessment.csv) |
| **06 — Risk Treatment Plan** | Mitigation strategies, primary treatment decisions, and independent residual evaluations. | [risk-treatment-plan.md](file:///C:/Users/Lenovo/.gemini/antigravity/scratch/GRC-Risk-Compliance-Assessment/06-Risk-Treatment/risk-treatment-plan.md) \| [.csv](file:///C:/Users/Lenovo/.gemini/antigravity/scratch/GRC-Risk-Compliance-Assessment/06-Risk-Treatment/risk-treatment-plan.csv) |
| **07 — Final GRC Assessment Report** | Comprehensive executive management report detailing findings, gaps, and roadmap. | [final-grc-assessment.md](file:///C:/Users/Lenovo/.gemini/antigravity/scratch/GRC-Risk-Compliance-Assessment/07-Final-Report/final-grc-assessment.md) |
| **08 — Remediation Roadmap** | Phased 0–30, 31–90, and 91–180 day implementation schedule with assigned roles. | [remediation-roadmap.md](file:///C:/Users/Lenovo/.gemini/antigravity/scratch/GRC-Risk-Compliance-Assessment/08-Remediation-Roadmap/remediation-roadmap.md) \| [.csv](file:///C:/Users/Lenovo/.gemini/antigravity/scratch/GRC-Risk-Compliance-Assessment/08-Remediation-Roadmap/remediation-roadmap.csv) |

---

## Repository Directory Structure

```text
GRC-Risk-Compliance-Assessment/
│
├── README.md                              <- Project overview & repository index
├── 01-Organization-Profile/
│   └── organization-profile.md            <- Company background, tech stack, data flows, posture
├── 02-Asset-Inventory/
│   ├── asset-inventory.md                 <- Classified hardware, software, data & cloud assets
│   └── asset-inventory.csv                <- Asset inventory spreadsheet deliverable
├── 03-Risk-Assessment/
│   ├── risk-methodology.md                <- 5x5 Likelihood/Impact risk scoring methodology
│   ├── risk-register.md                   <- Comprehensive Cybersecurity Risk Register
│   └── risk-register.csv                  <- Risk Register spreadsheet deliverable
├── 04-ISO27001/
│   ├── iso27001-gap-assessment.md        <- ISO/IEC 27001:2022 Annex A control gap assessment
│   └── iso27001-gap-assessment.csv        <- ISO 27001 gap assessment spreadsheet deliverable
├── 05-NIST-CSF/
│   ├── nist-csf-assessment.md            <- NIST CSF 2.0 mapping across 6 core functions
│   └── nist-csf-assessment.csv            <- NIST CSF 2.0 mapping spreadsheet deliverable
├── 06-Risk-Treatment/
│   ├── risk-treatment-plan.md            <- Risk Treatment Plan & primary treatment decisions
│   └── risk-treatment-plan.csv            <- Risk Treatment Plan spreadsheet deliverable
├── 07-Final-Report/
│   └── final-grc-assessment.md            <- Final Executive Management GRC Assessment Report
└── 08-Remediation-Roadmap/
    ├── remediation-roadmap.md            <- Phased 0-30, 31-90, 91-180 day remediation schedule
    └── remediation-roadmap.csv            <- Remediation Roadmap spreadsheet deliverable
```

---

## Portfolio Disclaimer & Ground-Truth Context

> **IMPORTANT DISCLAIMER FOR RECRUITERS & AUDITORS:**  
> This project is a **simulated portfolio assessment** created strictly for academic demonstration and job application purposes.  
> 
> * **Fictional Entity:** ShopPulse Retail Solutions Inc. is a fictional e-commerce organization.
> * **Non-Audit Declaration:** This project does **not** represent an actual audit, formal ISO 27001 certification, PCI DSS attestation of compliance, or commercial consulting engagement.
> * **No False Claims:** No actual management approvals, commercial cyber insurance purchases, external penetration tests, or technical remediations have occurred.
