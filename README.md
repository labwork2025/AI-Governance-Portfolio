AI Governance Risk Report: Month 1
Date: 10/31/2025 Analyst: Elijah Banks Asset: "AI Server" (T-Pot Honeypot, IP: 192.168.52.150)

1. Executive Summary
A risk assessment was performed on the target AI Server to identify its network attack surface and validate active threats. The assessment discovered multiple critical- and high-risk vulnerabilities, including open, unencrypted services and a confirmed vulnerability to brute-force credential attacks. Immediate remediation is required to mitigate the high probability of unauthorized access and a potential breach of data integrity.

2. Findings & Evidence
The assessment was conducted in three phases: Reconnaissance, Simulated Attack, and Log Analysis.

Evidence Packet A: Reconnaissance (Nmap Scan)
A network scan was run from an internal attacker-profile VM (192.168.52.138) to map the target's open ports. The scan revealed a dangerously large attack surface, violating the Principle of Least Privilege.

Key High-Risk Services Identified:

23/tcp (Telnet): CRITICAL. An unencrypted protocol that transmits credentials in plain text.

21/tcp (FTP): HIGH. An unencrypted protocol for file transfer.

445/tcp (microsoft-ds): HIGH. The SMB protocol, a common vector for ransomware (e.g., WannaCry).

22/tcp (SSH): OPEN. The vector for our simulated attack.

Evidence Packet B: Simulated Attack (Hydra)
We simulated a standard brute-force attack against the open SSH port (22) using hydra. This mimics the most common attack pattern from low-sophistication threat actors.

Attacker Command:

Bash

hydra -l root -P /usr/share/wordlists/fasttrack.txt ssh://192.168.52.150
Result: The tool successfully ran 407 password attempts against the root user.

Evidence Packet C: Log Analysis (Kibana Dashboard)
We analyzed the server's internal logs via the Kibana dashboard to confirm the simulated attack was seen by the victim. The "Cowrie" (SSH Honeypot) dashboard provided irrefutable proof:

Attacker IP Confirmed: The Src IP - Top 10 panel identified our attacker VM (192.168.52.138) as the source of 407 malicious login events.

Target Username Confirmed: The Username Tagcloud panel showed root as the primary target.

Attack Method Confirmed: The Password Tagcloud panel logged the exact password list from our attack (P@ssword!, 123456, test, admin, etc.).

3. Risk Analysis & Governance Impact
This exercise successfully links a potential vulnerability (an open port) to a proven threat (a logged brute-force attack).

This finding directly impacts the "MAP" function of the NIST AI Risk Management Framework. We have "mapped the context" of the AI system and identified technical risks that threaten its integrity and security. An attacker who successfully guesses a password could gain access to the server, potentially poison the training data, or steal the AI model.

4. Recommended Controls (Remediation)
Based on this evidence, the following controls are recommended:

Immediate (Critical):

Disable and firewall the 23/tcp (Telnet) and 21/tcp (FTP) services immediately.

Investigate and block the 445/tcp (SMB) port unless there is an urgent, documented business need.

Standard (High):

Configure the SSH service to disable direct root login.

Implement key-based authentication for SSH and disable password-based logins entirely.
