# Activity: Apply OS Hardening Techniques

**Course:** Google Cybersecurity Professional Certificate — Course 3: Connect and Protect: Networks and Network Security

**Platform:** Coursera (DICT Sector D Google Learning Program)

**Status:** Completed — 100% Score

**Submitted:** July 12, 2026

---

## Scenario Overview

As a cybersecurity analyst for **yummyrecipesforme.com**, a website that sells recipes and cookbooks, I investigated a security incident involving a former employee who executed a brute force attack against the administrative account.

The attacker guessed the default admin password, accessed the admin panel, and embedded a malicious JavaScript function in the website's source code. This script prompted all visitors to download an executable file. When users ran the file, their browsers were redirected to a malicious copycat site, **greatrecipesforme.com**, which contained malware.

The incident was discovered after multiple customers reported being prompted to download a file and experiencing slow computer performance afterward. The website owner was locked out of the admin panel because the attacker had changed the password post-compromise.

---

## Activity Steps Completed

### Step 1 — Identify the Network Protocol
Used the provided tcpdump traffic log to identify which network protocols were used during the attack. Determined that:
- **DNS** (Domain Name System) — Used to resolve domain names to IP addresses
- **HTTP** (Hypertext Transfer Protocol) — Used to load web pages and initiate the malicious file download

Both operate at the **Application Layer** of the TCP/IP model.

### Step 2 — Document the Incident
Documented the full sequence of events observed in the tcpdump log:
1. Browser sent DNS request → resolved yummyrecipesforme.com
2. DNS server returned the IP address
3. Browser sent HTTP GET request to yummyrecipesforme.com
4. Website triggered automatic download of malicious executable
5. Browser sent DNS request → resolved greatrecipesforme.com
6. DNS server returned IP address for greatrecipesforme.com
7. Browser sent HTTP GET request to greatrecipesforme.com (malicious site)

### Step 3 — Recommend a Remediation
Recommended **Two-Factor Authentication (2FA)** on all administrative accounts as the primary remediation to prevent future brute force attacks.

**Rationale:** Even if a malicious actor guesses or obtains the correct password, 2FA requires a second form of verification (e.g., a one-time code sent to a registered device), making unauthorized access significantly more difficult.

---

## Key Findings

| Category | Detail |
|---|---|
| Attack Type | Brute Force Attack |
| Target | Administrative account — yummyrecipesforme.com |
| Root Cause | Default admin password; no brute force protection controls |
| Attack Vector | Admin panel access via guessed default credentials |
| Malicious Action | JavaScript injection → forced file download → browser redirect |
| Malware Destination | greatrecipesforme.com |
| Protocols Identified | DNS, HTTP (Application Layer — TCP/IP) |
| Evidence Sources | tcpdump log, source code review, downloaded file analysis, helpdesk reports |
| Recommended Fix | Implement Two-Factor Authentication (2FA) on admin accounts |

---

## Files in This Repository

| File | Description |
|---|---|
| `README.md` | Project overview, scenario, findings, and remediation summary |
| `security-incident-report.md` | Completed Security Incident Report (Sections 1–3) |

---

## Skills Demonstrated

- Network protocol analysis (DNS, HTTP, TCP/IP model)
- tcpdump log interpretation
- Security incident documentation
- Brute force attack identification
- OS hardening and remediation recommendations
- Cybersecurity report writing

---

## Course Context

This activity is part of the **Google Cybersecurity Professional Certificate** on Coursera, under the DICT Sector D Google Learning Program. It is designed to simulate real-world cybersecurity analyst tasks including log analysis, incident documentation, and recommending security controls.
