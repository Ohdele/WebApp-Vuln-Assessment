
## Phase 1: Environment Setup (VM & Network)

**Objective:** Set up the Attacker (Ubuntu) and Target (DVWA Host) virtual machines and configure the network (IP addresses and communication check).

[View Output in phase1-output.txt]

---

## Phase 2: DVWA Deployment & Fixes

**Objective:** Deploy DVWA, resolve database access issues, and ensure the application is fully operational for testing.

**Issue Encountered:**
- PHP Fatal error in Apache logs: `Access denied for user 'root'@'localhost'`
- File: `/var/www/html/dvwa/dvwa/includes/DBMS/MySQL.php:13`
- Occurred during initial setup at: `http://192.168.10.11/dvwa/setup.php`

**Resolution Steps:**
1. **Database Fix**
   - Created a dedicated database user:

2. **Configuration Update**
   - Updated `/var/www/html/dvwa/config/config.inc.php` to use the new database credentials.

3. **Apache Adjustments**
   - Verified Apache configuration and restarted service to apply changes.

**Outcome:**
- DVWA database connection established successfully.
- Application login accessible at: [http://192.168.10.11/dvwa/login.php](http://192.168.10.11/dvwa/login.php)  
- Credentials: `admin / password`

[View Output in phase2-output.txt]

---

## Phase 3: Reconnaissance (Nmap and Directory Enumeration)

**Objective:** Perform network port scanning (Nmap) and directory enumeration on the target server to identify running services, non‑standard ports, and hidden application paths.

[View Commands and Outputs in phase3_log.txt]

---

## Phase 4: Vulnerability Analysis and Exploitation

**Objective:** Test for and successfully exploit three key vulnerabilities (SQL Injection, Local File Inclusion, and File Upload) on the DVWA application to confirm compromise.

[View Commands and Outputs in phase4_log.txt]

---

## Phase 5: Post-Exploitation and Privilege Escalation

**Objective:** Escalate privileges from the compromised web user (`www-data`) to the system administrator (root) by exploiting local vulnerabilities.

[View Commands and Outputs in phase5_log.txt]

---

## Risk Analysis (Business Impact)

The successful exploitation demonstrates **Critical Risk** to the organization, requiring immediate remediation.

| Vulnerability | Technical Impact | Business Impact | Risk Rating |
| :--- | :--- | :--- | :--- |
| **SQL Injection (SQLi)** | Complete database compromise (data theft/modification). | Loss of customer data, unauthorized administrator access, regulatory fines. | **Critical** |
| **File Upload (RCE)** | Full remote code execution as the web user (`www-data`). | Complete control of the web server, leading to defacement, pivoting, and service disruption. | **Critical** |
| **Privilege Escalation** | Gained root access (highest level) on the server. | Total server compromise, ability to install backdoors, steal all local files, and affect other internal systems. | **Critical** |

---

## Remediation Guidance

These are the immediate steps required to mitigate the vulnerabilities found in this assessment:

1.  **Input Validation & Parameterization:** **Never** concatenate user input directly into SQL queries. Use **Prepared Statements** (parameterized queries) for all database interaction to eliminate SQL Injection.
2.  **File Upload Hardening:** Implement a robust upload filter that relies on a **whitelist** of allowed file extensions (e.g., `.jpg`, `.png`). Store uploaded files outside of the web root, and rename them to prevent execution.
3.  **Principle of Least Privilege:** The web service (`www-data`) **must not** have sensitive SUID permissions. Remove the SUID bit from binaries like `/usr/bin/find`. Limit file permissions for the web user to only what is strictly necessary.
