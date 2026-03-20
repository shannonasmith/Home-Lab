<div align="center">

# 🧠 Home Lab Setup  
## VMware Networking & Kali Configuration Troubleshooting

![Category](https://img.shields.io/badge/Category-Lab%20Setup-purple?style=for-the-badge)
![Focus](https://img.shields.io/badge/Focus-Network%20Troubleshooting-blue?style=for-the-badge)
![Method](https://img.shields.io/badge/Method-Virtualization-success?style=for-the-badge)

</div>

---

### 🎯 Objective

Set up a functional cybersecurity lab environment using VMware and resolve network connectivity issues preventing system updates.

The goal was to ensure:
- stable virtual networking  
- proper IP assignment  
- internet connectivity for Kali  

---

### 🖥 Environment

| Component | Purpose |
|----------|--------|
| VMware Workstation | Virtualization platform |
| Kali Linux | Attacker machine |
| Metasploitable2 | Vulnerable target |
| NAT Network | VM communication |

---

### 📦 Step 1 — Initial Lab Deployment

Virtual machines were imported and configured in VMware.

📸 **VMware Lab Environment**

<img src="../images/vmware_lab_overview.png" width="700">

---

### 🔍 Step 2 — Identify Network Failure

Kali update failed with:

```bash
Temporary failure resolving 'http.kali.org'

📸 APT Update Failure

<img src="../images/kali_update_error.png" width="700">
🧪 Step 3 — Inspect Network Interface
ip a

📸 Interface Showing NO-CARRIER

<img src="../images/kali_no_carrier.png" width="700">
🔄 Step 4 — Review VMware Adapter Settings

The adapter was configured as NAT but not properly connected.

📸 Network Adapter Configuration

<img src="../images/vmware_adapter_settings.png" width="700">
🧰 Step 5 — Restart VMware Services

Restarted:

VMware NAT Service

VMware DHCP Service

📸 VMware Services

<img src="../images/vmware_services.png" width="500">
🛠 Step 6 — Reset Virtual Network

Used Virtual Network Editor → Restore Defaults

📸 Virtual Network Editor

<img src="../images/vmnet_editor.png" width="700">
🔁 Step 7 — Rebuild Network Adapter

Removed existing adapter

Re-added NAT adapter

✅ Step 8 — Confirm Connectivity
ip a

📸 IP Address Assigned

<img src="../images/kali_ip_success.png" width="700">
🧪 Step 9 — Verify Internet Access
ping -c 3 8.8.8.8

📸 Successful Ping

<img src="../images/ping_success.png" width="700">
🔄 Step 10 — Update System
sudo apt update && sudo apt full-upgrade -y
🧠 Methodology Framework Applied
Deployment
   ↓
Failure identification
   ↓
Interface inspection
   ↓
Service troubleshooting
   ↓
Network reset
   ↓
Adapter rebuild
   ↓
Connectivity validation
🛠 Techniques Used

virtual network troubleshooting

DHCP validation

interface inspection

VMware service management

🛡 Defensive Insight

Misconfigured virtual networking can completely prevent system functionality.

Understanding infrastructure is critical before performing security testing.

💡 Skills Reinforced

virtualization troubleshooting

network debugging

system configuration

problem-solving methodology

<div align="center">

🧱 Strong labs start with stable infrastructure
🔧 Debugging is a core cybersecurity skill

</div> ```
