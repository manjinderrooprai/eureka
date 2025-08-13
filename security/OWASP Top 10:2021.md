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

### Key Changes from the 2017 List

OWASP introduced notable updates in the 2021 version:

* **Three New Categories Added**:

  * **Insecure Design (A04)**
  * **Software and Data Integrity Failures (A08)**
  * **Server-Side Request Forgery (SSRF) (A10)** 

* **Renamed or Broadened Categories**:

  * *Sensitive Data Exposure* → **Cryptographic Failures (A02)**
  * *Broken Authentication* → **Identification and Authentication Failures (A07)** 

* **Consolidated Categories**:

  * *Cross-Site Scripting (XSS)* is now part of **Injection (A03)**
  * *XML External Entities (XXE)* merged into **Security Misconfiguration (A05)**
  * *Insecure Deserialization* included under **Software and Data Integrity Failures (A08)**

## 1. Broken Access Control

<img width="856" height="448" alt="image" src="https://github.com/user-attachments/assets/f324743b-70f9-457e-b2df-45763ff04b64" />

**Websites have pages that are protected from regular visitors**. For example, **only the site's admin user should be able to access a page to manage other users**. **If a website visitor can access protected pages they are not meant to see, then the access controls are broken**.

#### A regular visitor being able to access protected pages can lead to the following:

- **Being able to view sensitive information from other users**
- **Accessing unauthorized functionality**

Simply put, **broken access control allows attackers to bypass authorisation**, allowing them to **view sensitive data** or **perform tasks they aren't supposed to**.

**For example**, a vulnerability was found in 2019, where an attacker could get any single frame from a Youtube video marked as private. The researcher who found the vulnerability showed that he could ask for several frames and somewhat reconstruct the video. Since the expectation from a user when marking a video as private would be that nobody had access to it, this was indeed accepted as a broken access control vulnerability.

#### Insecure Direct Object Reference

**IDOR or Insecure Direct Object Reference** refers to an **access control vulnerability** where you can access resources you wouldn't ordinarily be able to see. This **occurs when the programmer exposes a Direct Object Reference**, which is just an identifier that refers to specific objects within the server. **By object, we could mean a file, a user, a bank account in a banking application, or anything really**.

For example, let's say we're logging into our bank account, and after correctly authenticating ourselves, we get taken to a URL like this `https://bank.thm/account?id=111111`. On that page, we can see all our important bank details, and a user would do whatever they need to do and move along their way, thinking nothing is wrong.

<img width="805" height="364" alt="image" src="https://github.com/user-attachments/assets/7735001b-6747-4aca-a0b6-e1b237972fd1" />

There is, however, **a potentially huge problem here**, anyone may be able to change the `id` parameter to something else like `222222`, and if the site is incorrectly configured, then he would have access to someone else's bank information.

<img width="805" height="365" alt="image" src="https://github.com/user-attachments/assets/477e14a8-6e1a-4556-b086-ea38a152673b" />

The application exposes a direct object reference through the id parameter in the URL, which points to specific accounts. **Since the application isn't checking if the logged-in user owns the referenced account**, **an attacker can get sensitive information from other users because of the IDOR vulnerability**. Notice that **direct object references aren't the problem**, **but rather that the application doesn't validate if the logged-in user should have access to the requested account**.

#### Prevent Broken Access Control and IDOR:

* Enforce **server-side authorization checks** for every request.
* Verify **both authentication and authorization** before granting access.
* Use **unpredictable identifiers** (UUIDs, random IDs) instead of sequential numbers.
* Implement **Role-Based Access Control (RBAC)** or **Attribute-Based Access Control (ABAC)**.
* Apply the **principle of least privilege**.
* Validate access at all layers — controller, service, and database query level.
* Filter DB queries by **current user’s ownership**.
* Do **not rely on hidden UI elements** or client-side checks for security.
* **Centralize** access control logic in one place.
* Regularly perform **security testing** (manual, automated, penetration testing).

## 2. Cryptographic Failures
