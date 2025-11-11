# AI Governance Risk Report: T-Pot Server

* **Date:** 10/31/2025
* **Analyst:** Elijah Banks
* **Asset:** "AI Server" (T-Pot Honeypot, IP: `192.168.52.150`)

---

### 1. Executive Summary

I ran a risk assessment on the AI Server and found **multiple critical- and high-risk vulnerabilities.** The server is exposed with unencrypted services and is confirmed to be vulnerable to a simple brute-force attack. These issues need to be fixed immediately to prevent unauthorized access.

---

### 2. My Findings (The 3-Step Process)

I confirmed the risk in three phases: Recon, Attack, and Log Analysis.

#### Phase 1: Reconnaissance (Nmap Scan)
I scanned the server from an attacker's perspective (`192.168.52.138`). The scan showed a massive attack surface with several high-risk ports open.

**Key Services Identified:**
* `23/tcp` (Telnet): **CRITICAL.** Sends passwords in clear text.
* `21/tcp` (FTP): **HIGH.** Unencrypted file transfer.
* `445/tcp` (SMB): **HIGH.** A primary target for ransomware.
* `22/tcp` (SSH): **OPEN.** This was the port I decided to attack.

#### Phase 2: Simulated Attack (Hydra)
I ran a standard Hydra brute-force attack against the open SSH port (22) using a common password list.

**Command:**
```bash
hydra -l root -P /usr/share/wordlists/fasttrack.txt ssh://192.168.52.150
