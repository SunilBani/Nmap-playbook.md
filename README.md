# Nmap-playbook.md
Nmap (Network Mapper) is an open-source security auditing and network discovery tool. It is the industry standard for penetration testers and sysadmins to map out a network and identify "what is running where."

Core Capabilities:
Host Discovery: Identifying live hosts on a network (e.g., "Is this server up?").
Port Scanning: Discovering which ports are open (e.g., Web, Database, SSH).
Service Version Detection: Determining the specific version of software running (e.g., Apache 2.2.8).
OS Detection: Guessing the operating system of the target.
Scripting Engine (NSE): Automating advanced tasks like vulnerability detection and exploitation.
Command,Purpose
nmap -sT [IP],TCP Connect Scan: Completes the 3-way handshake.
nmap -sS [IP],SYN Scan (Stealth): Faster and more subtle than a full connect scan.
nmap -sV [IP],Version Detection: Probes ports to determine service versions.
nmap -sC [IP],Default Scripts: Runs common NSE scripts for service enumeration.
nmap -Pn [IP],No Ping: Skips host discovery; assumes the host is up.
nmap -p- [IP],"All Ports: Scans all 65,535 TCP ports."

Vulnerability Assessment Report
Target: 192.168.1.3 (Metasploitable 2)
Date: February 11, 2026
Status: CRITICAL RISKA. Executive Summary (Expanded)
1. Overview of Engagement
A point-in-time Vulnerability Assessment was conducted on the host 192.168.1.3 to identify security weaknesses, misconfigurations, and outdated software. The objective was to evaluate the system's resilience against internal and external threats.

2. Key Findings & Critical Risks
The assessment revealed a Critical Security Posture, characterized by the presence of multiple "Low-Hanging Fruit" vulnerabilities that are trivial for an attacker to exploit.
Unauthenticated Remote Access: The discovery of an active Bind Shell on Port 1524 represents a total breakdown of access control. This allows any network participant to gain "Root" (administrative) privileges without providing credentials, bypassing all security layers.
Malicious Software Backdoors: The identification of vsftpd version 2.3.4 and UnrealIRCd indicates that the system is running software intentionally tampered with by attackers (supply-chain compromise). These backdoors provide hidden entry points for remote command execution.
Clear-text Information Leakage: Legacy protocols such as Telnet (Port 23) and RSH (Ports 512-514) were found active. Because these protocols do not use encryption, an attacker performing a "Man-in-the-Middle" (MitM) attack can sniff the network traffic to capture administrative passwords and sensitive session data in plain text.
Lateral Movement Potential: Services like Samba (SMB) and NFS are misconfigured to share system information and file structures with "Anonymous" or "Guest" users. This facilitates Lateral Movement, allowing an attacker who has compromised one machine to easily navigate and infect other systems on the same network.

4. Strategic Impact
If left unaddressed, these vulnerabilities could lead to:
Full System Takeover: Attackers gaining complete control over the operating system.
Data Breach: Unauthorized access to the MySQL and PostgreSQL databases discovered on the host.
Compliance Failure: Violation of standard security frameworks (like PCI-DSS or ISO 27001) which strictly prohibit the use of unencrypted legacy protocols and unpatched "Critical" vulnerabilities.
