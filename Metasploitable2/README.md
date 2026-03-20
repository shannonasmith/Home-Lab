<div align="center">

# 🧠 Metasploitable2  
## Enumeration & Root Exploitation via Exposed Bindshell

![Category](https://img.shields.io/badge/Category-Network%20Exploitation-red?style=for-the-badge)
![Focus](https://img.shields.io/badge/Focus-Service%20Enumeration-blue?style=for-the-badge)
![Method](https://img.shields.io/badge/Method-Manual%20Exploitation-success?style=for-the-badge)

</div>

---

### 🎯 Objective

Perform enumeration on a vulnerable Linux system, identify exposed services, and determine a viable path to gain root-level access.

The target contained multiple known weaknesses, requiring analysis to determine which attack path was the most effective.

The goal was to simulate a realistic penetration testing workflow by scanning the system, evaluating attack options, and exploiting the simplest working path.

This challenge focused on **service enumeration, exploit validation, and manual exploitation techniques**.

---

### 🖥 Environment

| Tool | Purpose |
|-----|------|
| Kali Linux | Attacker machine |
| Metasploitable2 | Vulnerable target |
| Nmap | Service enumeration |
| Metasploit | Exploit research and validation |
| Netcat | Manual exploitation |

---

### 📦 Step 1 — Perform Initial Enumeration

The target system was scanned to identify open ports and running services.

`nmap -sC -sV 192.168.74.129`

The results revealed a broad attack surface, including FTP, SMB, Telnet, Apache, Tomcat, and a bindshell service on port 1524.

Among the most important findings were:

- `21/tcp` — vsftpd 2.3.4  
- `22/tcp` — SSH  
- `23/tcp` — Telnet  
- `80/tcp` — Apache  
- `445/tcp` — Samba  
- `1524/tcp` — Bindshell  
- `3306/tcp` — MySQL  
- `8180/tcp` — Tomcat  

---

### 🔍 Step 2 — Evaluate Attack Paths

The enumeration results suggested several possible ways forward.

The FTP service running vsftpd 2.3.4 appeared attractive because it is widely associated with a known backdoor vulnerability.

At the same time, port `1524` stood out because it exposed a bindshell, which may provide direct command execution without authentication.

This created two potential attack paths:

- attempt the known vsftpd route first  
- pivot to the bindshell if a direct shell was available  

---

### 🧪 Step 3 — Launch Metasploit and Investigate the FTP Path

Metasploit was opened to test the vsftpd 2.3.4 exploit path.

📸 **Metasploit Console Started**

<img src="../images/Screenshot 2026-03-19 201834.png" width="700">

The vsftpd module was identified and configured against the target.

📸 **vsftpd Module Selected**

<img src="../images/Screenshot 2026-03-19 202118.png" width="700">

However, the attempt ran into payload validation issues involving `LHOST`.

---

#### 🔎 Analytical Observation

This was an important reminder that not every known exploit path will work cleanly in practice.

Even when a service version looks promising, tooling, payload selection, or service behavior can complicate the process.

Attackers need to validate findings and adapt their approach when the initial path is not reliable.

---

### 🔄 Step 4 — Attempt to Correct the vsftpd Exploit Path

Additional Metasploit adjustments were attempted to resolve the payload issue.

📸 **Payload Adjustment Attempt**

<img src="../images/Screenshot 2026-03-19 202309.png" width="700">

A follow-up attempt still resulted in the framework defaulting back to an `LHOST`-dependent payload.

📸 **Metasploit Still Requiring LHOST**

<img src="../images/Screenshot 2026-03-19 202350.png" width="700">

At this point, the FTP route was proving less efficient than expected.

---

### 🧪 Step 5 — Test the vsftpd Backdoor Manually

Rather than continue forcing Metasploit, the suspected backdoor port was tested directly.

`nc 192.168.74.129 6200`

📸 **Backdoor Connection Refused**

<img src="../images/Screenshot 2026-03-19 202641.png" width="700">

The connection was refused, confirming that this path was not viable in the current scenario.

---

#### 🔎 Analytical Observation

This reinforced an important lesson in exploitation work:

Not all discovered vulnerabilities are practically exploitable, and not all promising paths are worth pursuing once they stop being efficient.

A good workflow depends on pivoting quickly when a better route is available.

---

### 🔄 Step 6 — Pivot to the Bindshell

With the FTP path ruled out, focus shifted to the bindshell exposed on port `1524`.

Because a bindshell listens for incoming connections, it can provide direct command execution if exposed and reachable.

This made it the most straightforward attack path available.

---

### 💥 Step 7 — Exploit the Bindshell

A direct connection was established with Netcat.

`nc 192.168.74.129 1524`

📸 **Shell Access via Port 1524**

<img src="../images/Screenshot 2026-03-19 202800.png" width="700">

A shell was obtained immediately after connecting.

---

### 🔐 Step 8 — Confirm Privilege Level

To verify the level of access, the following command was executed:

`whoami`

📸 **Privilege Confirmation**

<img src="../images/Screenshot 2026-03-19 202821.png" width="700">

Output:

`root`

This confirmed full system compromise and demonstrated that the bindshell provided unauthenticated root-level access.

---

## 🧠 Methodology Framework Applied

```
Enumeration
      ↓
Service analysis
      ↓
Exploit path selection
      ↓
Metasploit validation
      ↓
Manual exploit testing
      ↓
Attack path pivot
      ↓
Bindshell exploitation
      ↓
Privilege verification
```

---

## 🛠 Techniques Used

Primary techniques used:

- network enumeration  
- service analysis  
- exploit validation  
- manual shell access  
- attack path prioritization  

Key concept investigated:

```
Service-based exploitation and attack path prioritization
```

---

## 🛡 Defensive Insight

Exposed services without authentication controls represent critical vulnerabilities.

The bindshell on port `1524` provided direct root-level access and demonstrated how a simple misconfiguration can lead to total compromise.

To reduce this type of risk, organizations should:

- disable unnecessary services  
- restrict exposed ports  
- enforce authentication controls  
- implement segmentation and monitoring  
- continuously review external and internal attack surfaces  

---

## 💡 Skills Reinforced

- network enumeration and analysis  
- exploit troubleshooting  
- manual validation of attack paths  
- adaptive exploitation strategy  
- privilege verification  

---

<div align="center">

🔍 Enumeration reveals the attack surface  
💥 Simpler paths often lead to compromise  
🔐 Security depends on reducing exposed services  

</div>
