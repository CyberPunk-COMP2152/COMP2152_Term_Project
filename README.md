# COMP2152 — Term Project: CTF Bug Bounty

## Project Overview
The project focuses on identifying misconfigurations, insecure implementations, and information disclosure vulnerabilities.

## Team Name
<!-- Replace with your team name -->
CyberPunk

## Team Members

| Member | Vulnerability Found | Branch Name |
|--------|-------------------|-------------|
| Hooman Abedi | Header Exposure, Missing Security Headers, Insecure HTTP | header_exposure, missing_headers, http_insecure |
| Ali Sazesh | API Exposure / Input Testing | ali_api_search |
| Amir Ghaffari | Directory Exposure / Sensitive File Exposure | amir_backup_storage |

## Videos

Each team member records a short video (max 3 minutes) explaining their vulnerability. Add your YouTube links below:

- Hooman Abedi: https://youtube.com/watch?v=_______
- Ali Sazesh: https://youtube.com/watch?v=_______
- Amir Ghaffari: https://youtube.com/watch?v=_______

## Target

- Server: `0x10.cloud` and its subdomains
- Submission: http://submit.0x10.cloud
- Leaderboard: http://ranking.0x10.cloud

## Important: Rate Limit

The server allows **10 requests per second** per IP address. If you send requests too fast, you will get blocked (HTTP 429). Add a small delay between requests:

```python
import time
time.sleep(0.15)  # wait 150ms between requests
```
## Vulnerabilities Found

### 1. Header Exposure
**Target:** `api.0x10.cloud`  
**Description:**  
The server exposes HTTP headers that reveal server information such as server type and configuration details. This allows attackers to identify technologies and versions used.

**Risk:**  
Information disclosure that can help attackers exploit known vulnerabilities.

---

### 2. Missing Security Headers
**Target:** `search.0x10.cloud`  
**Description:**  
Missing important headers:
- X-Frame-Options  
- Content-Security-Policy  
- X-Content-Type-Options  

**Risk:**  
- Cross-Site Scripting (XSS)  
- Clickjacking  
- MIME-type attacks  

---

### 3. Insecure HTTP Communication
**Target:** `upload.0x10.cloud`  
**Description:**  
The server allows communication over HTTP instead of enforcing HTTPS.

**Risk:**  
Sensitive data can be intercepted via Man-in-the-Middle attacks.

---

### 4. Directory Exposure
**Target:** `backup.0x10.cloud`  
**Description:**  
Directory listing is enabled, exposing internal folders and files.

**Risk:**  
Attackers can access sensitive files and system structure.

---

### 5. Sensitive File Exposure
**Target:** `storage.0x10.cloud`  
**Description:**  
Sensitive files such as `.env` and configuration files are accessible.

**Risk:**  
Exposure of credentials and internal configurations.

---

### 6. Jenkins Misconfiguration
**Target:** `jenkins.0x10.cloud`  
**Description:**  
Jenkins dashboard is accessible without authentication.

**Risk:**  
- Unauthorized access to build pipelines  
- Exposure of credentials  
- Potential full system compromise  

---

### 7. Unrestricted File Upload
**Target:** `upload.0x10.cloud`  
**Description:**  
The application allows uploading files without validating file types.

**Risk:**  
- Upload of malicious scripts  
- Remote code execution  
- Server compromise  

---

### 8. Port Scanning
**Target:** `telnet.0x10.cloud`  
**Description:**  
Port scanning was performed to detect open network services.

**Risk:**  
Open ports may expose services that can be exploited.

---

## Screenshots
The screenshots demonstrate proof of vulnerabilities and script execution results.
All screenshots are located in the `/screenshots` folder and include:
- Script execution outputs (terminal)
- Browser evidence of vulnerabilities
- GitHub Pull Request and merge workflow

---

## Scripts
Each script is designed to demonstrate a specific vulnerability using Python standard libraries.
All custom scripts are located in the `/scripts` folder and include:
- header_exposure.py
- jenkins_header_exposure.py
- missing_headers.py
- http_check.py
- dir_check.py
- port_scan.py
- ali_api_check.py
- amir_backup_check.py

## Getting Started

1. Look at the three example scripts:
   - `example_http_check.py` — checks if a site uses HTTPS (uses `urllib`)
   - `example_port_check.py` — checks if a port is open (uses `socket`)
   - `example_header_check.py` — reads HTTP response headers for info leaks (uses `urllib`)
2. Run all examples: `python3 main.py`
3. Create your own branch: `git checkout -b your_vuln_name`
4. Write a Python script that finds and demonstrates a vulnerability
5. Submit your finding at http://submit.0x10.cloud
6. Merge your branch into master when done

## Rules

- **Python standard library only** — `socket`, `urllib`, `ssl`, `json`, `base64`, `time`. No pip packages.
- **Only scan `*.0x10.cloud`** — do not scan any other domain.
- **Respect the rate limit** — 10 requests/second max.

## Conclusion
This project demonstrated how common security vulnerabilities can be identified using simple tools and scripts. It highlights the importance of proper configuration and security practices in web applications.