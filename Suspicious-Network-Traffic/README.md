<div align="center">

## 🌐 Suspicious Network Traffic  
### SOC Investigation Using Wireshark & PCAP Analysis

![Category](https://img.shields.io/badge/Category-Network%20Analysis-blue?style=for-the-badge)
![Focus](https://img.shields.io/badge/Focus-Traffic%20Investigation-green?style=for-the-badge)
![Tools](https://img.shields.io/badge/Tools-Wireshark%20%7C%20PCAP-orange?style=for-the-badge)

</div>

---

## 🧠 Scenario

During analysis of a captured network traffic file (PCAP), unusual communication patterns were identified between internal and external systems.

This investigation simulates a **Security Operations Center (SOC)** workflow focused on detecting and analyzing suspicious network activity using packet inspection techniques.

---

## 🎯 Objective

- identify suspicious network behavior  
- analyze packet-level communication  
- isolate potentially malicious traffic  
- determine indicators of compromise  

---

## 🚨 Detection

Initial indicators of suspicious activity included:

- unexpected outbound connections  
- abnormal protocol usage  
- repeated communication with external IP addresses  
- irregular request patterns  

---

### 📊 Initial Filtering (Wireshark)

```wireshark
http
dns
tcp

➡️ Used to identify dominant protocols and narrow investigation scope

🔍 Investigation
Step 1 — Review Traffic Overview
loaded PCAP into Wireshark
reviewed protocol hierarchy
identified top talkers and endpoints
Step 2 — Identify Suspicious Endpoints

Focused on:

external IP addresses
high-frequency communication patterns
non-standard traffic behavior
Step 3 — Apply Targeted Filters
ip.addr == <suspicious_ip>

➡️ Isolated traffic associated with a specific endpoint

Step 4 — Inspect Packet Contents
examined payload data
reviewed request/response patterns
searched for encoded or unusual strings
🌐 Network Analysis

Observed behavior included:

repeated outbound connections to a single host
consistent communication intervals
potential data transfer patterns within packets

These characteristics may indicate:

command-and-control communication
automated beaconing behavior
possible data exfiltration
⚠️ Findings
suspicious external communication identified
abnormal traffic patterns inconsistent with baseline behavior
potential indicators of compromise within packet data
🛡️ Response Actions
Containment
block suspicious IP address
isolate affected system
Investigation
correlate findings with SIEM logs
review authentication and endpoint activity
Prevention
implement network monitoring alerts
enhance traffic inspection rules
📊 Key Takeaways
packet-level analysis reveals hidden attack behavior
identifying abnormal traffic patterns is critical
filtering techniques are essential for efficient investigation
network visibility supports early detection
💡 Skills Demonstrated
network traffic analysis
Wireshark filtering and inspection
investigative methodology
detection of anomalous behavior
SOC workflow execution
<div align="center">

🌐 Network traffic reveals attacker behavior
🔍 Filtering and analysis drive detection
🛡️ Visibility enables effective defense

</div> ```
