<div align="center">

# 🧠 Metasploitable2  
## Enumeration & Root Exploitation via Exposed Bindshell

![Category](https://img.shields.io/badge/Category-Network%20Exploitation-red?style=for-the-badge)
![Focus](https://img.shields.io/badge/Focus-Service%20Enumeration-blue?style=for-the-badge)
![Method](https://img.shields.io/badge/Method-Manual%20Exploitation-success?style=for-the-badge)

</div>

---

### 🎯 Objective

Perform enumeration on a vulnerable Linux system, identify exposed services, and determine a viable path to gain root-level access.

The system contained multiple known vulnerabilities, requiring analysis to determine the most effective exploitation strategy.

This challenge focused on **service enumeration, vulnerability validation, and manual exploitation techniques**.

---

### 🖥 Environment

| Tool | Purpose |
|-----|------|
| Kali Linux | Attacker machine |
| Metasploitable2 | Vulnerable target |
| Nmap | Service enumeration |
| Netcat | Exploitation |

---

### 📦 Step 1 — Perform Enumeration

The target system was scanned:

`nmap -sC -sV 192.168.74.129`

This revealed numerous open ports and services.

---

### 🔍 Step 2 — Analyze Exposed Services

The scan identified multiple potential attack vectors.

Key finding:

`1524/tcp open  bindshell`

This indicated a service capable of providing direct shell access.

---

#### 🔎 Analytical Observation

A bindshell listens for incoming connections and can provide immediate command execution if exposed.

This makes it a high-priority target during enumeration.

---

### 🧪 Step 3 — Attempt Alternative Exploit

An attempt was made to exploit the vsftpd backdoor:

`nc 192.168.74.129 6200`

📸 **Backdoor Attempt Failed**

<img src="../images/vsftpd_failed.png" width="700">

The connection was refused, indicating the exploit path was not viable.

---

#### 🔎 Analytical Observation

Not all vulnerabilities are exploitable in practice.

Effective attackers validate findings and pivot when necessary.

---

### 🔄 Step 4 — Pivot to Bindshell

After the failed attempt, attention shifted to the bindshell on port 1524.

This represented a simpler and more reliable attack path.

---

### 💥 Step 5 — Exploit the Bindshell

A connection was established:

`nc 192.168.74.129 1524`

📸 **Root Shell Established**

<img src="../images/root_shell.png" width="700">

A shell was immediately obtained.

---

### 🔐 Step 6 — Confirm Root Access

To verify privileges:

`whoami`

📸 **Privilege Confirmation**

<img src="../images/whoami_root.png" width="700">

Output:

`root`

This confirmed full system compromise.

---

## 🧠 Methodology Framework Applied


Enumeration
↓
Service identification
↓
Exploit attempt
↓
Failure analysis
↓
Strategy pivot
↓
Successful exploitation
↓
Privilege verification


---

## 🛠 Techniques Used

Primary techniques used:

- network enumeration  
- service analysis  
- exploit validation  
- manual shell access  

Key concept investigated:


Service-based exploitation and attack path prioritization


---

## 🛡 Defensive Insight

Exposed services without authentication controls represent critical vulnerabilities.

Organizations should:

- restrict unnecessary open ports  
- enforce authentication  
- implement segmentation  
- monitor exposed services  

---

## 💡 Skills Reinforced

- enumeration and analysis  
- vulnerability identification  
- exploit validation  
- adaptive attack strategy  

---

<div align="center">

🔍 Enumeration reveals attack paths  
💥 Simple misconfigurations lead to full compromise  
🔐 Security depends on reducing exposed services  

</div>
