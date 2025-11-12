# AI Governance Risk Report: T-Pot Server

* **Date:** 11/10/2025
* **Analyst:** Elijah Banks
* **Asset:** "AI Server" (T-Pot Honeypot)
* **IP Address:** `192.168.52.149`

---

### 1. Executive Summary

I performed a risk assessment on the AI Server and identified **multiple critical- and high-risk vulnerabilities.** The analysis confirmed that the server is exposed via unencrypted services and is vulnerable to a standard brute-force attack. These findings were confirmed by analyzing the T-Pot SIEM (Kibana), which logged over 52,000 malicious events from my attacker VMs.

These findings require immediate remediation to prevent unauthorized access and protect the integrity of the AI system.

---

### 2. My Findings: 3-Phase Analysis

I confirmed the risk using a three-phase process: Reconnaissance, Simulated Attack, and Log Analysis.

#### Phase 1: Reconnaissance (Nmap Scan)
I scanned the target from my Kali attacker VM (`192.168.52.138`) to map its attack surface.

**Result:** The scan was immediately detected by the T-Pot's Intrusion Detection System (IDS).
* **Evidence:** The Kibana `Suricata Alert Signature` panel logged multiple "ET SCAN Possible Nmap User-Agent" alerts, confirming the reconnaissance phase.

#### Phase 2: Simulated Attack (Hydra)
I executed a standard brute-force SSH attack from the Kali VM (`192.168.52.138`) against the T-Pot server (`192.168.52.149`).

**Attacker Command:**
```bash
hydra -l root -P /usr/share/wordlists/fasttrack.txt ssh://192.168.52.149
