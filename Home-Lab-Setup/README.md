🧠 Home Lab Setup
VMware Network Troubleshooting & Kali Environment Configuration






🎯 Objective

Build a functional cybersecurity lab using VMware and resolve networking issues preventing system updates and connectivity.

🖥 Environment
Component	Details
Hypervisor	VMware Workstation
Attacker	Kali Linux
Target	Metasploitable2
Network	NAT
📦 Step 1 — Lab Deployment

Virtual machines were imported into VMware.

📸 VMware Lab Environment



🔍 Step 2 — Network Failure

Kali update failed with:

Temporary failure resolving 'http.kali.org'

📸 APT Failure



🧪 Step 3 — Interface Analysis
ip a

📸 No Carrier / Interface Down



🔄 Step 4 — VMware Adapter Issue

The adapter was:

Set to NAT

Not properly connected

“Connected” option unavailable

📸 Adapter Configuration



🧰 Step 5 — Service Troubleshooting

Restarted:

VMware NAT Service

VMware DHCP Service

📸 VMware Services



🛠 Step 6 — Network Reset

Used Virtual Network Editor → Restore Defaults

📸 VMnet Configuration



🔁 Step 7 — Adapter Rebuild

Removed network adapter

Re-added NAT adapter

✅ Step 8 — Connectivity Restored
ip a

📸 IP Assigned



🧪 Step 9 — Verification
ping -c 3 8.8.8.8

📸 Ping Success



🧠 Methodology
Deployment → Failure → Analysis → Services → Reset → Rebuild → Validation
🛠 Techniques Used

Virtual networking troubleshooting

DHCP validation

Service management

Interface debugging

🛡 Key Insight

Virtual networking issues can completely block system functionality.
Understanding infrastructure is essential before security testing.

🧱 Strong labs start with stable infrastructure
🔧 Debugging is a core cybersecurity skill
