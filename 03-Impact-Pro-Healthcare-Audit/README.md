# Audit Log: Impact-Pro Population Health Model

**Project:** Impact-Pro (High-Risk Care Management)
**Date:** Feb 01, 2026
**Auditor:** E. Banks
**Decision:** REJECTED (Do Not Deploy)

> **Simulation Disclosure:** This case study was conducted as a dynamic role-play simulation using an LLM (Google Gemini). The scenario is based on real-world documented failures (Obermeyer et al., 2019). While the AI presented the scenario and data, the diagnostic questions, risk identification, and final rejection decision represent my own analysis during the exercise.

## 1. System Overview
Population Health Management requested approval for "Impact-Pro," a predictive model designed to identify high-risk patients for enrollment in an intensive care management program.
* **Intended Use:** Automate selection of the top 1% of "high risk" patients for extra nursing support.
* **Target Volume:** 200,000+ patient lives.
* **Input Data:** Commercial insurance claims data, excluding race and demographic labels to prevent bias.
* **Proxy Variable:** The model uses **Total Medical Expenditure** (cost) as the proxy for "Health Needs."

## 2. Critical Findings (Showstoppers)

### Finding A: Proxy Variable Failure (Cost does not equal Health)
* **Issue:** The model relies on the assumption that "Health Costs" are a direct equivalent to "Health Needs."
* **Auditor Analysis:** This assumption is flawed. Patients with higher income or better insurance access generate higher costs (more visits, more tests) than low-income patients with the same conditions.
* **Impact:** The model systematically prioritizes wealthier patients for help while overlooking sicker, low-income patients who utilize the medical system less frequently due to financial barriers.

### Finding B: Hidden Racial Bias
* **Issue:** Although "Race" was removed from the training data, the reliance on "Cost" acts as a proxy for race.
* **Real-World Context:** Research indicates that Black patients generate significantly lower medical costs than White patients for the same severity of chronic illness.
* **Consequence:** By optimizing for cost, the model reduced the selection of Black patients by more than 50% compared to a model based on biological markers.

### Finding C: Economic Disparity
* **Auditor Observation:** Patients on governmental assistance or with limited financial means would be systematically under-scored by this tool, as their lack of spending would be interpreted by the AI as "good health."

## 3. Governance Determination
**Status: REJECTED**

The model in its current form is unfit for deployment. While the removal of demographic labels was intended to ensure fairness, the decision to train on **Financial Utilization** rather than **Biological Metrics** creates a discriminatory feedback loop.

**Required Remediation:**
1.  **Change Target Variable:** The model must be retrained to predict **Biological Outcomes** (e.g., A1C flares, ER visits, mortality) rather than **Financial Cost**.
2.  **Equity Audit:** Vendor must demonstrate that the selection rate for high-need minority patients matches their actual prevalence in the sick population.
