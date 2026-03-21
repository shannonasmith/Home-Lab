<div align="center">

## 🌐 Suspicious DNS Activity  
### SOC Investigation Using Enterprise DNS Logs

![Category](https://img.shields.io/badge/Category-Log%20Analysis-blue?style=for-the-badge)
![Focus](https://img.shields.io/badge/Focus-DNS%20Investigation-green?style=for-the-badge)
![Tools](https://img.shields.io/badge/Tools-DNS%20Logs%20%7C%20CLI%20%7C%20Detection-orange?style=for-the-badge)

</div>

---

## 🧠 Scenario

During review of enterprise DNS logs, repeated query patterns and abnormal DNS activity were identified involving external clients, reverse lookup activity, internal hostnames, and repeated zone transfer failures.

This investigation approaches the dataset from a **Security Operations Center (SOC)** perspective, focusing on reconnaissance detection and infrastructure exposure.

---

## 🎯 Objective

- identify suspicious DNS query behavior  
- detect reconnaissance and enumeration patterns  
- analyze internal naming exposure  
- identify misconfigurations and attack indicators  

---

## 🖥️ Data Source

| Source | Description |
|---|---|
| dns_log_file.txt | DNS query and server log dataset |
| DNS logs | Query activity, reverse lookups, and transfer attempts |

---

## 🚨 Detection Perspective

Indicators observed:

- repeated PTR (reverse DNS) lookups  
- repeated queries from external IPs  
- failed zone transfer attempts  
- internal domain name exposure  
- abnormal query patterns  

These behaviors may indicate reconnaissance, misconfiguration, or attempted data extraction.

---

## 🔍 Investigation

### Step 1 — Identify External Query Patterns

Repeated activity observed from external IP:

- `7.204.241.161`

This host generated frequent DNS queries across multiple timestamps.

---

### Step 2 — Analyze Reverse DNS Activity

📸 Figure 1 — Reverse DNS Enumeration Activity

<div align="center">
  <img src="../images/Screenshot 2026-03-20 235427.png" width="600">
</div>

<p align="center"><em>Repeated PTR (reverse DNS) queries originating from a single external IP indicate potential reconnaissance activity. The frequency and pattern of lookups suggest automated enumeration of internal hosts.</em></p>

---

### Step 3 — Review Zone Transfer Behavior

📸 Figure 2 — DNS Zone Transfer Attempts

<div align="center">
  <img src="../images/Screenshot 2026-03-20 235808.png" width="600">
</div>

<p align="center"><em>Repeated DNS zone transfer attempts targeting the hq.bluenet domain were observed. Multiple failed connections and repeated transfer attempts indicate potential reconnaissance or misconfigured DNS synchronization behavior.</em></p>

---

### Step 4 — Identify Internal Naming Exposure

📸 Figure 3 — Internal Domain Query Exposure

<div align="center">
  <img src="../images/Screenshot 2026-03-20 235902.png" width="600">
</div>

<p align="center"><em>Queries for internal domains such as jabber.usma.bluenet and smtp.usma.bluenet reveal internal service naming conventions. This exposure increases attacker visibility into the internal network structure.</em></p>

---

## 🌐 Analysis

Observed behaviors indicate:

- external host performing repeated reverse DNS lookups  
- enumeration of internal network structure  
- repeated zone transfer attempts indicating interest in full DNS records  
- internal naming conventions exposed through query activity  

This strongly suggests **pre-attack reconnaissance activity**.

---

## ⚠️ Findings

- repeated DNS queries from a single external IP  
- high frequency of PTR lookups (enumeration behavior)  
- internal domain exposure through DNS queries  
- repeated failed zone transfer attempts  
- abnormal query patterns  

---

## 🛡️ Response Actions

### Containment
- restrict external DNS query access  
- limit exposure of internal DNS records  

### Investigation
- correlate IP activity with firewall and endpoint logs  
- identify source and intent of external querying system  

### Prevention
- disable or restrict zone transfers  
- monitor for abnormal DNS query patterns  
- implement DNS logging and alerting  
- review internal naming exposure  

---

## 📊 Key Takeaways

- DNS logs can reveal reconnaissance before exploitation  
- reverse DNS lookups are strong indicators of enumeration  
- internal naming conventions increase attack surface visibility  
- zone transfer attempts are high-risk indicators  
- early detection improves defensive response  

---

## 💡 Skills Demonstrated

- DNS log analysis  
- reconnaissance detection  
- pattern identification  
- SOC investigation methodology  
- security-focused log interpretation  

---

<div align="center">

🌐 **DNS logs reveal reconnaissance before compromise**  
🔍 **Enumeration patterns create detection opportunities**  
🛡️ **Visibility enables defense**

</div>
