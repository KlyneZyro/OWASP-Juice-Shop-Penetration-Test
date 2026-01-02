# OWASP Juice Shop Security Assessment 

**Target:** OWASP Juice Shop (Docker Container)  
**Type:** Web Application Security Assessment (Black Box)  
**Date:** January 2026  
**Analyst:** Klyne Zyro C. Reyes

##  [Download the Full Report (PDF)](./OWASP%20Juice%20Shop%20Web%20Application%20Security%20Assessment.pdf)

---

##  Executive Summary
This project involves a comprehensive security assessment of the OWASP Juice Shop application. The goal was to identify and exploit vulnerabilities mapped to the **OWASP Top 10** framework. The assessment simulates a real-world engagement, moving from reconnaissance to active exploitation and privilege escalation.

###  Tools Used
* **Burp Suite Community:** Traffic interception and manipulation.
* **Firefox Developer Tools:** DOM analysis and JavaScript debugging.
* **Manual Exploitation:** SQL Injection, XSS payloads, and logic abuse.

---

##  Key Findings

### 1. SQL Injection & Account Takeover (Critical)
* **Vulnerability:** The login portal failed to sanitize input, allowing for a classic SQL Injection (`' OR 1=1 --`).
* **Impact:** Bypassed authentication to gain **Administrative Access** without valid credentials.
* **Data Exfiltration:** Exploited a UNION-based SQL injection to dump the entire `Users` table and database schema.

### 2. Sensitive Data Exposure via "Soft Deletion"
* **Vulnerability:** The application marked products as "deleted" in the database but did not remove them.
* **Impact:** Used SQL injection to recover "unsafe" products (Rippertuer Special Juice) that were supposedly removed from the platform.

### 3. Supply Chain Intelligence (OSINT)
* **Vulnerability:** Uncovered a `package.json.bak` file via a "Poison Null Byte" directory traversal attack.
* **Impact:** Revealed exact version numbers of backend libraries (e.g., `sanitize-html` v1.4.2), enabling precise mapping of unpatched CVEs in the software supply chain.

### 4. Broken Access Control (IDOR)
* **Vulnerability:** Insecure Direct Object References in the Basket functionality.
* **Impact:** Allowed unauthorized viewing and manipulation of other users' shopping carts by simply changing the `bid` (Basket ID) parameter.

---

##  Professional Reflection
While this assessment focused on web-specific vectors (XSS, SQLi), the findings reinforced my interest in **Infrastructure and Network Security**. Discovering the server-side dependency leaks and understanding the backend architecture were the highlights of this engagement. 

My future projects will focus on **Post-Exploitation** and pivoting from compromised web servers into internal Active Directory environments.

---

* **Disclaimer:** This assessment was performed on a locally hosted, intentionally vulnerable application (OWASP Juice Shop) for educational purposes. No live systems were targeted.*
