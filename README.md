# AI Governance Risk Report: T-Pot Server

* **Date:** 10/31/2025
* **Analyst:** Elijah Banks
* **Asset:** "AI Server" (T-Pot Honeypot)
* **IP Address:** `192.168.52.150`

---

### 1. Executive Summary

I performed a risk assessment on the AI Server and identified **multiple critical- and high-risk vulnerabilities.** The analysis confirmed that the server is exposed via unencrypted services and is vulnerable to a standard brute-force attack. These findings require immediate remediation to prevent unauthorized access and protect the integrity of the AI system.

---

### 2. My Findings: 3-Phase Analysis

I confirmed the risk using a three-phase process: Reconnaissance, Simulated Attack, and Log Analysis.

#### Phase 1: Reconnaissance (Nmap Scan)
I scanned the target from an attacker's perspective (`192.168.52.138`) to map its attack surface. The scan revealed several high-risk services, indicating a clear violation of the Principle of Least Privilege.

**Key Services Identified:**
* `23/tcp` (Telnet): **CRITICAL.** An unencrypted protocol that transmits credentials in plain text.
* `21/tcp` (FTP): **HIGH.** An unencrypted protocol for file transfer.
* `445/tcp` (SMB): **HIGH.** A common vector for ransomware.
* `22/tcp` (SSH): **OPEN.** This was the vector I selected for the simulated attack.

#### Phase 2: Simulated Attack (Hydra)
I executed a standard brute-force attack against the open SSH port (22) using Hydra and a common wordlist.

**Attacker Command:**
```bash
hydra -l root -P /usr/share/wordlists/fasttrack.txt ssh://192.168.52.150
