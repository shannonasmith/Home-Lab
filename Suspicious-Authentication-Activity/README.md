<div align="center">

## 🔐 Suspicious Authentication Activity  
### SOC Investigation Using Splunk SIEM

![Category](https://img.shields.io/badge/Category-SIEM%20Investigation-red?style=for-the-badge)
![Focus](https://img.shields.io/badge/Focus-Authentication%20Analysis-blue?style=for-the-badge)
![Tools](https://img.shields.io/badge/Tools-Splunk%20%7C%20Linux%20Logs-green?style=for-the-badge)

</div>

---

## 🧠 Scenario

During routine monitoring, unusual authentication activity was identified within Linux system logs ingested into Splunk.

The activity included repeated login attempts, irregular access patterns, and potential indicators of unauthorized access.

This project simulates a **SOC investigation** using Splunk to analyze authentication logs.

---

## 🎯 Objective

- analyze authentication activity in Linux logs  
- detect suspicious login patterns  
- identify potential unauthorized access  
- investigate user and host behavior  

---

## 🖥️ Data Source

| Source | Description |
|---|---|
| linux_s_30DAY.log | Linux authentication logs |
| Splunk SIEM | Log analysis platform |

---

## 🚨 Detection

Indicators observed:

- multiple failed login attempts  
- repeated authentication attempts from same IP  
- unusual login timing  
- unfamiliar source hosts  

---

### 📊 Detection — Failed Logins

```spl
index=main sourcetype=linux_secure "Failed password"
| stats count by user, src_ip
| sort -count
```

➡️ Identifies brute-force style activity  

---

<div align="center">
  <img src="images/image.png" width="600">
</div>

<p align="center"><em>Figure 1. Failed login activity showing repeated authentication attempts across users and source IPs.</em></p>

---

### 📊 Detection — Successful Logins

```spl
index=main sourcetype=linux_secure "Accepted password"
| stats count by user, src_ip
```

➡️ Shows successful authentication patterns  

---

<div align="center">
  <img src="images/image 1.png" width="600">
</div>

<p align="center"><em>Figure 2. Successful authentication events used to correlate potential compromise after failed attempts.</em></p>

---

## 🔍 Investigation

### Step 1 — Identify Targeted Accounts

- users with high failed login counts  
- accounts under repeated attack  

---

### Step 2 — Correlate Success After Failures

- identify successful logins after failed attempts  
- detect possible compromise  

---

### Step 3 — Analyze Source IP Activity

```spl
index=main sourcetype=linux_secure
| stats count by src_ip
| sort -count
```

➡️ Identifies top attacking sources  

---

<div align="center">
  <img src="images/image 2.png" width="600">
</div>

<p align="center"><em>Figure 3. Source IP activity highlighting repeated login attempts from specific hosts.</em></p>

---

### Step 4 — Analyze Login Timing

- review timestamps  
- identify off-hours activity  

---

## 🌐 Analysis

Observed patterns:

- repeated login attempts  
- multiple attempts from single IP  
- failures followed by success  

➡️ Possible indicators:

- brute-force attack  
- credential stuffing  
- compromised account  

---

## ⚠️ Findings

- suspicious login behavior identified  
- repeated authentication attempts detected  
- abnormal access patterns observed  

---

## 🛡️ Response Actions

### Containment
- lock affected accounts  
- block suspicious IPs  

### Investigation
- review endpoint + network logs  
- correlate with other alerts  

### Prevention
- enforce strong passwords  
- enable account lockout policies  
- implement MFA  

---

## 📊 Key Takeaways

- authentication logs are critical detection sources  
- failed login spikes indicate attack attempts  
- correlation is key to identifying compromise  
- SIEM enables efficient investigation  

---

## 💡 Skills Demonstrated

- Splunk SIEM usage  
- log analysis and correlation  
- authentication investigation  
- SPL query development  
- SOC workflow execution  

---

<div align="center">

🔐 **Authentication logs reveal attacker behavior**  
📊 **Correlation turns logs into insight**  
🛡️ **Detection enables response**

</div>
