<div align="center">

# 🧠 Home Lab Setup  
## VMware Networking & Kali Linux Environment Configuration

![Category](https://img.shields.io/badge/Category-Lab%20Setup-purple?style=for-the-badge)
![Focus](https://img.shields.io/badge/Focus-Network%20Troubleshooting-blue?style=for-the-badge)
![Method](https://img.shields.io/badge/Method-Virtualization%20Debugging-success?style=for-the-badge)

</div>

---

### 🎯 Objective

Build a functional cybersecurity home lab using Kali Linux and Metasploitable2 within VMware.

During setup, Kali Linux was unable to reach external repositories, preventing updates and indicating a network misconfiguration.

The goal was to diagnose and resolve the issue to establish a stable lab environment for future security testing.

This challenge focused on **virtual networking, troubleshooting methodology, and environment validation**.

---

### 🖥 Environment

| Tool | Purpose |
|-----|------|
| VMware Workstation | Virtualization platform |
| Kali Linux | Attacker machine |
| Metasploitable2 | Vulnerable target |
| NAT networking | Internal VM communication |

---

### 📦 Step 1 — Deploy Virtual Machines

The lab environment was initialized by importing prebuilt virtual machines into VMware.

Kali Linux was configured as the attacker machine, and Metasploitable2 was prepared as the vulnerable target.

<img src="../images/Screenshot 2026-03-19 172119.png" width="700">

---

### 🔍 Step 2 — Identify Network Connectivity Issue

While attempting to update Kali, the following error was encountered:

`sudo apt update`

`Temporary failure resolving 'http.kali.org'`

<img src="../images/Screenshot 2026-03-19 190423.png" width="700">

---

### 🧪 Step 3 — Inspect Network Interface

`ip a`

<img src="../images/Screenshot 2026-03-19 200537.png" width="700">

The interface showed no active connection.

---

### 🧰 Step 4 — Troubleshoot VMware Networking

- Verified adapter settings  
- Checked “connected” status (grayed out issue)  

<img src="../images/Screenshot 2026-03-19 172224.png" width="700">
<img src="../images/Screenshot 2026-03-19 172325.png" width="700">

---

### 🔄 Step 5 — Reset Virtual Network Configuration

Used Virtual Network Editor and restored defaults.

<img src="../images/Screenshot 2026-03-19 191801.png" width="700">
<img src="../images/Screenshot 2026-03-19 192023.png" width="700">

---

### 🔁 Step 6 — Restart VMware Services

Restarted:

- VMware NAT Service  
- VMware DHCP Service  

<img src="../images/Screenshot 2026-03-19 192358.png" width="700">

---

### 🔄 Step 7 — Verify IP Assignment

`ip a`

<img src="../images/Screenshot 2026-03-19 201134.png" width="700">

Result:

`192.168.74.128`

---

### 🧪 Step 8 — Validate Connectivity

`ping -c 3 8.8.8.8`

<img src="../images/Screenshot 2026-03-19 201834.png" width="700">

---

### 🔄 Step 9 — Update System

`sudo apt update && sudo apt full-upgrade -y`

<img src="../images/Screenshot 2026-03-19 202118.png" width="700">

---

### 📦 Step 10 — Verify Final State

System fully operational after troubleshooting.

<img src="../images/Screenshot 2026-03-19 202309.png" width="700">
<img src="../images/Screenshot 2026-03-19 202350.png" width="700">

---

## 🧠 Methodology Framework Applied


Environment setup
↓
Failure identification
↓
Troubleshooting
↓
Network reset
↓
Validation


---

## 💡 Skills Reinforced

- virtualization troubleshooting  
- network diagnostics  
- system configuration  

---

<div align="center">

🧱 Strong labs start with stable infrastructure  

</div>
