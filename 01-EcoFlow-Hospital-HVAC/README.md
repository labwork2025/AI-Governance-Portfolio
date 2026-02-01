# Audit Log: EcoFlow Smart Hospital HVAC

**Project:** EcoFlow-Health (Autonomous BAS Integration)
**Date:** Jan 20, 2026
**Auditor:** E. Banks
**Decision:** CONDITIONAL APPROVAL (Pending Remediation)

## 1. System Overview
Facilities Management requested approval for "EcoFlow-Health," an AI agent designed to interface with the Hospital Building Automation System (BAS) to optimize energy usage.
* **Intended Use:** Autonomous control of VAV boxes, dampers, and chillers to reduce energy spend by 15%.
* **Connectivity:** Requires read-access to IT network (ADT feeds) and write-access to OT network (JACE controllers).
* **Fail-Safe Mode:** Cloud-based control loop with default "hold last setting" on connection loss.

## 2. Critical Findings

### Finding A: IT/OT Segmentation Risk (Lateral Movement)
* **Issue:** The proposed architecture required a direct bridge between the clinical IT network (Patient ADT feeds) and the BAS OT network.
* **Impact:** High risk of lateral movement. An attacker compromising the HVAC controller could pivot to the clinical network to exfiltrate PII.
* **Vendor Response:** Vendor agreed to modify architecture to accept only anonymized, aggregated zone counts rather than raw ADT data.

### Finding B: Operational Safety (Fail-Safe)
* **Issue:** The default fail-safe ("Hold Last Setting") is unsafe for critical care environments. If the AI crashes while dampers are closed to save energy, airflow could cease, violating infection control standards.
* **Impact:** Potential for airborne pathogen spread or patient suffocation risk during an outage.
* **Vendor Response:** Validated that local facilities staff can physically override the system via "Hand-Off-Auto" switches.

### Finding C: Vendor SLA & Financial Risk
* **Issue:** The "15% Energy Savings Guarantee" contract clause was voidable if local staff manually overrode the AI.
* **Impact:** This created a perverse incentive for staff to delay safety interventions to preserve financial savings.
* **Vendor Response:** Contract amended to allow manual overrides without penalty if the root cause is a vendor system failure.

## 3. Governance Determination
**Status: CONDITIONAL APPROVAL**

The system is approved for deployment subject to the execution of the following controls. The original architecture presented an unacceptable security risk to patient data and operational safety.

**Conditions for Deployment:**
1.  **Data Minimization:** Implementation of the data aggregation script to ensure no raw PII touches the vendor's cloud.
2.  **Safety Protocol:** Installation of physical manual override switches in the Facilities Command Center.
3.  **Contract Revision:** Execution of the amended SLA clause protecting the energy savings guarantee during safety events.
