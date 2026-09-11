<div align="center">

## 🔎 Network & Web Application Security Assessment  
### Multi-Tool Enumeration and Service Exploitation Workflow

![Category](https://img.shields.io/badge/Category-Penetration%20Testing-blue?style=for-the-badge)
![Focus](https://img.shields.io/badge/Focus-Enumeration%20%7C%20Exploitation-purple?style=for-the-badge)
![Approach](https://img.shields.io/badge/Approach-Methodology%20Driven-success?style=for-the-badge)

</div>

---

## 🧠 Scenario

A target environment was assessed using a structured penetration testing approach to identify exposed services, hidden application functionality, and potential access vectors.

The assessment focused on combining multiple tools and techniques to simulate real-world attacker behavior across both **web and network layers**.

---

## 🎯 Objective

- identify exposed subdomains and services  
- discover hidden web application endpoints  
- enumerate open ports and services  
- gain unauthorized access to exposed systems  
- validate impact through data retrieval  

---

## 🧭 Investigation Workflow

```text
Subdomain Enumeration
         ↓
Web Enumeration (ffuf + dirb)
         ↓
Network Scanning (nmap)
         ↓
Service Analysis
         ↓
Access via Exposed Service (FTP)
         ↓
Data Retrieval
```

---

## 🔎 Step 1 — Subdomain Enumeration

Subdomain discovery was performed to expand the attack surface and identify additional entry points.

---

## 🔍 Step 2 — Web Enumeration

### Tools Used
- ffuf → targeted endpoint fuzzing  
- dirb → directory discovery and validation  

### 📸 Figure 1 — ffuf Enumeration

<div align="center">
  <img src="../images/image 27.png" width="600">
</div>

<p align="center"><em>ffuf was used to fuzz web endpoints and identify hidden application paths using a common wordlist.</em></p>

---

### 📸 Figure 2 — dirb Directory Discovery

<div align="center">
  <img src="../images/image 28.png" width="600">
</div>

<p align="center"><em>dirb confirmed the existence of multiple directories and files, including sensitive resources such as logs and private directories.</em></p>

---

## 🌐 Step 3 — Network Scanning

Network reconnaissance was conducted to identify exposed services and potential attack vectors.

### 📸 Figure 3 — Nmap Scan Results

<div align="center">
  <img src="../images/image 100.png" width="600">
</div>

<p align="center"><em>Nmap identified multiple open ports and services, including SSH, HTTP, SMTP, and POP3.</em></p>

---

## 🔬 Step 4 — Service Analysis

Analysis of the scan results revealed:

- multiple externally accessible services  
- potential misconfigurations  
- services suitable for further exploitation  

Particular attention was given to services allowing authentication or file transfer.

---

## 💥 Step 5 — Exploitation (FTP Access)

An exposed FTP service was accessed using valid credentials, allowing interaction with the remote system.

### 📸 Figure 4 — FTP Access and File Retrieval

<div align="center">
  <img src="../images/image 129.png" width="600">
</div>

<p align="center"><em>Successful FTP authentication allowed directory listing and retrieval of sensitive files, demonstrating unauthorized access to system data.</em></p>

---

## 🔐 Impact

The assessment demonstrated:

- exposure of internal services  
- ability to enumerate application structure  
- successful access to a remote system  
- retrieval of sensitive data  

➡️ This represents a **critical breakdown in access control and service exposure**

---

## 🛠️ Techniques Applied

- subdomain enumeration  
- directory and endpoint discovery  
- network scanning  
- service enumeration  
- credential-based access  
- data exfiltration via FTP  

---

## 🧩 MITRE ATT&CK Mapping

| Technique | Description |
|---|---|
| T1046 | Network Service Scanning |
| T1083 | File and Directory Discovery |
| T1078 | Valid Accounts |
| T1105 | Ingress Tool Transfer |

---

## 🛡️ Remediation

### Access Control
- restrict external access to sensitive services  
- enforce strong authentication mechanisms  

### Network Security
- limit exposed ports and services  
- implement firewall rules and segmentation  

### Monitoring
- detect abnormal scanning behavior  
- monitor login attempts and file transfers  

### Hardening
- disable unused services  
- secure file transfer mechanisms  

---

## 📊 Key Takeaways

- combining tools improves discovery effectiveness  
- exposed services significantly increase attack surface  
- enumeration is critical to identifying vulnerabilities  
- weak access controls lead directly to exploitation  
- early detection can prevent deeper compromise  

---

## 💡 Skills Demonstrated

- multi-tool enumeration  
- network and web reconnaissance  
- vulnerability identification  
- exploitation workflow  
- security assessment methodology  

---

<div align="center">

🔎 **Enumeration reveals the full attack surface**  
🌐 **Multiple tools provide deeper visibility**  
💥 **Service exposure leads to compromise**

</div>
