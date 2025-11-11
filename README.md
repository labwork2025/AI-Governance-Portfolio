# AI Governance Risk Report: "T-Pot" AI Server

* **Date:** 10/31/2025
* **Analyst:** Elijah Banks
* **Asset:** "AI Server" (T-Pot Honeypot)
* **IP Address:** `192.168.52.150`

---

### 1. Executive Summary

A risk assessment was performed on the target AI Server to identify its network attack surface and validate active threats. The assessment discovered **multiple critical- and high-risk vulnerabilities**, including open, unencrypted services and a confirmed vulnerability to brute-force credential attacks.

Immediate remediation is required to mitigate the high probability of unauthorized access and a potential breach of data integrity.

---

### 2. Findings & Evidence

The assessment was conducted in three phases: Reconnaissance, Simulated Attack, and Log Analysis.

#### Evidence Packet A: Reconnaissance (Nmap Scan)
A network scan was run from an internal attacker-profile VM (`192.168.52.138`) to map the target's open ports. The scan revealed a dangerously large attack surface, violating the Principle of Least Privilege.

**Key High-Risk Services Identified:**
* `23/tcp` (Telnet): **CRITICAL.** An unencrypted protocol that transmits credentials in plain text.
* `21/tcp` (FTP): **HIGH.** An unencrypted protocol for file transfer.
* `445/tcp` (microsoft-ds): **HIGH.** The SMB protocol, a common vector for ransomware (e.g., WannaCry).
* `22/tcp` (SSH): **OPEN.** The vector for our simulated attack.

#### Evidence Packet B: Simulated Attack (Hydra)
We simulated a standard brute-force attack against the open SSH port (22) using Hydra. This mimics the most common attack pattern from low-sophistication threat actors.

**Attacker Command:**
```bash
hydra -l root -P /usr/share/wordlists/fasttrack.txt ssh://192.168.52.150
