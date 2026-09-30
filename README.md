
<img width="100%" src="https://capsule-render.vercel.app/api?type=rounded&color=0:111827,45:374151,100:991b1b&height=185&section=header&text=Mediroza%20Security%20Assessment&fontSize=38&fontColor=fca5a5&fontAlignY=35&desc=Networkwalks%20B083%20%7C%20Week%204%20Capstone%20Project&descAlignY=55&descSize=17&font=&stroke=000000" alt="Mediroza Security Assessment">

<p align="center">
  <a href="https://git.io/typing-svg"><img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=18&duration=3500&pause=1000&color=F87171&center=true&vCenter=true&width=600&height=35&lines=External+Web+Application+Security+Review;Authorized+Black-Box+Penetration+Test;Protecting+Patient+Privacy+%26+Digital+Defenses" alt="Typing SVG" /></a>
</p>

<p align="center">
  <img alt="Assessment type: Black box" src="https://img.shields.io/badge/ASSESSMENT-BLACK%20BOX-4b5563?style=for-the-badge&labelColor=1f2937">
  <img alt="Overall risk: Critical" src="https://img.shields.io/badge/OVERALL%20RISK-CRITICAL-ef4444?style=for-the-badge&labelColor=1f2937">
</p>
<p align="center">
  <img alt="Seven findings" src="https://img.shields.io/badge/FINDINGS-7-6b7280?style=flat-square&labelColor=1f2937">
  <img alt="Three critical findings" src="https://img.shields.io/badge/CRITICAL-3-ef4444?style=flat-square&labelColor=1f2937">
  <img alt="Two high findings" src="https://img.shields.io/badge/HIGH-2-f87171?style=flat-square&labelColor=1f2937">
  <img alt="Authorized testing" src="https://img.shields.io/badge/STATUS-FULLY%20AUTHORIZED-9ca3af?style=flat-square&labelColor=1f2937">
</p>

> ⚠️ **Overall Risk Level: CRITICAL.** This assessment uncovered a seamless attack path starting right at the public-facing login portal and leading straight to sensitive patient medical records, internal staff payrolls, and corporate ownership details.

<br>

## 📌 Project Overview

This repository records an authorized black-box penetration test performed on the web infrastructure of Mediroza General Hospital (`[https://medirozahospital.com](https://medirozahospital.com)`) as part of the Networkwalks B083 Week 4 Capstone Project. The engagement focused on uncovering security flaws, illustrating their real-world impact through controlled exploitation, and providing practical hardening strategies.

Across the assessment, seven vulnerabilities were identified, scaling from Medium to Critical severity. The core security breakdown began with a SQL injection flaw on the patient portal login page. In this controlled test environment, this single flaw enabled a complete authentication bypass, opened access to confidential patient lab report PDFs, leaked sensitive administrative metadata, and ultimately exposed an unencrypted database backup containing sensitive employee payrolls and corporate shareholder details.

<br>

## 💡 Objectives


* **External Assessment:** Evaluate the web application's security posture from an unauthenticated, black-box perspective.
* **Vulnerability Discovery:** Uncover weaknesses across authentication workflows, input validation mechanisms, file access controls, and server configurations.
* **Impact Validation:** Demonstrate the real-world operational impact of each discovered flaw through safe, controlled exploitation.
* **Actionable Guidance:** Document comprehensive technical evidence and deliver prioritized, practical remediation strategies to harden the application.

<br>

## 🔐 Authorization & Scope

Testing was conducted strictly under written authorization from the client as part of a controlled educational exercise for the Networkwalks capstone program. All activities adhered strictly to the defined rules of engagement.

| Scope Status | Target / Assessment Boundary |
| :--- | :--- |
| ✅ **In-Scope** | • Public-facing web application behavior<br>• Patient portal and all discovered web paths within `https://medirozahospital.com` |
| ❌ **Out-of-Scope**| • Social engineering attacks against staff or users<br>• Denial of Service (DoS) or stress testing<br>• Any domains, systems, or IP addresses not explicitly agreed upon |

<br>

## ⚙️ Assessment Methodology
 
 
The evaluation followed a phased, structured black-box approach to ensure comprehensive coverage and safe execution:

* **Reconnaissance:** Performed initial intelligence gathering and surface mapping using open-source tools and public-facing endpoints.

* **Vulnerability Discovery:** Analyzed application logic, input fields, and authentication workflows to identify potential security gaps.

* **Controlled Exploitation:** Safely verified the operational impact of each flaw within the authorized testing boundaries without causing disruption.
  
* **Reporting & Remediation:** Documented technical evidence, step-by-step reproduction paths, and prioritized defensive hardening recommendations.

<br>

## 🧰 Tools Used

| Tool | Purpose in the Assessment |
| :--- | :--- |
| **cURL** | Sending HTTP requests and reviewing web-server responses |
| **Browser Developer Tools** | Inspecting page source and login-form behavior |
| **Burp Suite** | Intercepting, analyzing, and modifying HTTP request traffic during login and input testing |
| **Networkwalks Hash Calculator** | Extracting PDF password hashes |
| **Networkwalks Password Cracker** | Testing PDF password hashes against wordlists |
| **QPDF** | Decrypting password-protected PDFs after password recovery |
| **ExifTool** | Reading hidden metadata from PDFs |
| **ChatGPT** | Converting raw SQL data into readable tables during analysis |

<br>

## 📋 Executive Summary

