
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
| **Gobuster** | Automating directory and file enumeration to discover hidden server endpoints and paths |
| **Browser Developer Tools** | Inspecting page source and login-form behavior |
| **Burp Suite** | Intercepting, analyzing, and modifying HTTP request traffic during login and input testing |
| **Networkwalks Hash Calculator** | Extracting PDF password hashes |
| **Networkwalks Password Cracker** | Testing PDF password hashes against wordlists |
| **QPDF** | Decrypting password-protected PDFs after password recovery |
| **ExifTool** | Reading hidden metadata from PDFs |
| **Gemini** | Converting raw SQL data into readable tables during analysis |

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

<br>

## The Attack Chain

### 0. Reconnaissance:
Mapped the target surface using footprinting utilities including `WHOIS`, `nslookup`, `curl -I`, `wafw00f`, `dnsrecon` and `Nmap`. An inspection of `robots.txt` subsequently disclosed restricted server paths (`/patient/`, `/staff/`, and `/old/`), providing a clear roadmap for the assessment.

### 1. Username enumeration via differential login responses:
The login page leaked account validity by returning distinct error messages for invalid usernames versus incorrect passwords, confirming a valid administrative user account.

<p align="center">
  <img src="https://github.com/user-attachments/assets/b2b73cd6-96df-4753-8243-058ef847b707" alt="Username Enumeration Proof" width="800" /><br>
  <em>Differential error responses confirmed the existence of a valid administrative user account, streamlining subsequent attacks.</em>
</p>


### 2. SQL Injection Auth Bypass: 
The patient portal login page (`/patient/login.php`) suffered from a severe SQL injection vulnerability. Inputting `admin'--` as the username alongside an empty password successfully manipulated the database query logic, returning an HTTP `302` redirect to `portal.php` and granting an authenticated session without credentials.

<p align="center">
  <img src="https://github.com/user-attachments/assets/3ba6db84-d42f-4833-a881-2cf2d2179f2d" alt="Burp Suite SQL Injection Proof" width="850" /><br>
  <em>The injected login request triggered an HTTP 302 Found response, successfully bypassing authentication.</em>
</p>

Once inside the portal, the application exposed three password-protected patient lab reports for download.

### 3. Unauthorized access to encrypted patient PDFs:
Following the successful authentication bypass, the patient portal provided direct download access to three sensitive lab-report PDFs that should have been strictly restricted to authorized clinicians and their respective patients.

<p align="center">
  <img src="https://github.com/user-attachments/assets/0a019352-3a13-4716-a695-059d081cba71" alt="Directory listing of /patient/reports/ showing downloadable PDFs" width="800" /><br>
  <em>Directory listing of /patient/reports/ reveals three downloadable PDFs.</em>
</p>

### 4. Weak user passwords protecting confidential PDFs:
Despite PDF encryption, the weak passwords used were easily compromised using standard wordlists; two reports were unlocked with a basic 100-word list, while the final file required John the Ripper's default dictionary, demonstrating that the applied protection offered negligible security for confidential medical records.

<p align="center">
  <img src="https://github.com/user-attachments/assets/17827aa6-d6a9-4375-a848-445243043b3f" alt="PDF Password Cracking Proof" width="800" /><br>
  <em>Cracking weak PDF passwords using standard wordlists to recover protected medical documents.</em>
</p>

### 5. Directory enumeration & sensitive endpoint exposure via automated tooling revealing hidden admin panels and configuration files:

* **Exposed Administrative Directories**: Multiple user and system home directories (including `~admin/`, `~administrator/`, `~test/`, `~root/`, and `~sysadm/`) returned a `301 Moved Permanently` status code.


* **Legacy Backup Directory**: An obsolete `old/` directory was uncovered with a `301` status, presenting a risk of housing unmaintained scripts or legacy files.


* **Exposed Sensitive Files**: Critical application entry points—such as `robots.txt` and the `wp-admin` portal—were exposed with a `200` status, expanding the attack surface.

<div align="center">
  <img src="https://github.com/user-attachments/assets/5acff773-3bf9-47a1-ae9f-5721667cee6e" alt="Screenshot_2026-09-29_13_25_33" width="800" /><br>
  <img src="https://github.com/user-attachments/assets/c14b43fa-73d9-4a85-9c5f-a757000f0d72" alt="Screenshot_2026-09-29_13_26_14" width="800" /><br>
  <em>Gobuster directory enumeration results revealing exposed user home directories, legacy backup paths, and sensitive administrative files.</em>
</div>

### 6. Exposed legacy backup folder with directory indexing: 
During reconnaissance, review of the `robots.txt` file identified the `/old/` directory, the relevance of which was confirmed by prior metadata analysis. Because directory listing was enabled, a database backup file was exposed to unauthenticated users and successfully downloaded during the authorized test.

<div align="center">
  <img src="https://github.com/user-attachments/assets/65bea792-1851-4c80-83a9-b48e02677230" alt="Screenshot_2026-09-28_19_58_35" width="800" /><br>
  <em>The robots.txt file for medirozahospital.com revealing sensitive disallowed directories including /old/, /patient/, and /staff/. </em>
</div>
<br>

