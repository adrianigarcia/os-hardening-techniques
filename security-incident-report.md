# Security Incident Report

**Activity:** Apply OS Hardening Techniques
**Course:** Google Cybersecurity Professional Certificate — Course 3
**Platform:** Coursera (DICT Sector D Google Learning Program)
**Date Submitted:** July 12, 2026
**Grade:** 100%

---

## Section 1: Identify the Network Protocol Involved in the Incident

The network protocols identified in the tcpdump log during this investigation are **DNS (Domain Name System)** and **HTTP (Hypertext Transfer Protocol)**.

DNS was used when the browser sent requests to resolve the domain names `yummyrecipesforme.com` and `greatrecipesforme.com` into their corresponding IP addresses. HTTP was used when the browser sent GET requests to load the webpages and download the malicious executable file. Both protocols operate at the **Application Layer** of the TCP/IP model.

The traffic captured in the tcpdump log confirms that the browser initiated DNS queries, received IP address responses, and then made HTTP requests to those resolved addresses — first to `yummyrecipesforme.com` and subsequently to `greatrecipesforme.com` after the malware redirected the browser.

---

## Section 2: Document the Incident

### Incident Summary

On the date of investigation, `yummyrecipesforme.com` — a website that sells recipes and cookbooks — was compromised by a former employee acting as a malicious actor. The attacker executed a **brute force attack** against the website's administrative account by repeatedly entering known default passwords until the correct credentials were guessed. Once access to the admin panel was obtained, the attacker modified the website's source code to embed a **JavaScript function** that prompted all visiting users to download an executable file described as a browser update.

When users downloaded and ran the file, their browsers were automatically redirected from `yummyrecipesforme.com` to a malicious copycat website, `greatrecipesforme.com`, which contained malware. Visitors reported that after running the downloaded file, the website's address changed in their browsers and their computers began running more slowly — consistent with malware infection.

### How the Incident Was Discovered

The incident was first discovered when multiple customers contacted `yummyrecipesforme.com`'s helpdesk to report being prompted to download a file. The website owner attempted to log in to the admin panel to investigate but was unable to do so, as the attacker had changed the administrative password following the compromise. The website hosting provider was contacted, and a cybersecurity team was tasked with investigating.

### Investigation Findings (tcpdump Log Analysis)

During the investigation, a sandbox environment was used to safely replicate the attack. The network protocol analyzer `tcpdump` was run while loading `yummyrecipesforme.com`. The following sequence of events was observed and logged:

| Step | Event |
|------|-------|
| 1 | The browser sent a DNS request to resolve `yummyrecipesforme.com` |
| 2 | The DNS server returned the correct IP address for `yummyrecipesforme.com` |
| 3 | The browser made an HTTP GET request to load the `yummyrecipesforme.com` webpage |
| 4 | The website triggered an automatic download of a malicious executable file |
| 5 | The browser sent a DNS request to resolve `greatrecipesforme.com` |
| 6 | The DNS server returned the IP address for `greatrecipesforme.com` |
| 7 | The browser made an HTTP GET request to `greatrecipesforme.com` — the malicious site |

### Confirmation

A senior analyst confirmed that JavaScript code had been injected into the website's source code. Analysis of the downloaded file revealed a script designed to redirect users' browsers to `greatrecipesforme.com`. The cybersecurity team confirmed the root cause was a brute force attack that succeeded due to the use of a **default administrative password** and the **absence of any brute force protection controls**.

### Sources of Evidence

- tcpdump traffic log
- Website source code review
- Downloaded executable file analysis
- Customer helpdesk reports

---

## Section 3: Recommend One Remediation for Brute Force Attacks

### Recommendation: Implement Two-Factor Authentication (2FA) on All Administrative Accounts

Two-factor authentication (2FA) is an effective countermeasure against brute force attacks because it requires a second form of verification — such as a one-time code sent to a registered mobile device or email — in addition to a password.

**Why 2FA is effective:**

Even if a malicious actor successfully guesses or obtains the correct administrative password through a brute force attack, they would be unable to access the account without also possessing the second authentication factor. This significantly increases the difficulty of unauthorized access and reduces the risk of account compromise.

Implementing 2FA on the administrative account for `yummyrecipesforme.com` would have prevented the attacker from gaining access to the admin panel and modifying the website's source code, even after correctly guessing the default password.

**Additional recommended measures (supplementary):**

- Require strong, unique passwords for all accounts (no default passwords)
- Limit the number of failed login attempts (account lockout policy)
- Monitor and alert on unusual login activity
- Require regular password changes for privileged accounts

---

*This report was completed as part of the Google Cybersecurity Professional Certificate program on Coursera.*
