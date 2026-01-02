# VAPT Report: OWASP Juice Shop Web Application Assessment

##  Project Overview
This repository contains a comprehensive Vulnerability Assessment and Penetration Testing (VAPT) report for **OWASP Juice Shop**, a modern web application designed with intentional security flaws. The assessment follows a black-box methodology, demonstrating a complete attack lifecycle—from initial reconnaissance and logic abuse to administrative account takeover and supply chain analysis.

##  Target Profile
- **Target Application:** OWASP Juice Shop (Node.js / Express / SQLite)
- **Primary Attack Vectors:** SQL Injection (SQLi), Cross-Site Scripting (XSS), IDOR
- **Risk Severity:** CRITICAL (Multiple High/Critical findings)

##  Executive Summary
Successfully compromised the application's administrative tier by exploiting a **Union-Based SQL Injection** in the login portal. Following the initial compromise, I performed a full database dump to exfiltrate user credentials and bypassed access controls to manipulate customer orders. The assessment also uncovered a **Supply Chain Vulnerability** via a "Poison Null Byte" attack, allowing the exfiltration of the backend `package.json` file to identify outdated and vulnerable dependencies.

##  Key Skills & Tools Demonstrated
- **Reconnaissance:** Endpoint enumeration and traffic analysis using `Burp Suite Community` and `Firefox Developer Tools`.
- **Exploitation:** Manual execution of SQL Injection (`UNION SELECT`) and Reflected XSS payloads to bypass frontend restrictions.
- **Post-Exploitation:** Schema extraction and mass credential harvesting (User/Password Hash dump).
- **Supply Chain Analysis:** identified specific version vulnerabilities in backend libraries (`sanitize-html`, `sqlite3`) by retrieving the server's dependency manifest.
- **Logic Abuse:** Exploited Insecure Direct Object References (IDOR) to manipulate shopping baskets and forge customer reviews.
- **Reporting:** Authored a professional remediation report focusing on Input Validation, RBAC enforcement, and Secrets Management.

##  Documentation
- **[Full Technical Report (PDF)](./OWASP%20Juice%20Shop%20Web%20Application%20Security%20Assessment.pdf)** - Detailed step-by-step walk-through, screenshots, and remediation roadmap.

##  Lessons Learned
- **Input Validation is Non-Negotiable:** A single unvalidated input field on the login page compromised the entire administrative tier, reinforcing the need for global sanitization.
- **"Soft Deletion" Risks:** Marking database rows as "deleted" without physical removal allows attackers to recover sensitive data via SQL Injection.
- **Obscurity != Security:** Attempts to hide paths using Base64/ROT13 encoding or "hidden" directories (like `/ftp`) were trivially bypassed during the recon phase.
- **Strategic Pivot:** While web exploitation is effective, analyzing the backend architecture (the "Supply Chain" finding) provided the most critical insight into the system's long-term security posture.

---
*Disclaimer: This project was conducted in a locally hosted, authorized lab environment for educational purposes. Unauthorized hacking is illegal and unethical.*
