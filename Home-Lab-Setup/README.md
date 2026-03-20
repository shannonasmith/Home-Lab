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

### 📦 Step 1 — Deploy the Lab Environment

The lab environment was initialized by importing prebuilt virtual machines into VMware.

Kali Linux was configured as the attacker machine, and Metasploitable2 was prepared as the vulnerable target.

Both systems were placed on a NAT network to allow communication and internet access.

📸 **Kali Linux VM in VMware**

<img src="../images/Screenshot 2026-03-19 172325.png" width="700">

---

### 🔍 Step 2 — Identify Network Connectivity Issue

While attempting to update Kali, the following error was encountered:

`sudo apt update`

`Temporary failure resolving 'http.kali.org'`

📸 **APT Update Failure**

<img src="../images/Screenshot 2026-03-19 190423.png" width="700">

This indicated a DNS resolution failure and suggested the VM was not successfully reaching the network.

---

### 🧪 Step 3 — Inspect the Network Interface

The network interface was examined to confirm whether Kali had an active connection.

`ip a`

📸 **Interface Showing No Active Carrier**

<img src="../images/Screenshot 2026-03-19 191801.png" width="700">

The interface showed **NO-CARRIER**, confirming that the system was not connected to the network.

---

### 🔄 Step 4 — Review VMware Adapter Settings

The virtual network adapter was reviewed inside VMware.

It was configured for NAT, but the connection state and adapter behavior indicated that networking was still not functioning correctly.

📸 **VMware Network Adapter Settings**

<img src="../images/Screenshot 2026-03-19 190728.png" width="700">

This suggested the problem was not simply the adapter mode, but potentially the VMware network stack itself.

---

### 🧰 Step 5 — Review VMware Networking Services

To restore VMware networking, the relevant Windows services were checked and restarted.

The key services involved were:

- VMware NAT Service  
- VMware DHCP Service  

📸 **VMware Services**

<img src="../images/Screenshot 2026-03-19 192023.png" width="700">

These services are responsible for address assignment and NAT translation for the guest machines.

---

### 🛠 Step 6 — Reset Virtual Network Configuration

The VMware Virtual Network Editor was used to restore default network settings.

📸 **Virtual Network Editor**

<img src="../images/Screenshot 2026-03-19 192358.png" width="700">

Resetting the virtual network helped restore a known-good NAT and DHCP configuration.

---

### 🔁 Step 7 — Recheck Interface State After Troubleshooting

After restarting services, restoring defaults, and reconfiguring the adapter, the interface was checked again.

`ip a`

📸 **Kali Interface Now Receiving an IP Address**

<img src="../images/Screenshot 2026-03-19 193157.png" width="700">

The system now showed a valid address on the NAT network.

Result:

`inet 192.168.74.128`

This confirmed successful communication with the DHCP server.

---

### 🧪 Step 8 — Validate Internet Connectivity

Connectivity was tested by sending ICMP requests to an external host.

`ping -c 3 8.8.8.8`

📸 **Successful Ping Test**

<img src="../images/Screenshot 2026-03-19 193252.png" width="700">

The system successfully reached an external address, confirming that the network issue had been resolved.

---

### 🔄 Step 9 — Update the Kali System

With connectivity restored, the Kali system was updated.

`sudo apt update && sudo apt full-upgrade -y`

`sudo apt autoremove -y`

`reboot`

This ensured the attacker machine was fully updated before continuing with the lab.

---

### 📦 Step 10 — Import and Boot the Target Machine

Metasploitable2 was imported into VMware and powered on as the vulnerable target.

📸 **Metasploitable2 Booted and Ready**

<img src="../images/Screenshot 2026-03-19 200537.png" width="700">

After boot, the system was accessed using the default credentials.

📸 **Metasploitable2 Login Complete**

<img src="../images/Screenshot 2026-03-19 200810.png" width="700">

---

### 🔍 Step 11 — Verify Target Network Assignment

The target machine’s interface configuration was checked to confirm that it was on the same NAT network as Kali.

`ip a`

📸 **Metasploitable2 IP Address**

<img src="../images/Screenshot 2026-03-19 201134.png" width="700">

Result:

`192.168.74.129`

From Kali, this confirmed that both machines were now positioned for enumeration and exploitation.

---

### 🧩 Step 12 — Note on VMware Tools

An attempt to use VMware Tools on the legacy Linux target generated a compatibility warning.

📸 **VMware Tools Warning**

<img src="../images/Screenshot 2026-03-19 201000.png" width="700">

This did not affect the lab objective, since VMware Tools were not required for scanning or exploitation.

---

## 🧠 Methodology Framework Applied

```
Environment setup
      ↓
Failure identification
      ↓
Interface inspection
      ↓
Adapter analysis
      ↓
Service troubleshooting
      ↓
Network reset
      ↓
Connectivity validation
      ↓
Target onboarding
```

---

## 🛠 Techniques Used

Primary techniques used:

- virtual network troubleshooting  
- DHCP validation  
- interface inspection  
- VMware service management  
- NAT configuration review  

Key concept investigated:

```
Virtual network configuration and troubleshooting
```

---

## 🛡 Defensive Insight

Misconfigured infrastructure can prevent systems from functioning before security testing even begins.

Understanding virtual networking fundamentals is critical in both offensive and defensive cybersecurity roles.

Reliable lab setup depends on validating connectivity, IP assignment, and service behavior before moving into exploitation.

---

## 💡 Skills Reinforced

- virtualization troubleshooting  
- network diagnostics  
- system configuration validation  
- structured problem-solving  
- lab environment preparation  

---

<div align="center">

🧱 Strong labs start with stable infrastructure  
🔧 Troubleshooting is a core cybersecurity skill  
🌐 Networking fundamentals enable everything  

</div>
