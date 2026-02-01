# Audit Log: Talent-Rank Automated Hiring System

**Project:** Talent-Rank AI (Resume Screening Pilot)
**Date:** Feb 01, 2026
**Auditor:** E. Banks
**Decision:** REJECTED (Do Not Deploy)

## 1. System Overview
HR requested approval for "Talent-Rank," an ML-based candidate scoring engine trained on 10 years of internal hiring data.
* **Intended Use:** Automate rejection for candidates scoring below 85/100.
* **Target Volume:** 5,000+ applicants for Cyber Analyst roles.
* **Input Data:** Historical PDF resumes of "High Performers" (2015-2025).

## 2. Critical Findings (Showstoppers)

### Finding A: Sampling Bias in Training Data
* **Issue:** The model was trained exclusively on historical hires ("High Performers"). Given the lack of diversity in the legacy workforce, the model created a feedback loop, penalizing candidates who did not match the demographic or educational profile of previous hires.
* **Impact:** Systematically lower scores for diverse candidates despite equal qualifications.
* **Vendor Response:** Vendor confirmed data was not balanced with external baselines.

### Finding B: Disparate Impact on Veterans
* **Issue:** The scoring logic applies a negative weight to employment gaps greater than 6 months.
* **Impact:** This logic fails to account for military service transitions or deployment gaps, creating disparate impact against a protected class (Veterans).
* **Vendor Response:** The weight is hard-coded in the neural net and cannot be toggled off for specific groups.

### Finding C: Lack of Explainability (Black Box)
* **Issue:** Vendor cannot provide specific reasons for individual rejection decisions.
* **Regulatory Risk:** Violates transparency requirements (e.g., EEOC guidance, NYC Local Law 144) regarding adverse action notices.

## 3. Governance Determination
**Status: REJECTED**

The tool in its current state is non-compliant with fair hiring standards. The reliance on historical "success" data without synthetic balancing creates an unacceptable risk of proxy discrimination. Furthermore, the inability to explain adverse decisions exposes the organization to legal liability.

**Required Remediation for Re-Evaluation:**
1.  **Retraining:** Model must be retrained on a synthetic, balanced dataset.
2.  **White-Box Logic:** Scoring criteria must be auditable (explainable).
3.  **Gap Analysis:** "Employment Gap" logic must include exceptions for military service.
