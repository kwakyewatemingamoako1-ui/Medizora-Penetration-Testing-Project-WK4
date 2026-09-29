
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

## 📌 Project Objectives


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
