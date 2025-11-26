# AutoRecon Toolkit

<p align="center">
  <img src="https://img.shields.io/badge/Language-Python%203-blue?style=for-the-badge">
  <img src="https://img.shields.io/badge/License-MIT-green?style=for-the-badge">
  <img src="https://img.shields.io/badge/Status-Stable-success?style=for-the-badge">
  <img src="https://img.shields.io/badge/Platform-Linux%20%7C%20Kali%20%7C%20Windows-lightgrey?style=for-the-badge">
  <img src="https://img.shields.io/badge/Recon-Automated-red?style=for-the-badge">
</p>


AutoRecon is a lightweight automated reconnaissance tool written in Python.  
It combines multiple industry-standard recon tools into a single, easy-to-use workflow.  
This toolkit is designed for CTFs, penetration testing labs, and bug bounty recon.

---

## Features

- WAF detection (wafw00f)
- SSL certificate expiry information
- Subdomain enumeration (subfinder)
- Technology fingerprinting (WhatWeb)
- Service discovery (Nmap -sV)
- URL Crawling (Katana)
- Historical URLs (waybackurls)
- Colored CLI output
- Generates a full recon summary report
- Plug-and-play design—no frameworks needed


## Installation

1.Install Required External Tools:

sudo apt install -y wafw00f whatweb nmap openssl

go install -v github.com/projectdiscovery/subfinder/v2/cmd/subfinder@latest

go install -v github.com/projectdiscovery/katana/cmd/katana@latest

go install -v github.com/tomnomnom/waybackurls@latest


2.Add Go bin PATH if tools are not detected:

export PATH=$PATH:$(go env GOPATH)/bin


3.Usage:

autorecon -h              

Usage:
    autorecon <target>

Example:
    autorecon https://testphp.vulnweb.com

Description:
    Performs automated recon including:
    • WAF detection
    • SSL date scan
    • Subdomain enumeration
    • Technology detection
    • Service scan (nmap -sV)
    • Katana crawling
    • Wayback archive URLs

### 2. Clone Repository
```bash

git clone https://github.com/Themar-Y/autorecon-toolkit.git
cd autorecon-toolkit

## 3.Threat Model (STRIDE-Based)

This section outlines the potential risks and security considerations surrounding the use of the AutoRecon Toolkit.  
It follows the **STRIDE framework**, a standard in threat modeling for security tools.

---

### **Objective**
AutoRecon performs automated information gathering using publicly available reconnaissance tools.  
The goal of this threat model is to:

- Identify **misuse risks**
- Define **ethical boundaries**
- Explain **possible attack vectors**
- Suggest **mitigations**

---

# STRIDE Analysis

---

## **1. Spoofing**
**Risk:**  
The tool does not provide authentication, identity verification, or request signing.  
An attacker could intentionally spoof their source IP or run scans anonymously.

**Impact:**  
- Hard to attribute scans  
- Could be used to hide malicious activity  

**Mitigation:**  
- Add legal usage warnings  
- Log execution timestamps if used in enterprise environments  
- Use approved VPN / testing environment for authorized engagements only  

---

## **2. Tampering**
**Risk:**  
AutoRecon relies on external binaries (nmap, subfinder, wafw00f, katana, waybackurls).  
A malicious user could replace binaries with trojanized versions.

**Impact:**  
- Output manipulation  
- Execution of unauthorized code  
- Compromised system integrity  

**Mitigation:**  
- Install recon tools from official sources  
- Validate checksums where possible  
- Use isolated environments (VM / containers)

---

## **3. Repudiation**
**Risk:**  
The tool does not track user identity or maintain audit logs.  
Actions could be denied or left unattributed.

**Impact:**  
- Lack of traceability  
- Difficult incident investigation  

**Mitigation:**  
- Optional: enable logging mode in enterprise settings  
- Maintain separate activity logs during pentest engagements  

---

## **4. Information Disclosure**
**Risk:**  
The tool collects recon data such as:
- Subdomains  
- URLs  
- Server technologies  
- SSL metadata  

These results may contain sensitive information about the target environment.

**Impact:**  
- Accidental exposure if reports are shared publicly  
- Leakage of internal attack surface  

**Mitigation:**  
- Store `<domain>_recon_summary.txt` securely  
- Never commit recon results to public GitHub repos  
- Encrypt or restrict access to stored scan data  

---

## **5. Denial of Service (DoS)**
**Risk:**  
Some scans (e.g., nmap, katana crawling) generate heavy traffic.  
Running them aggressively can overwhelm small or poorly configured servers.

**Impact:**  
- Unintentional DoS  
- High load on target systems  

**Mitigation:**  
- Use moderate scan intensity (`-T4` instead of `-T5`)  
- Add optional rate-limiting or delays  
- Perform scans only on permitted systems with written authorization  

---

## **6. Elevation of Privilege**
**Risk:**  
AutoRecon itself does not require root privileges, but external tools may:
- nmap may require root for advanced scans  
- Other tools could request system-level permissions  

**Impact:**  
- Possible execution with elevated privileges  
- Increased impact if a tool is compromised  

**Mitigation:**  
- Run AutoRecon as a non-root user whenever possible  
- Only elevate privileges when absolutely necessary  

---

# **Threat Modeling Summary**

| STRIDE Category       | Risk Level | Requires Mitigation? |
|-----------------------|-----------|-----------------------|
| Spoofing             | Medium    | Yes |
| Tampering            | High      | Yes |
| Repudiation          | Low/Med   | Optional |
| Information Disclosure | High      | Yes |
| DoS                  | Medium    | Yes |
| Elevation of Privilege | Low       | Minimal |



# **Legal & Ethical Use Notice**

AutoRecon is intended **solely for educational purposes, CTFs, and authorized penetration testing**.  
Running this tool on systems without explicit permission is illegal and unethical.

The authors are not responsible for misuse.

## License
This project is licensed under the MIT License. See the LICENSE file for details.


## Why requirements.txt?

The `requirements.txt` file is included to ensure users can quickly install the Python dependencies required for the AutoRecon Toolkit.

Although the toolkit relies mainly on external system tools (such as `nmap`, `subfinder`, `whatweb`, `katana`, and `waybackurls`), it uses one Python package for terminal formatting:

- `colorama`

Including this file helps provide:

### ✔ Consistency
All users install the same Python packages, ensuring the tool behaves the same across environments.

### ✔ Easy Setup
Users can install everything with a single command:

```bash
pip install -r requirements.txt


                      
