# Cybersecurity Risk Assessment Methodology

**Organization:** ShopPulse Retail Solutions Inc.  
**Methodology References:** ISO 31000:2018 / ISO/IEC 27005:2022 / NIST SP 800-30 Rev. 1  
**Scoring Model:** 5x5 Semi-Quantitative Risk Matrix  
**Version:** 1.3 (Final Ground-Truth Definitions & Regulatory Scope)  

---

## 1. Risk Assessment Overview & Framework Alignment

This risk assessment methodology defines a standardized, repeatable process for identifying, analyzing, evaluating, and prioritizing cybersecurity risks at **ShopPulse Retail Solutions Inc.**

The methodology references international risk management standards:
* **ISO 31000:2018** — Risk Management Guidelines
* **ISO/IEC 27005:2022** — Information security risk management
* **NIST SP 800-30 Rev. 1** — Guide for Conducting Risk Assessments

> **Assessment Convention Note:** The 5x5 scoring matrix and thresholds are the assessment conventions selected for this simulated engagement. International standards provide risk management principles but do not mandate this exact matrix design.

---

## 2. Risk Calculation Formula & Core Definitions

Risk is evaluated using a semi-quantitative **5x5 Matrix** comparing **Inherent Risk** and **Residual Risk**:

$$\text{Risk Score} = \text{Likelihood Rating (1--5)} \times \text{Impact Rating (1--5)}$$

* **Inherent Risk:** The level of risk assessed before considering the effectiveness of existing security controls.
* **Residual Risk:** The remaining level of risk assessed after considering the effectiveness of existing baseline security controls.
* **Minimum Possible Score:** $1 \times 1 = 1$
* **Maximum Possible Score:** $5 \times 5 = 25$

---

## 3. Likelihood Rating Scale (1 to 5)

Likelihood represents the probability of a threat source exploiting a vulnerability within a 12-month evaluation window.

> **Likelihood Disclaimer:** Frequency expectations are qualitative assessment bands used for this simulated engagement and do not represent measured historical incident frequency.

| Rating | Level | Description & Probability Criteria | Frequency Expectation Band |
| :---: | :--- | :--- | :--- |
| **1** | **Rare** | Highly improbable. Requires extreme skill, rare vulnerability combinations, or extreme effort. | Less than once every 5+ years |
| **2** | **Unlikely** | Improbable but possible. Threat source has low motivation or controls significantly hinder exploitation. | Once every 2 to 5 years |
| **3** | **Possible** | Might occur. Threat source has moderate capability and vulnerability is known or easily discovered. | Once per year |
| **4** | **Likely** | High probability. Threat source possesses capability and vulnerability is unpatched or common. | Multiple times per year |
| **5** | **Almost Certain** | Expected to occur. Vulnerability is actively targeted, automated, or publicly exposed without controls. | Continuous / Monthly occurrence |

---

## 4. Impact Rating Scale (1 to 5)

Impact measures the potential harm to ShopPulse across four primary dimensions: **Financial Loss**, **Operational Disruption**, **Regulatory / Compliance Consequences**, and **Reputational Damage**.

| Rating | Level | Financial Loss | Operational Disruption | Regulatory / Compliance Consequences | Reputational Damage |
| :---: | :--- | :--- | :--- | :--- | :--- |
| **1** | **Negligible** | < $5,000 | Minor glitch; < 1 hr non-critical system downtime | No regulatory or contractual implications | Internal annoyance; no public exposure |
| **2** | **Minor** | $5,000 – $25,000 | Short outage (< 4 hrs); minimal customer impact | Minor non-compliance note; negligible penalty | Minimal localized negative customer feedback |
| **3** | **Moderate** | $25,000 – $100,000 | Core checkout degraded for 4–12 hrs; order delays | Potential privacy notice required; small fine | Local press or moderate social media coverage |
| **4** | **Major** | $100,000 – $500,000 | Major checkout outage (12–48 hrs); business paralyzed | Formal regulatory investigation or significant PCI DSS compliance consequences | National media exposure; significant churn |
| **5** | **Catastrophic** | > $500,000 | Extended outage (> 48 hrs); permanent data loss | Severe statutory, contractual, regulatory, or litigation consequences | Severe brand destruction; loss of customer trust |

---

## 5. Risk Matrix & Severity Thresholds

The intersection of Likelihood and Impact yields the overall Risk Level rating.

```text
                  LIKELIHOOD ──►
IMPACT  │    1        2        3        4        5
  ▼     │  Rare   Unlikely Possible  Likely  Almost Certain
────────┼──────────────────────────────────────────────
5 Catast│   5 (M)   10 (H)   15 (H)   20 (C)   25 (C)
4 Major │   4 (L)    8 (M)   12 (H)   16 (H)   20 (C)
3 Moder │   3 (L)    6 (M)    9 (M)   12 (H)   15 (H)
2 Minor │   2 (L)    4 (L)    6 (M)    8 (M)   10 (H)
1 Neglig│   1 (L)    2 (L)    3 (L)    4 (L)    5 (M)
```

### Risk Level Definitions & Priority Alignment

| Risk Score Range | Severity Level | Color Code | Action & Escalation Requirements | Priority Alignment |
| :---: | :--- | :---: | :--- | :---: |
| **17 – 25** | **Critical** | **Red** | **Immediate Action Required (0–30 Days):** Severe risk to enterprise operations or compliance. | Critical |
| **10 – 16** | **High** | **Orange** | **Prompt Action Required (31–90 Days):** Significant business or operational threat. | High |
| **5 – 9** | **Medium** | **Yellow** | **Planned Action (91–180 Days):** Moderate risk managed via standard operational cycles. | Medium |
| **1 – 4** | **Low** | **Green** | **Acceptable / Monitor:** Minimal impact. Managed during routine maintenance. | Low |

---

## 6. Defensibility & Rationale for Methodology Choice

* **Why a 5x5 Matrix over 3x3:** A 3x3 matrix flattens risk nuance, making it difficult to distinguish between minor operational bugs and catastrophic regulatory privacy breaches. The 5x5 matrix allows clear separation between high-frequency low-impact events vs. low-frequency high-impact events.
* **Multi-Dimensional Impact Scoring:** E-commerce businesses face severe reputational and compliance penalties even when direct immediate financial loss appears small. Evaluating impact across financial, operational, regulatory, and reputational vectors ensures realistic executive risk visibility.