<div align="center">
  <img src="https://github.com/user-attachments/assets/891d0d70-ccfc-43ad-9b94-caea3aabddd5" alt="Screenshot_2026-09-29_13_34_43" width="800" /><br>
  <em>Additional evidence of the database backup and contents uncovered during the assessment.</em>
</div>
The recovered database backup comprised 30 employee records; detailing names, national identification numbers, and salaries, alongside the complete 10-entry shareholder register.

### 7. Plaintext employee payroll and corporate shareholder data:
The compromised database backup exposed unencrypted records for both employees and shareholders. Employee details featured names, positions, contact numbers, national identification numbers, and monthly compensation, while shareholder details listed names, ownership shares, and share categories. To protect privacy, this document outlines the extent of the exposure rather than displaying the raw, sensitive data.

<div align="center">
  <img src="https://github.com/user-attachments/assets/8f88f549-ac40-4483-b2be-dd6596ae13f7" alt="Screenshot_2026-09-29_13_38_25" width="800" /><br>
  <img src="https://github.com/user-attachments/assets/dbf0c748-0c36-41b3-abaa-707873e9923d" alt="Screenshot_2026-09-29_13_38_44" width="800" /><br>
  <img src="https://github.com/user-attachments/assets/3eedb9ef-282f-4a86-a3ce-e0f79ef9f281" alt="Screenshot_2026-09-29_13_38_51" width="800" /><br>
  <em>Evidence of the exposed database backup file and contents discovered within the legacy directory during the assessment.</em>
</div>

<br>

# ⚔️ Attack Chain Walkthrough

**1. Reconnaissance & Endpoint Exposure (`Vuln-05`)** 
Automated tooling and initial analysis of the root domain (`/`) uncovered directory enumeration and exposed sensitive endpoints, including paths revealed via `robots.txt`.

**2. Username Enumeration (`Vuln-01`)** 
Inspecting the login interface at `patient/login.php`, differential error messages permitted successful username enumeration to identify valid accounts.

**3. Authentication Bypass (`Vuln-02`)** 
Leveraging vulnerable input handling on `patient/login.php`, a controlled SQL injection payload bypassed authentication controls entirely.

**4. Portal Access (`Vuln-03`)** 
Bypassing the login mechanism granted unauthorized access to restricted directories and files within `patient/reports/`.

**5. Document Access (`Vuln-03`)** 
Confidential patient lab-report PDFs were downloaded directly from the portal interface.

**6. Credential Weakness (`Vuln-04`)** 
Wordlist attacks easily defeated the weak user passwords protecting these confidential `patient_report_*.pdf` files.

**7. Internal Footprinting** 📝
Metadata extracted from the unlocked PDFs exposed an internal staff note pointing toward legacy structures.

**8. Directory Indexing (`Vuln-06`)** 
Investigation of the legacy endpoint revealed an exposed legacy backup folder with directory indexing enabled at `/old/`.

**9. Critical Data Compromise (`Vuln-07`)** 
Accessing `/old/mediroza_db_backup_2019.sql` directly exposed plaintext employee payroll details and corporate shareholder data.

# Full Report

<br>

# 💡 Lessons Learned

The penetration test against `medirozahospital.com` highlighted several critical takeaways for improving organizational security posture:

* **Chained Vulnerabilities:** Small security flaws can combine into a high-impact attack chain.

* **Information Disclosure:** Authentication errors and database errors reveal valuable information to attackers.

* **Cryptographic Weakness:** Encryption is ineffective when document passwords are weak and easily guessed.

* **Metadata Security:** Document metadata requires the same security review as visible content.

* **Backup Management:** Backups must never be placed in publicly accessible web directories.

* **Defense in Depth:** Defense in depth is essential: secure input handling, authorization, file storage, server configuration, and data governance must all work together.

<br>

# 🏁 Conclusion

This assessment successfully demonstrated an end-to-end attack path from the initial login interface to highly sensitive internal data, driven entirely by common and preventable flaws. It is strongly recommended that all Critical and High-risk findings be remediated immediately prior to deploying the system for live patient data or production use.

<br>

# ⚖️ Disclaimer

This report was produced as part of a controlled educational security assessment by Networkwalks. All testing was performed within authorized parameters and adhered strictly to the agreed-upon scope. The techniques and methodologies described in this document are intended strictly for defensive awareness and must never be executed against any system without prior, explicit written authorization from the legal owner.

<br>

# 👤 Credits

* **Author:** Kwakyewa Teming-Amoako
* **Cybersecurity Mentor:** Waqas Karim, CCIE
* **Organization:** Networkwalks
* **Program:** B083 Cybersecurity Internship – Week 4 Capstone Project

<br>

<p align="center">
  <img alt="For educational and authorized testing only" src="https://img.shields.io/badge/FOR%20EDUCATIONAL%20AND%20AUTHORIZED%20TESTING%20ONLY-0b1026?style=for-the-badge">
</p>

<!-- FOOTER -->
<img width="100%" src="https://capsule-render.vercel.app/api?type=rounded&color=0:111827,45:374151,100:991b1b&height=120&section=footer&text=Networkwalks%20B083%20%7C%20Week%204%20Capstone&fontSize=20&fontColor=fca5a5&fontAlignY=50&stroke=000000" alt="Mediroza Security Assessment Footer">
