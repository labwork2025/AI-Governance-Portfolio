# AI Governance Case Study: EcoFlow Smart Hospital HVAC

**Role:** AI Governance Officer  
**Domain:** Critical Infrastructure / Smart City  
**Project Type:** Algorithmic Impact Assessment (AIA) & Vendor Risk Management  
**Status:** Conditional Approval Granted

## 1. Executive Summary
The Regional Medical Center proposed the acquisition of "EcoFlow-Health," an AI-driven system designed to optimize HVAC energy consumption by 15%. The system required bridging the IT (Patient Data) and OT (Operational Technology) networks.

**Objective:** Assess the security, safety, and financial risks of integrating an autonomous AI agent into critical hospital infrastructure.

**Final Decision:** **CONDITIONAL APPROVAL.** The project was approved only after the vendor agreed to specific architectural changes regarding data privacy and fail-safe protocols.

---

## 2. Risk Assessment Artifact (AIA)
*The following risks were identified during the vendor interview and mitigated via contract clauses.*

| Risk Domain | Identified Risk | Risk Level | Mitigation / Control (The Condition) |
| :--- | :--- | :--- | :--- |
| **Security** | **Lateral Movement:** The AI required a bridge between BAS (Building Automation) and ADT (Patient Records), creating a path for attackers to pivot from HVAC to PII. | **HIGH** | **Data Minimization:** Vendor restricted to receiving *anonymized, aggregated counts* only. No raw PII or ADT feeds allowed. |
| **Safety** | **Operational Failure:** If the AI crashes or internet is lost, dampers could remain closed, risking air quality/infection control. | **HIGH** | **Manual Override:** Local facilities staff retain a physical "Hand-Off-Auto" switch to disconnect AI immediately without vendor intervention. |
| **Financial** | **SLA Voidance:** Manual overrides to ensure safety would void the vendor's 15% energy savings guarantee. | **MED** | **Contract Clause:** If the system is manually disabled due to a *Vendor System Failure*, the 15% savings guarantee remains valid. |

---

## 3. Governance Process Log
*Below is a summary of the audit interview conducted with the vendor to identify the risks above.*

### Phase 1: Discovery & Architecture Review
**Governance Officer:** Does this system have the ability to gain access to other core systems linked to the Building Automation System (BAS)?
**Vendor:** Yes. We need a 'Read-Only' bridge into the hospital's main network to see patient counts (ADT feed) and 'Write Access' to the JACE controllers to change airflow.

**Governance Officer:** What is the fail-safe? If the internet goes down, does a person need to come out to fix it?
**Vendor:** It is cloud-based. If it goes down, equipment stays at the last setting. Our nearest technician is 4 hours away in Miami.

### Phase 2: Risk Challenge
**Governance Officer:** This poses a critical security risk. If you have access to BAS core systems, an attacker could pivot to our patient database (PII). What are your protections?
**Vendor:** We can change the architecture to use **anonymized counts only**. Instead of "John Doe," we just see "Zone 1: 1 Patient."

**Governance Officer:** Regarding the 4-hour delay—can local staff adjust settings manually?
**Vendor:** Yes, local staff can override, but it voids the 15% Energy Savings Guarantee for that month.

### Phase 3: Negotiation & Final Ruling
**Governance Officer:** The safety risk of a 4-hour delay is unacceptable. We require the ability to manually override the system locally.

**Determination:** We will move to **Conditional Approval** with the following stipulation:
> *If the system must be overridden due to a vendor error or security threat, the vendor is liable for the performance guarantee. The hospital retains the right to sever the connection immediately for safety reasons.*

---

## 4. Key Competencies Demonstrated
* **OT/IT Convergence Security:** Assessing risks at the intersection of physical infrastructure and digital networks.
* **Privacy by Design:** Enforcing data minimization techniques (Anonymization) to protect PII.
* **Vendor Risk Management (VRM):** Negotiating Service Level Agreements (SLAs) to protect the organization from financial liability.
* **NIST AI RMF Alignment:** Mapping risks to *Map, Measure, Manage* functions.
