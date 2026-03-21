<div align="center">

## 🌐 Suspicious DNS Activity  
### SOC Investigation Using Enterprise DNS Logs

![Category](https://img.shields.io/badge/Category-Log%20Analysis-blue?style=for-the-badge)
![Focus](https://img.shields.io/badge/Focus-DNS%20Investigation-green?style=for-the-badge)
![Tools](https://img.shields.io/badge/Tools-DNS%20Logs%20%7C%20CLI%20%7C%20Detection-orange?style=for-the-badge)

</div>

---

## 🧠 Scenario

During review of enterprise DNS logs, repeated query patterns and abnormal DNS activity were identified involving external clients, internal hostnames, reverse lookup requests, and repeated zone transfer failures.

This project approaches the dataset as a **SOC investigation**, focusing on how DNS logs can reveal reconnaissance, naming leakage, misconfiguration, and potential pre-attack behavior. The analysis is based on the uploaded DNS log dataset. :contentReference[oaicite:0]{index=0}

---

## 🎯 Objective

- identify suspicious DNS query behavior  
- detect signs of reconnaissance and enumeration  
- analyze repeated client activity and query patterns  
- determine defensive actions to reduce exposure  

---

## 🖥️ Data Source

| Source | Description |
|---|---|
| `dns_log_file.txt` | DNS server query and service log data |
| DNS server logs | Query activity, warnings, zone transfer status, and resolver behavior |

---

## 🚨 Detection Perspective

The log data contains several behaviors that are useful from a detection standpoint:

- repeated PTR lookups from the same external client  
- repeated queries for internal services and hostnames  
- failed zone transfer attempts  
- malformed or unusual domain lookups  
- high-frequency repeated `A` record requests  

These behaviors may indicate:

- DNS reconnaissance  
- infrastructure enumeration  
- attempted zone transfer abuse  
- automated querying or scripted discovery  
- internal misconfiguration worth investigating  

---

### 📊 Example Detection Logic (CLI)

```bash
grep "query:" dns_log_file.txt | awk '{print $7}' | sort | uniq -c | sort -nr | head
```

➡️ Identifies the most active querying clients

```bash
grep "in-addr.arpa" dns_log_file.txt | sort | uniq -c | sort -nr | head
```

➡️ Highlights repeated reverse DNS lookups associated with enumeration

```bash
grep "Transfer started\|failed to connect\|zone transfer" dns_log_file.txt
```

➡️ Surfaces potential zone transfer issues and transfer failures

---

## 🔍 Investigation

### Step 1 — Identify Repeated External Client Activity

The dataset shows repeated DNS activity from the same external address, especially:

- `7.204.241.161`
- `31.154.241.4`
- `31.154.241.11`

These clients repeatedly query internal resources and reverse lookup records, which may indicate automated enumeration or scripted reconnaissance. :contentReference[oaicite:1]{index=1}

---

### Step 2 — Review Reverse Lookup Behavior

Repeated PTR queries appear throughout the log, including lookups such as:

- `181.190.75.3.in-addr.arpa`
- `203.60.1.10.in-addr.arpa`
- `253.60.1.10.in-addr.arpa`
- `20.10.1.10.in-addr.arpa`

High-frequency reverse lookups can be consistent with host discovery and infrastructure mapping behavior. :contentReference[oaicite:2]{index=2}

---

### Step 3 — Identify Internal Naming Exposure

The logs reveal repeated queries for internal services, including:

- `jabber.usma.bluenet`
- `smtp.usma.bluenet`
- `ns1.usma.bluenet`
- `www.usma.bluenet`
- `www1.hq.bluenet`

This exposes internal naming conventions and service roles that could support follow-on targeting. :contentReference[oaicite:3]{index=3}

---

### Step 4 — Review Zone Transfer Failures

The dataset includes repeated zone transfer events and errors such as:

- `zone hq.bluenet/IN: Transfer started`
- `transfer of 'hq.bluenet/IN' from 10.1.10.5#53: failed to connect: connection refused`
- `refresh: skipping zone transfer as master 10.1.10.5#53 ... is unreachable`

These events suggest repeated transfer attempts combined with connection failures, creating both security and resilience concerns. :contentReference[oaicite:4]{index=4}

---

### Step 5 — Investigate Abnormal Query Patterns

The logs include unusual queries such as:

- `en-us.fxfeeds.mozilla.com.usma.bluenet`
- `quickdraw.splunk.com.usma.bluenet`
- `www1.hq.bluenet.usma.bluenet`
- `hq.blunet`

These patterns may indicate:

- search path leakage  
- malformed resolution attempts  
- typo-driven lookups  
- application or client misconfiguration  

They are also useful signals for detection tuning. :contentReference[oaicite:5]{index=5}

---

## 🌐 Analysis

Observed patterns suggest a mix of suspicious and operationally significant activity:

- repeated external reverse DNS queries indicate likely reconnaissance behavior  
- internal service hostnames are exposed through query activity  
- repeated failed zone transfer activity suggests attempted synchronization or transfer misuse  
- malformed appended domains suggest resolver search path or client-side issues  
- repeated query bursts for the same internal hosts may indicate automation or unstable clients  

From a SOC perspective, the most significant concern is the repeated DNS activity from external clients combined with internal naming visibility and repeated reverse lookups. :contentReference[oaicite:6]{index=6}

---

## ⚠️ Findings

- repeated external client activity observed against internal DNS resources  
- frequent PTR lookups consistent with enumeration behavior  
- internal service names exposed through query patterns  
- repeated zone transfer failures identified  
- malformed or appended-domain requests indicate possible resolver misconfiguration  
- repeated `A` record lookups suggest scripted or automated behavior  

---

## 🛡️ Response Actions

### Containment
- restrict DNS access from unauthorized external clients  
- review and limit exposure of internal DNS records  
- verify zone transfer permissions and source restrictions  

### Investigation
- correlate active client IPs with firewall, proxy, and host logs  
- determine whether repeated PTR lookups align with known admin systems or unauthorized sources  
- investigate repeated zone transfer attempts and transfer failures  

### Prevention
- disable or strictly restrict zone transfers  
- monitor for high-volume PTR lookups and repeated DNS failures  
- create alerts for unusual query bursts and malformed internal domain lookups  
- review resolver search path settings and DNS client configurations  

---

## 📊 Key Takeaways

- DNS logs can reveal reconnaissance before direct exploitation occurs  
- reverse lookups are valuable indicators of infrastructure enumeration  
- internal hostname exposure increases attacker knowledge of the environment  
- repeated zone transfer failures are both operational and security-relevant  
- DNS anomalies provide strong early-warning signals for SOC monitoring  

---

## 💡 Skills Demonstrated

- DNS log analysis  
- pattern recognition across large log datasets  
- identification of reconnaissance behavior  
- detection-oriented investigation methodology  
- infrastructure exposure assessment  
- SOC-style triage and response thinking  

---

<div align="center">

🌐 **DNS logs often reveal reconnaissance before compromise**  
🔍 **Enumeration patterns create early detection opportunities**  
🛡️ **Visibility into naming, queries, and transfer behavior strengthens defense**

</div>