Overall, the application demonstrated a critically weak security posture. A sequence of minor oversights allowed an external, unauthenticated attacker to chain vulnerabilities together—moving from initial surface mapping all the way to patient files and an exposed database backup.

The recovered database contained confidential records for 30 hospital employees and 10 shareholders. All personal and financial data has been strictly redacted from this repository to ensure privacy.

Immediate patch management and configuration hardening are urgently required for all identified Critical and High-risk issues.

<br>

## 📊 Summary of Findings

| Ref | Vulnerability Description | Target Location | Severity |
| --- | --- | --- | --- |
| **Vuln-01** | Username enumeration via differential login responses | `patient/login.php` | 🟡 **Medium** |
| **Vuln-02** | SQL injection authentication bypass | `patient/login.php` | 🔴 **Critical** |
| **Vuln-03** | Unauthorized access to encrypted patient PDFs | `patient/reports/` | 🟠 **High** |
| **Vuln-04** | Weak user passwords protecting confidential PDFs | `patient_report_*.pdf` | 🟠 **High** |
| **Vuln-05** | Directory enumeration & sensitive endpoint exposure via automated tooling revealing hidden admin panels and configuration files | `/` (Root domain) | 🟡 **Medium** |
| **Vuln-06** | Exposed legacy backup folder with directory indexing | `/old/` | 🔴 **Critical** |
| **Vuln-07** | Plaintext employee payroll and corporate shareholder data | `/old/mediroza_db_backup_2019.sql` | 🔴 **Critical** |

Let me know when you are ready to write out the detailed subsections or if you need any code snippets generated for your evidence screenshots!

<br>

## The Attack Chain

### 1. Reconnaissance:
Mapped the target surface using footprinting utilities including `WHOIS`, `nslookup`, `curl -I`, `wafw00f`, `dnsrecon` and `Nmap`. An inspection of `robots.txt` subsequently disclosed restricted server paths (`/patient/`, `/staff/`, and `/old/`), providing a clear roadmap for the assessment.

### 2. Username enumeration via differential login responses:
The login page leaked account validity by returning distinct error messages for invalid usernames versus incorrect passwords, confirming a valid administrative user account.

<p align="center">
  <img src="https://github.com/user-attachments/assets/b2b73cd6-96df-4753-8243-058ef847b707" alt="Username Enumeration Proof" width="800" /><br>
  <em>Differential error responses confirmed the existence of a valid administrative user account, streamlining subsequent attacks.</em>
</p>


### 3. SQL Injection Auth Bypass: 
The patient portal login page (`/patient/login.php`) suffered from a severe SQL injection vulnerability. Inputting `admin'--` as the username alongside an empty password successfully manipulated the database query logic, returning an HTTP `302` redirect to `portal.php` and granting an authenticated session without credentials.

<p align="center">
  <img src="https://github.com/user-attachments/assets/3ba6db84-d42f-4833-a881-2cf2d2179f2d" alt="Burp Suite SQL Injection Proof" width="850" /><br>
  <em>The injected login request triggered an HTTP 302 Found response, successfully bypassing authentication.</em>
</p>

Once inside the portal, the application exposed three password-protected patient lab reports for download.

### 4. Unauthorized access to encrypted patient PDFs
Following the successful authentication bypass, the patient portal provided direct download access to three sensitive lab-report PDFs that should have been strictly restricted to authorized clinicians and their respective patients.

<p align="center">
  <img src="https://github.com/user-attachments/assets/0a019352-3a13-4716-a695-059d081cba71" alt="Directory listing of /patient/reports/ showing downloadable PDFs" width="800" /><br>
  <em>Directory listing of /patient/reports/ reveals three downloadable PDFs.</em>
</p>

### 5. Weak user passwords protecting confidential PDFs:
Despite PDF encryption, the weak passwords used were easily compromised using standard wordlists; two reports were unlocked with a basic 100-word list, while the final file required John the Ripper's default dictionary, demonstrating that the applied protection offered negligible security for confidential medical records.

<p align="center">
  <img src="https://github.com/user-attachments/assets/17827aa6-d6a9-4375-a848-445243043b3f" alt="PDF Password Cracking Proof" width="800" /><br>
  <em>Cracking weak PDF passwords using standard wordlists to recover protected medical documents.</em>
</p>

### 6. Directory enumeration & sensitive endpoint exposure via automated tooling revealing hidden admin panels and configuration files:

* **Exposed Administrative Directories**: Multiple user and system home directories (including `~admin/`, `~administrator/`, `~test/`, `~root/`, and `~sysadm/`) returned a `301 Moved Permanently` status code.


* **Legacy Backup Directory**: An obsolete `old/` directory was uncovered with a `301` status, presenting a risk of housing unmaintained scripts or legacy files.


* **Exposed Sensitive Files**: Critical application entry points—such as `robots.txt` and the `wp-admin` portal—were exposed with a `200` status, expanding the attack surface.

<div align="center">
  <img src="https://github.com/user-attachments/assets/5acff773-3bf9-47a1-ae9f-5721667cee6e" alt="Screenshot_2026-09-29_13_25_33" width="800" /><br>
  <img src="https://github.com/user-attachments/assets/c14b43fa-73d9-4a85-9c5f-a757000f0d72" alt="Screenshot_2026-09-29_13_26_14" width="800" /><br>
  <em>Gobuster directory enumeration results revealing exposed user home directories, legacy backup paths, and sensitive administrative files.</em>
</div>

