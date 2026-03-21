<div align="center">

## 🌐 Web Application Security Investigation  
### Hidden Endpoint Discovery & Unauthorized Transaction Exploit

![Category](https://img.shields.io/badge/Category-Web%20Security-blue?style=for-the-badge)
![Focus](https://img.shields.io/badge/Focus-Enumeration%20%7C%20Exploitation-purple?style=for-the-badge)
![Impact](https://img.shields.io/badge/Impact-Unauthorized%20Access-red?style=for-the-badge)

</div>

---

<div align="center">
  <img src="images/Screenshot 1.png" width="500">
</div>

---

## 🧠 Scenario

A web-based banking application was assessed from an attacker perspective to identify exposed functionality and potential security weaknesses.

The investigation focused on:

- identifying hidden application endpoints  
- analyzing access controls  
- determining exploitability of discovered functionality  
- evaluating potential impact of unauthorized actions  

---

## 🎯 Objective

Simulate real-world web application enumeration and exploitation techniques to identify and abuse exposed functionality.

Focus areas:

- endpoint discovery  
- access control weaknesses  
- unauthorized functionality execution  
- impact validation  

---

## 🖥️ Environment

| Tool | Purpose |
|---|---|
| Kali Linux | Attack platform |
| Gobuster | Directory enumeration |
| Web Browser | Application interaction |
| Wordlist | Endpoint discovery |

---

## 🔍 Step 1 — Enumeration

Initial reconnaissance was performed using directory brute-forcing to identify hidden application endpoints.

### 📊 Command Used

```bash
gobuster -u http://fakebank.thm -w wordlist.txt dir
```

### 📸 Evidence 1 — Enumeration Results

<div align="center">
  <img src="images/Screenshot 2.png" width="500">
</div>

**Analysis:**  
Enumeration revealed a previously undisclosed endpoint:

```
/bank-transfer
```

**Key Insight**

- sensitive functionality was not properly restricted  
- endpoint was discoverable through brute-force techniques  

---

## 🧪 Step 2 — Endpoint Discovery

The identified endpoint was manually accessed through a browser.

### 📸 Evidence 2 — Hidden Functionality

<div align="center">
  <img src="images/Screenshot 3.png" width="500">
</div>

**Analysis:**  

The endpoint exposed functionality allowing direct interaction with financial operations.

**Key Insight**

- no authentication or authorization enforcement observed  
- endpoint accessible to unauthenticated users  

---

## 💥 Step 3 — Exploitation

The exposed functionality was leveraged to perform unauthorized financial transactions.

### 📸 Evidence 3 — Unauthorized Transaction

<div align="center">
  <img src="images/Screenshot 4.png" width="500">
</div>

**Analysis:**  

An attacker was able to manipulate transaction parameters and execute unauthorized actions.

**Key Insight**

- lack of access control validation  
- client-side trust assumptions exploited  

---

## 🔐 Step 4 — Impact

The vulnerability enabled direct financial manipulation within the application.

**Impact Observed**

- unauthorized fund transfers  
- potential account compromise  
- loss of data integrity  

➡️ This represents a **critical access control failure**

---

## 🧠 Attack Flow

```text
Application reconnaissance
↓
Directory enumeration (Gobuster)
↓
Hidden endpoint discovery
↓
Unauthorized access to functionality
↓
Transaction manipulation
↓
Security impact
```

---

## 🛠️ Techniques

- directory brute-forcing  
- endpoint enumeration  
- access control bypass  
- parameter manipulation  
- web application exploitation  

---

## 🧩 MITRE ATT&CK Mapping

| Technique | Description |
|---|---|
| T1190 | Exploit Public-Facing Application |
| T1083 | File and Directory Discovery |
| T1078 | Valid Accounts (Abuse of access) |

---

## 🛡️ Remediation

### Access Control
- enforce authentication on all sensitive endpoints  
- implement role-based access control (RBAC)  

### Input Validation
- validate all transaction parameters server-side  
- restrict unauthorized account access  

### Monitoring
- log access to sensitive endpoints  
- detect abnormal transaction activity  

### Hardening
- restrict endpoint exposure  
- implement application-layer security controls  

---

## 📊 Key Takeaways

- hidden endpoints can expose critical functionality  
- enumeration remains a powerful attack vector  
- lack of access control leads to severe impact  
- sensitive operations must always be authenticated and validated  

---

## 💡 Skills Demonstrated

- web application enumeration  
- vulnerability identification  
- exploitation workflow  
- impact analysis  
- security assessment methodology  

---

<div align="center">

🌐 **Enumeration reveals what should be hidden**  
🔓 **Access control failures lead to exploitation**  
💥 **Small exposures create critical impact**

</div>
