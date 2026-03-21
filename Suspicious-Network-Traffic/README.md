<div align="center">

## 🌐 Suspicious Network Traffic  
### SOC Investigation Using Wireshark & PCAP Analysis

![Category](https://img.shields.io/badge/Category-Network%20Analysis-blue?style=for-the-badge)
![Focus](https://img.shields.io/badge/Focus-Traffic%20Investigation-green?style=for-the-badge)
![Tools](https://img.shields.io/badge/Tools-Wireshark%20%7C%20PCAP-orange?style=for-the-badge)

</div>

---

## 🧠 Scenario

During analysis of a packet capture (PCAP), unusual communication patterns were identified between internal and external systems.

This investigation simulates a **SOC workflow** focused on detecting and analyzing suspicious network traffic.

---

## 🎯 Objective

- identify suspicious network behavior  
- analyze packet-level communication  
- isolate potentially malicious traffic  
- determine indicators of compromise  

---

## 🚨 Detection

Initial indicators included:

- unexpected outbound connections  
- abnormal protocol usage  
- repeated communication with external IPs  
- irregular request patterns  

---

### 📊 Initial Filtering (Wireshark)

```wireshark
http
dns
tcp
```

➡️ Used to identify dominant protocols and narrow scope  

---

## 🔍 Investigation

### Step 1 — Traffic Overview

- loaded PCAP into Wireshark  
- reviewed protocol hierarchy  
- identified top endpoints  

---

### Step 2 — Identify Suspicious Hosts

Focused on:

- external IPs  
- high-frequency communication  
- unusual traffic patterns  

---

### Step 3 — Apply Targeted Filters

```wireshark
ip.addr == <suspicious_ip>
```

➡️ Isolated traffic for deeper inspection  

---

### Step 4 — Inspect Payloads

- examined packet contents  
- reviewed request/response patterns  
- searched for encoded or unusual data  

---

## 🌐 Network Analysis

Observed behavior:

- repeated outbound connections to a single host  
- consistent communication intervals  
- potential data transfer patterns  

➡️ Possible indicators of:
- command-and-control traffic  
- beaconing behavior  
- data exfiltration  

---

## ⚠️ Findings

- suspicious external communication identified  
- abnormal traffic patterns  
- indicators of compromise within packet data  

---

## 🛡️ Response Actions

### Containment
- block suspicious IP  
- isolate affected host  

### Investigation
- correlate with SIEM logs  
- review endpoint activity  

### Prevention
- implement network monitoring alerts  
- enhance traffic inspection rules  

---

## 📊 Key Takeaways

- packet analysis reveals hidden threats  
- abnormal traffic patterns indicate compromise  
- filtering is critical for investigations  
- network visibility enables detection  

---

## 💡 Skills Demonstrated

- network traffic analysis  
- Wireshark filtering  
- investigative workflow  
- anomaly detection  
- SOC methodology  

---

<div align="center">

🌐 **Network traffic reveals attacker behavior**  
🔍 **Filtering enables detection**  
🛡️ **Visibility is defense**

</div>
