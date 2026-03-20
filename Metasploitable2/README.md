<div align="center">

# 🧠 Metasploitable2

## Initial Access & Root Exploitation via Exposed Bindshell

![Category](https://img.shields.io/badge/Category-Network%20Exploitation-red?style=for-the-badge)
![Focus](https://img.shields.io/badge/Focus-Service%20Enumeration-blue?style=for-the-badge)
![Method](https://img.shields.io/badge/Method-Direct%20Shell%20Access-success?style=for-the-badge)

</div>

---

### 🎯 Objective

Perform reconnaissance and vulnerability analysis against a deliberately vulnerable Linux system (**Metasploitable2**) to identify exposed services and achieve root-level access.

The goal was to simulate a real-world penetration testing workflow by:

* enumerating open ports and services
* identifying misconfigurations or vulnerabilities
* exploiting the easiest attack path to gain access

This lab focused on **network enumeration and initial access techniques**.

---

### 🖥 Environment

| Tool            | Purpose                            |
| --------------- | ---------------------------------- |
| Kali Linux      | Attacker machine                   |
| Metasploitable2 | Vulnerable target                  |
| Nmap            | Service and version enumeration    |
| Netcat          | Manual exploitation (shell access) |
| VMware          | Virtual lab environment            |

---

### 📦 Step 1 — Lab Setup & Connectivity

The lab environment was configured using two virtual machines:

* **Kali Linux (attacker)**
* **Metasploitable2 (target)**

Both systems were placed on the same NAT network to enable communication.

Connectivity was verified by confirming both systems received IP addresses in the same subnet and successfully responding to ICMP requests.

---

### 🔍 Step 2 — Service Enumeration

An Nmap scan was performed to identify open ports and running services on the target system.

```bash
nmap -sC -sV 192.168.74.129
```

---

### 🔑 Key Findings

| Port     | Service       | Version      | Notes                             |
| -------- | ------------- | ------------ | --------------------------------- |
| 21       | FTP           | vsftpd 2.3.4 | Known backdoor vulnerability      |
| 23       | Telnet        | -            | Insecure remote access            |
| 80       | HTTP          | Apache 2.2.8 | Web server                        |
| 445      | SMB           | Samba 3.0.20 | Potential lateral movement vector |
| **1524** | **bindshell** | -            | 🚨 Direct root access             |
| 3306     | MySQL         | 5.0.51       | Database exposure                 |
| 8180     | Tomcat        | 5.5          | Web application interface         |

---

#### 🔎 Analytical Observation

The presence of an open service on port **1524** identified as a bindshell is a critical finding.

A bindshell allows an attacker to connect directly to a listening service that provides command execution capabilities—often without authentication.

This represents a **severe misconfiguration** and an immediate attack vector.

---

### 🧪 Step 3 — Exploitation (Direct Shell Access)

Given the exposed bindshell, exploitation focused on establishing a direct connection to the service.

```bash
nc 192.168.74.129 1524
```

---

### 🔄 Step 4 — Access Validation

Upon connecting to the service, a command shell was immediately available.

```bash
whoami
```

**Output:**

```bash
root
```

This confirmed that the service provided **unauthenticated root-level access**.

---

### 🔐 Step 5 — Confirm Exploitation Success

📸 **Root Shell via Netcat**

<img src="../images/metasploitable_bindshell_root.png" width="600">

The ability to obtain a root shell without authentication demonstrates a complete system compromise.

---

## 🧠 Methodology Framework Applied

```
Network discovery
      ↓
Service enumeration
      ↓
Vulnerability identification
      ↓
Attack path prioritization
      ↓
Direct exploitation
      ↓
Privilege validation (root access)
```

---

## 🛠 Techniques Used

Primary techniques used:

* network scanning (Nmap)
* service enumeration
* vulnerability identification
* manual exploitation (Netcat)

Key concept investigated:

```
Exposed network services and unauthorized remote access
```

---

## 🛡 Defensive Insight

This scenario highlights the risks of exposing unnecessary or misconfigured services.

An open bindshell provides immediate system access and represents a critical failure in system hardening.

To mitigate this type of vulnerability, organizations should:

* restrict unnecessary open ports
* enforce authentication on all remote services
* implement firewall rules and network segmentation
* monitor for unauthorized listening services
* conduct regular vulnerability scans

Systems should follow the principle of **least exposure**, minimizing the attack surface.

---

## 💡 Skills Reinforced

* network enumeration and analysis
* vulnerability identification
* exploitation prioritization
* manual shell access techniques
* understanding of insecure service exposure

---

<div align="center">

🔍 Enumeration reveals hidden attack paths
💥 Misconfigured services lead to full compromise
🔐 Reduce attack surface to improve security

</div>
