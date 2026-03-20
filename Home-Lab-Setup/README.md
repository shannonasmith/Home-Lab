<div align="center">

# 🧠 Home Lab Setup  
## VMware Networking & Kali Linux Environment Configuration

![Category](https://img.shields.io/badge/Category-Lab%20Setup-purple?style=for-the-badge)
![Focus](https://img.shields.io/badge/Focus-Network%20Troubleshooting-blue?style=for-the-badge)
![Method](https://img.shields.io/badge/Method-Virtualization%20Debugging-success?style=for-the-badge)

</div>

---

### 🎯 Objective

Set up a functional cybersecurity home lab using VMware with Kali Linux and a vulnerable target machine.

During setup, the Kali system was unable to reach external repositories, preventing updates and indicating a network misconfiguration.

The goal was to diagnose and resolve the networking issue to establish a stable environment for future security testing.

This challenge focused on **virtual networking, troubleshooting methodology, and system validation**.

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

The setup began by importing prebuilt virtual machines into VMware.

Kali Linux was configured as the primary attacker system, while Metasploitable2 was added as a vulnerable target for testing.

Both systems were connected using a NAT network to allow internal communication and internet access.

---

### 🔍 Step 2 — Identify Network Connectivity Issue

While attempting to update Kali Linux, the following error was encountered:


sudo apt update

Temporary failure resolving 'http.kali.org'


📸 **APT Update Failure**

<img src="../images/kali_update_error.png" width="700">

This indicated that the system was unable to resolve domain names, suggesting a DNS or network connectivity issue.

---

### 🧪 Step 3 — Inspect Network Interface

To investigate further, the network interface configuration was examined:


ip a


📸 **Interface Showing NO-CARRIER**

<img src="../images/kali_no_carrier.png" width="700">

The interface displayed **NO-CARRIER**, indicating that no active network connection was established.

---

### 🔄 Step 4 — Analyze VMware Adapter Configuration

The virtual network adapter was reviewed within VMware settings.

It was configured to use NAT, which should allow the VM to share the host’s internet connection.

📸 **Network Adapter Configuration**

<img src="../images/vmware_adapter_settings.png" width="700">

This suggested that the issue was not with the adapter mode itself, but potentially with underlying VMware services or network configuration.

---

### 🧰 Step 5 — Restart VMware Networking Services

To restore functionality, VMware networking services were restarted:

- VMware NAT Service  
- VMware DHCP Service  

📸 **VMware Services**

<img src="../images/vmware_services.png" width="500">

Restarting these services can resolve issues related to IP assignment and network translation.

---

### 🛠 Step 6 — Reset Virtual Network Configuration

The VMware Virtual Network Editor was used to restore default network settings.

📸 **Virtual Network Editor**

<img src="../images/vmnet_editor.png" width="700">

This reset NAT and DHCP configurations to a known working state.

---

### 🔁 Step 7 — Reconfigure Network Adapter

The network adapter was removed and re-added to ensure proper attachment to the NAT network.

This step helps resolve hidden configuration inconsistencies.

---

### 🔄 Step 8 — Verify IP Address Assignment

After reconfiguration, the network interface was checked again:


ip a


📸 **IP Address Assigned**

<img src="../images/kali_ip_success.png" width="700">

A valid IP address was now assigned, confirming successful communication with the DHCP server.

---

### 🧪 Step 9 — Validate Network Connectivity

Connectivity was tested using ICMP requests:


ping -c 3 8.8.8.8


📸 **Successful Ping**

<img src="../images/ping_success.png" width="700">

The system successfully reached an external host, confirming network functionality.

---

### 🔄 Step 10 — Update System

With connectivity restored, the system was updated:


sudo apt update && sudo apt full-upgrade -y


This confirmed that the networking issue had been fully resolved.

---

## 🧠 Methodology Framework Applied


Environment setup
↓
Failure identification
↓
Interface inspection
↓
Configuration analysis
↓
Service troubleshooting
↓
Network reset
↓
Validation testing


---

## 🛠 Techniques Used

Primary techniques used:

- virtual network troubleshooting  
- DHCP validation  
- interface inspection  
- VMware service management  

Key concept investigated:


Virtual network configuration and troubleshooting


---

## 🛡 Defensive Insight

Misconfigured infrastructure can prevent systems from functioning correctly before any security testing begins.

Understanding networking fundamentals is critical in both offensive and defensive cybersecurity roles.

Proper configuration and validation are essential to ensure system reliability.

---

## 💡 Skills Reinforced

- virtualization troubleshooting  
- network diagnostics  
- system configuration validation  
- structured problem-solving  

---

<div align="center">

🧱 Strong labs start with stable infrastructure  
🔧 Troubleshooting is a core cybersecurity skill  
🌐 Networking fundamentals enable everything  

</div>
