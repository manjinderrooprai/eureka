# OWASP Top 10:2017

This breaks each OWASP topic down and includes details on what the vulnerability is, how it occurs and how you can exploit it. You will put the theory into practise by completing supporting challenges.

- **Broken Access Control**
- **Cryptographic Failures**
- **Injection**
- **Insecure Design**
- **Security Misconfiguration**
- **Vulnerable and Outdated Components**
- **Identification and Authentication Failures**
- **Software and Data Integrity Failures**
- **Security Logging & Monitoring Failures**
- **Server-Side Request Forgery (SSRF)**

### 1. Broken Access Control

<img width="856" height="448" alt="image" src="https://github.com/user-attachments/assets/f324743b-70f9-457e-b2df-45763ff04b64" />

**Websites have pages that are protected from regular visitors**. For example, **only the site's admin user should be able to access a page to manage other users**. **If a website visitor can access protected pages they are not meant to see, then the access controls are broken**.

#### A regular visitor being able to access protected pages can lead to the following:

- **Being able to view sensitive information from other users**
- **Accessing unauthorized functionality**

Simply put, **broken access control allows attackers to bypass authorisation**, allowing them to **view sensitive data** or **perform tasks they aren't supposed to**.

**For example**, a vulnerability was found in 2019, where an attacker could get any single frame from a Youtube video marked as private. The researcher who found the vulnerability showed that he could ask for several frames and somewhat reconstruct the video. Since the expectation from a user when marking a video as private would be that nobody had access to it, this was indeed accepted as a broken access control vulnerability.
