# 🔍 Apple CheckEngine — Dynamic Host Scanning Utility

### **Overview**

Apple **CheckEngine** is a **self-service dynamic host scanning utility** used to identify and mitigate security vulnerabilities across Apple networked services.
It performs a series of **automated security checks** on hosts and provides detailed findings, severity rankings, and actionable remediation recommendations.

CheckEngine and **Checkers** (Apple’s static code analyzer) form the core of **Gatehouse** — Apple Information Security’s self-service security toolkit for engineering teams.

---

## **Purpose**

Use CheckEngine to:

* Proactively identify **insecure configurations**, **exposed ports**, and **vulnerable services**.
* Assess hosts during the **software development lifecycle (SDLC)**.
* Meet **Gatehouse Check-in** security validation requirements.

CheckEngine can be used standalone or integrated into **Gatehouse** for comprehensive security posture analysis.

---

## **Key Features**

* **Dynamic Host Scanning**

  * Performs automated network checks across Apple-owned hosts.
* **Custom Scan Templates**

  * Run selective checks relevant to your service.
* **Detailed Findings**

  * Includes severity levels, remediation guidance, and port-specific issue tracking.
* **API Token Generation**

  * Enables automated scans using REST or GraphQL APIs.
* **GraphQL API Compatibility**

  * Integrates with internal automation tools.
* **Check Wizard**

  * Allows teams to submit **custom Python-based checks** for inclusion in CheckEngine’s suite.

---

## **Supported Domains & Ports**

### **Supported Domains**

CheckEngine is restricted to **Apple-owned domains** only.
It cannot scan:
* Third-party domains
* IP addresses (even if they belong to Apple’s internal network)

Allowed domains are listed at:
👉 [Allowed Domains](https://check-engine.apple.com/allowed_domains)

---

### **Scanned Ports**

CheckEngine scans a comprehensive set of **TCP ports** associated with Apple networked services.
Reference the official JSON list here:
👉 [Port List JSON](https://infosec.apple.com/content/dam/infosec/us/en_us/document/check_engine_ports.json)

---

## **Using CheckEngine**

### **Before You Begin**

Ensure:

* You are scanning **Apple-owned** hosts only.
* Hosts are **reachable and online**.
* You have **explicit authorization** to perform the scan.

---

### **Starting a Scan**

There are two main ways to launch a scan:

#### **1. Quick Setup Scan**

1. Log in to [CheckEngine](https://check-engine.apple.com/)
2. Select a **Scan Template** (or keep **Default**)
3. Enter one or more hostnames (comma-separated)
4. Click **Scan Hosts**

---

#### **2. Advanced Scan**

Accessed via the **“Advanced Scan”** option.

**Options for adding hosts:**

##### a) **Manual Entry**

* Enter one or more hostnames directly.
* Optionally, specify custom **ports** to target.
* You can add multiple hosts via the **“+” button**.

> Specifying ports limits results to those ports only (you can later adjust filters in the results view).

---

##### b) **CSV Upload**

* Upload a `.csv` file containing hosts and ports.
* A downloadable **CSV template** is provided on-screen.
* Maximum **300 hosts per scan** (files exceeding this limit are rejected).

---

##### c) **Saved Host Lists**

* Save and reuse frequently scanned host lists.
* Combine saved hosts with manual or CSV entries.

Once your host list is ready, click **“Scan Hosts”** to begin.

---

## **Reading Scan Results**

After a scan completes, the **Scans page** displays results.

### **For Each Finding**

* **Check name:** Which rule or test was triggered
* **Port:** Port number where issue was found
* **Severity:** From **Critical → Informational**
* **Blocking Status:** Whether the issue blocks Gatehouse Check-in
* **Description:** Details of the vulnerability or misconfiguration
* **Remediation:** Recommended actions to fix the issue

---

### **Severity Ratings**

| Severity       | Action Required         | Example                      |
| -------------- | ----------------------- | ---------------------------- |
| **Critical**   | Immediate fix required  | Exposed admin port           |
| **High**       | Fix as soon as possible | Unencrypted service endpoint |
| **Medium**     | Address in next sprint  | Missing security headers     |
| **Low / Info** | Recommended improvement | Deprecated TLS version       |

Learn more: [Security Policy Guidelines](https://infosec.apple.com/apply-security-requirements/policies.html)

---

## **Custom Templates**

You can create reusable **scan templates** to focus only on specific checks (e.g., TLS, DNS, SSH).
Templates can be defined in the **Template Management** section of CheckEngine.

Each template can:

* Define port ranges
* Include or exclude certain protocols
* Combine built-in and custom Python checks via **Check Wizard**

---

## **Check Wizard**

**Check Wizard** allows you to:

* Upload **third-party Python scripts** as custom checks
* Extend CheckEngine with domain-specific or service-specific scans
* Submit requests for inclusion in the central **Check Suite**

> All submitted checks undergo InfoSec validation before inclusion.

---

## **API & Automation**

### **API Token Generation**

* Access tokens via: [CheckEngine Token Portal](https://check-engine.apple.com/user_token)
* Use tokens to authenticate **GraphQL API** queries.

### **GraphQL API Documentation**

Full schema and usage examples:
👉 [GraphQL Docs](https://check-engine.apple.com/graphql_api_docs)

This API allows automation for:

* Triggering scans
* Fetching results
* Integrating with CI/CD or Gatehouse

---

## **Common Issues**

| Problem                 | Cause                                      | Resolution                                                                         |
| ----------------------- | ------------------------------------------ | ---------------------------------------------------------------------------------- |
| Cannot add host         | Host not Apple-owned                       | Verify domain in [Allowed Domains](https://check-engine.apple.com/allowed_domains) |
| Scan fails or times out | Host unreachable                           | Ensure host is online and accessible                                               |
| IP scans not working    | CheckEngine doesn’t support IP-based scans | Use domain names instead                                                           |
| Missing results         | Ports not included in scan template        | Add desired ports manually or edit template                                        |

If issues persist, reach out to **AskInfoSec**.

---

## **Integration with Gatehouse**

CheckEngine complements **Checkers** (SAST) in Apple’s **Gatehouse** framework:

| Tool            | Type                    | Purpose                                         |
| --------------- | ----------------------- | ----------------------------------------------- |
| **Checkers**    | Static (code-level)     | Detects insecure coding patterns                |
| **CheckEngine** | Dynamic (network-level) | Detects insecure network/service configurations |

Running both ensures complete **application and infrastructure security validation** before Check-in.
