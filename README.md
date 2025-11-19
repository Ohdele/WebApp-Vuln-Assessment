
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

