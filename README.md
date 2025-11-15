# AI Governance Risk Report: T-Pot Server

* Date: 11/10/2025
* Analyst: Elijah Banks
* Asset: "AI Server" (T-Pot Honeypot)
* IP Address: 192.168.52.149

---

## 1. Executive Summary

I performed a risk assessment on the AI Server and identified multiple critical- and high-risk vulnerabilities. The analysis confirmed that the server is exposed via unencrypted services and is vulnerable to a standard brute-force attack. These findings were confirmed by analyzing the T-Pot SIEM (Kibana), which logged over 52,000 malicious events from our attacker VMs.

These findings require immediate remediation to prevent unauthorized access and protect the integrity of the AI system.

---

## 2. My Findings: 3-Phase Analysis

I confirmed the risk using a three-phase process: Reconnaissance, Simulated Attack, and Log Analysis.

#### Phase 1: Reconnaissance (Nmap Scan)
I scanned the target from my Kali attacker VM (192.168.52.138) to map its attack surface.

Result: The scan was immediately detected by the T-Pot's Intrusion Detection System (IDS).
* Evidence: The Kibana Suricata Alert Signature panel logged multiple "ET SCAN Possible Nmap User-Agent" alerts, confirming the reconnaissance phase.

#### Phase 2: Simulated Attack (Hydra)
I executed a standard brute-force SSH attack from the Kali VM (192.168.52.138) against the T-Pot server (192.168.52.149).

Attacker Command:
hydra -l root -P /usr/share/wordlists/fasttrack.txt ssh://192.168.52.149

Result: The attack was successful and logged by the honeypot, generating a massive amount of "noise" and confirming the vulnerability.

#### Phase 3: Log Analysis (Kibana Dashboard)
I analyzed the Kibana dashboard to confirm the full impact of the attacks. The evidence was conclusive.

Evidence: Main Dashboard (52k+ Attacks)
![Kibana Main Dashboard](https://raw.githubusercontent.com/labwork2025/AI-Governance-Portfolio/main/evidence/Screenshot%20(866).png)

* Attacker IPs Confirmed: The Attacker AS/N - Top 10 panel showed:
    * 192.168.52.138 (Kali VM) as the source of 52,071 malicious events.
    * 192.168.52.177 (Windows VM) as the source of 6 events.
* Method Confirmed: The Password Tagcloud logged the exact passwords from the attack list, including P@ssword!, 123456, and test.
* Honeypot Confirmation: The Honeypot Attacks panel showed the SSH attack was successfully captured by the Cowrie honeypot, while other automated probes were captured by Honeytrap.

Evidence: Attacker IPs and Password Tagcloud
![Kibana Attacker IP and Password Evidence](https://raw.githubusercontent.com/labwork2025/AI-Governance-Portfolio/main/evidence/Screenshot%20(869).png)

![Kibana Tagcloud Evidence](https://raw.githubusercontent.com/labwork2025/AI-Governance-Portfolio/main/evidence/Screenshot%20(868).png)

---

## 3. Risk Analysis & AI Governance Impact

This assessment proves a direct link between a technical vulnerability (open SSH port) and a confirmed, logged threat (a successful brute-force attack).

This finding directly impacts the "MAP" function of the NIST AI Risk Management Framework. We have successfully "mapped" a technical risk to a high-level business impact on the AI system.

An attacker gaining this level of access could poison the model's training data or steal the proprietary AI model itself, leading to catastrophic business and reputational damage.

---

## 4. Recommended Controls (Remediation Plan)

Based on these findings, I recommend the following controls, prioritized by severity.

#### Immediate (Critical):
1. Disable & Firewall: The Telnet (23/tcp) and FTP (21/tcp) services must be disabled and firewalled immediately.
2. Investigate & Block: The SMB (445/tcp) port should be blocked unless there is a documented and approved business justification.

#### Standard (High-Priority Hardening):
1. Disable Root Login: Configure the SSH service to prohibit direct login for the root user.
2. Implement Key-Based Authentication: Disable password-based logins for SSH and enforce the use of public/private key pairs.
