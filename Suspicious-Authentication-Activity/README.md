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

This project simulates a **Security Operations Center (SOC)** investigation using Splunk to analyze authentication logs and identify suspicious behavior.

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
| linux_s_30DAY.log | Linux authentication and system activity logs |
| Splunk SIEM | Log ingestion, search, and analysis platform |

---

## 🚨 Detection

Initial indicators of suspicious activity included:

- multiple failed login attempts  
- repeated authentication attempts from the same source  
- unusual login times  
- activity from unfamiliar hosts  

---

### 📊 Detection Query (Failed Logins)

```spl
index=main sourcetype=linux_secure "Failed password"
| stats count by user, src_ip
| sort -count

➡️ Identifies accounts with repeated failed login attempts

📊 Detection Query (Successful Logins)
index=main sourcetype=linux_secure "Accepted password"
| stats count by user, src_ip

➡️ Highlights successful authentication patterns

🔍 Investigation
Step 1 — Identify Targeted Accounts
reviewed users with high failed login counts
identified accounts potentially targeted by brute force attempts
Step 2 — Correlate Successful Logins
checked if failed attempts were followed by successful logins
identified potential account compromise scenarios
Step 3 — Analyze Source IP Activity
index=main sourcetype=linux_secure
| stats count by src_ip
| sort -count

➡️ Identifies top source IPs generating authentication activity

Step 4 — Review Login Timing
analyzed timestamps of login attempts
identified unusual access times (off-hours activity)
🌐 Analysis

Observed patterns included:

repeated login attempts targeting specific users
multiple authentication attempts from single IP addresses
sequences of failed logins followed by success

These behaviors may indicate:

brute-force attacks
credential stuffing
compromised accounts
⚠️ Findings
suspicious authentication patterns identified
evidence of repeated login attempts
potential unauthorized access activity
abnormal user behavior detected
🛡️ Response Actions
Containment
lock affected user accounts
block suspicious IP addresses
Investigation
review additional logs (network, endpoint)
correlate with other security alerts
Prevention
enforce strong password policies
implement account lockout thresholds
enable multi-factor authentication
📊 Key Takeaways
authentication logs provide critical detection signals
repeated login attempts are strong indicators of attack activity
correlation of failed and successful logins is essential
SIEM tools enable efficient investigation and visibility
💡 Skills Demonstrated
Splunk SIEM usage
log analysis and correlation
authentication investigation
detection query development (SPL)
SOC investigation workflow
<div align="center">

🔐 Authentication logs reveal attacker intent
📊 Correlation turns data into insight
🛡️ Detection enables response

</div> ```
