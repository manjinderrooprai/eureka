### 🔍 **NFRs – Non-Functional Requirements**

These are requirements that define **how** a system performs rather than **what** it does. They are critical to ensure the **quality**, **scalability**, **security**, and **usability** of the system.

Common NFRs include:

* **Performance**
* **Security**
* **Scalability**
* **Reliability**
* **Maintainability**
* **Usability**

---

### 🛡️ **SAST – Static Application Security Testing**

* Also known as **white-box testing**.
* It analyzes your **source code or binaries** for security vulnerabilities **without executing** the program.
* Helps identify issues like:

  * SQL injection
  * Cross-site scripting (XSS)
  * Insecure code patterns
* Tools: **SonarQube, Fortify, Checkmarx, Veracode, CodeQL**

**Example**: Running a SAST scan on your Java codebase before deploying to catch insecure coding practices early.

### 🔓 **DAST – Dynamic Application Security Testing**

* Also known as **black-box testing**.
* It analyzes the **running application** for security vulnerabilities **at runtime**.
* Simulates real-world attacks like:

  * Broken authentication
  * Input validation flaws
  * Security misconfigurations
* Tools: **OWASP ZAP, Burp Suite, Netsparker**

**Example**: Running DAST tests against your deployed staging environment to see if it can be hacked from outside.

### 🚀 **Performance Benchmarking**

* Measures how your application **performs under various conditions** (load, stress, concurrency).
* Helps determine:

  * Response time
  * Throughput
  * Resource usage (CPU, memory, etc.)
* Tools: **JMeter, Gatling, Locust, k6**

**Example**: Simulating 5000 concurrent users to test if your app still responds within acceptable time limits.

### Summary Table:

| NFR Area                     | What it Checks                                | Tools                 |
| ---------------------------- | --------------------------------------------- | --------------------- |
| **SAST**                     | Code-level security flaws (before deployment) | SonarQube, Fortify    |
| **DAST**                     | Runtime vulnerabilities (after deployment)    | OWASP ZAP, Burp Suite |
| **Performance Benchmarking** | App speed, load handling, resource usage      | JMeter, k6            |

Here's a **comprehensive and detailed breakdown** of the NFRs you're expected to pick up — **SAST**, **DAST**, and **Performance Benchmarking** — including **tools, features, and examples**.

---

## 🔍 1. **Non-Functional Requirements (NFRs)** – Overview

NFRs focus on **how** a system behaves rather than **what** it does. While functional requirements specify *what* features a system must offer, NFRs define *constraints* and *quality attributes* like performance, security, scalability, etc.

You’re expected to focus on 3 critical NFRs:

* ✅ **SAST** – Secure code before deployment
* ✅ **DAST** – Detect vulnerabilities in running apps
* ✅ **Performance Benchmarking** – Ensure responsiveness and scalability

---
## 🛡️ 2. **SAST – Static Application Security Testing**

### 📌 What it is:

SAST tools scan **source code**, bytecode, or binaries **without running the application** to detect **insecure coding practices** early in the SDLC.

### 🎯 Key Features:

* Code vulnerability detection (SQLi, XSS, etc.)
* Early detection (before deployment)
* IDE or CI/CD integration
* Language-specific rule sets

### 🛠️ Common SAST Tools (with key features):

| Tool                                   | Features                                          | Example Usage                                            |
| -------------------------------------- | ------------------------------------------------- | -------------------------------------------------------- |
| **SonarQube**                          | Code quality, bug detection, security hotspots    | Scan your Java backend project during CI build           |
| **Fortify SCA (Static Code Analyzer)** | Deep static analysis, supports multiple languages | Enterprise-grade security scans in Jenkins               |
| **Checkmarx**                          | Customizable rules, IDE integration               | Enforce security rules in developer IDE                  |
| **Veracode Static Analysis**           | SaaS-based scans with rich dashboards             | Centralized security governance for large codebases      |
| **CodeQL (by GitHub)**                 | Semantic analysis queries, open-source support    | Run security checks on GitHub PRs using CodeQL Actions   |
| **Coverity**                           | High-precision defect detection                   | CI integration to catch memory leaks, concurrency issues |
| **Klocwork**                           | Detects complex security issues in C/C++          | Used in embedded systems for security auditing           |
| **FindSecBugs (plugin for SpotBugs)**  | Security plugin for Java                          | Detect hardcoded credentials, XSS, insecure random usage |
| **Reshift Security**                   | Dev-first JavaScript/Node SAST tool               | Integrate SAST in frontend CI pipelines                  |
| **RIPS Technologies**                  | PHP-specific SAST (now part of SonarSource)       | Secure PHP legacy codebases                              |

---
## 🔓 3. **DAST – Dynamic Application Security Testing**

### 📌 What it is:

DAST tools **test a live, running application** to find security vulnerabilities **from the outside**, like a hacker would. This happens **after deployment**, usually in staging/pre-prod environments.

### 🎯 Key Features:

* No access to source code needed
* Simulates real-world attacks (e.g., XSS, SQLi)
* Scans API endpoints or web interfaces
* Easy to integrate into CI/CD

### 🛠️ Common DAST Tools (with key features):
| Tool                          | Features                                     | Example Usage                                         |
| ----------------------------- | -------------------------------------------- | ----------------------------------------------------- |
| **OWASP ZAP**                 | Free, open-source, API scanning, spidering   | Schedule scans against staging URLs after CI deploy   |
| **Burp Suite (Professional)** | Manual & automated scanning, intercept proxy | Use to test login flows, session handling, XSS        |
| **Acunetix**                  | Fast scans, support for modern JS apps       | Scan single-page React/Angular apps                   |
| **Netsparker**                | Self-learning crawler, SQLi/XSS detection    | Automated DAST in CI pipelines                        |
| **Qualys Web App Scanning**   | Cloud-based scalable DAST                    | Scan multiple apps across environments centrally      |
| **AppScan (IBM)**             | Enterprise-grade tool, detailed dashboards   | Governance and regulatory compliance (HIPAA, PCI-DSS) |
| **Rapid7 InsightAppSec**      | Modern UI, cloud-based, reports integration  | Visualize risk exposure across applications           |
| **Tinfoil Security**          | Dev-focused scanning with CI/CD support      | Lightweight DAST for small-to-mid-sized teams         |
| **StackHawk**                 | Designed for developers, API scanning        | Run API security scans as part of CI build            |

---

## 🚀 4. **Performance Benchmarking**

### 📌 What it is:

Performance benchmarking ensures your application meets **speed, responsiveness, and scalability expectations** under different conditions.

### 🎯 Key Metrics:

* Response time (latency)
* Throughput (requests/sec)
* Error rate
* CPU/Memory usage
* Scalability under load

### 🛠️ Performance Testing Tools (with use cases):

| Tool                    | Features                                    | Example Usage                                        |
| ----------------------- | ------------------------------------------- | ---------------------------------------------------- |
| **Apache JMeter**       | Simulate heavy load on APIs/web apps        | Run 500 concurrent user simulation test              |
| **k6**                  | JavaScript-based scripting, CI/CD-ready     | Performance test REST APIs as part of GitHub Actions |
| **Gatling**             | Scala-based DSL for advanced load scenarios | Automate tests for login and checkout flows          |
| **Locust**              | Python-based, scalable via multiple users   | Define test flows using Python code                  |
| **Artillery**           | Lightweight, YAML/JS config, CI-friendly    | Performance test GraphQL endpoints                   |
| **BlazeMeter**          | SaaS platform built on JMeter               | Run distributed load tests with reports              |
| **NeoLoad (Tricentis)** | Advanced analytics, test reuse              | Enterprise performance testing across projects       |
| **WebLOAD**             | JavaScript scripting, cloud execution       | Measure response time for AJAX-heavy apps            |
| **LoadNinja**           | Real-browser testing, minimal scripting     | Measure frontend performance of single-page apps     |
| **Boomerang (Yahoo)**   | JS library for real-user monitoring         | Collect page load and user timing data in real time  |
---

## 🔄 Putting It Together – Example in DevSecOps

| Phase                     | Tool Category                            | Example Tools        | Description                                     |
| ------------------------- | ---------------------------------------- | -------------------- | ----------------------------------------------- |
| **Pre-Commit / Dev**      | SAST                                     | SonarQube, Checkmarx | Scan code in IDE or before merge                |
| **CI/CD Pipeline**        | SAST + DAST                              | CodeQL + OWASP ZAP   | Run security checks before and after deployment |
| **Pre-Prod Load Test**    | Performance                              | JMeter, k6           | Validate app performance under load             |
| **Production Monitoring** | Performance + Real User Monitoring (RUM) | New Relic, Dynatrace | Continuously monitor app behavior in production |

---

## 📝 Suggested Action Plan for You (Next 3 Months)

| Week  | Focus Area  | Activity                                                |
| ----- | ----------- | ------------------------------------------------------- |
| 1-2   | SAST        | Set up SonarQube in your local project and Jenkins      |
| 3-4   | DAST        | Learn OWASP ZAP and run against your dev/staging app    |
| 5-6   | Performance | Build a JMeter test for one of your APIs                |
| 7-8   | Deep Dive   | Learn CI/CD integration for all 3 tools                 |
| 9-10  | Benchmark   | Compare results across test runs and tune thresholds    |
| 11-12 | Showcase    | Document your work and prepare a demo/report for review |

---

## 🧭 Step 1: Understand What’s Expected

Your feedback highlights 3 clear **Non-Functional Requirement (NFR)** areas to strengthen before your ST (Senior Technologist / Specialist Technologist) movement:

| Focus Area                                      | Meaning                                                                                   | Why It’s Critical for ST Role                                                     |
| ----------------------------------------------- | ----------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------- |
| **SAST (Static Application Security Testing)**  | Analyzes source code for security vulnerabilities early in development                    | STs are expected to integrate security in SDLC and ensure secure coding practices |
| **DAST (Dynamic Application Security Testing)** | Tests running applications for vulnerabilities                                            | Ensures systems remain secure post-deployment                                     |
| **Performance Benchmarking**                    | Evaluating system performance (load, response time, scalability) under various conditions | STs must ensure applications are performant, scalable, and stable in production   |

---

## 🗓 Step 2: 3-Month Development Plan

Here’s a **structured roadmap** you can present to your manager/panel:

### **Month 1 – Foundation & Tool Familiarity**

**Goal:** Understand NFR principles and set up basic tools.

* 📘 Learn key concepts of SAST, DAST, and performance testing.
* 🧩 Tools to explore:

  * **SAST:** SonarQube, Checkmarx, GitHub Advanced Security
  * **DAST:** OWASP ZAP, Burp Suite
  * **Performance:** JMeter, k6, Gatling
* 🛠 Hands-on: Set up a sample app and perform a basic scan using SonarQube (SAST) and ZAP (DAST).

📄 **Deliverable:** Short summary/report comparing vulnerabilities identified via SAST and DAST.

---

### **Month 2 – Deep Dive & Project Application**

**Goal:** Apply learnings to a real or internal project.

* Integrate SAST tool (e.g., SonarQube) in CI/CD pipeline.
* Conduct DAST on staging or lower environment and document findings.
* Start defining **performance KPIs** (response time, throughput, error rate).
* Conduct **baseline performance test** with JMeter/k6.

📄 **Deliverable:**

* Security test results with remediation plan.
* Performance test report with metrics & recommendations.

---

### **Month 3 – Benchmarking & Knowledge Sharing**

**Goal:** Demonstrate leadership & readiness for ST responsibilities.

* Create a **performance benchmark document** for your team/project.
* Host a **mini knowledge session** for peers on SAST/DAST best practices.
* Document a **security and performance checklist** for new applications.
* Align with the ST panel or your manager for a readiness review.

📄 **Deliverable:** Knowledge session slides + benchmark report + checklist.

---

## 🧠 Step 3: Talking Points for the Follow-Up Discussion

When you meet your manager or the panel again, you can frame your conversation like this:

> “Thank you for the constructive feedback from the SP-ST gating discussion. I’ve created a focused 3-month plan to strengthen my understanding and hands-on experience in NFR areas—SAST, DAST, and Performance Benchmarking.
>
> * In the first month, I’ll build strong conceptual and tool-level knowledge using SonarQube, ZAP, and JMeter.
> * In the second, I’ll apply these in my project setup to generate tangible reports.
> * By the third, I aim to create a benchmark and conduct a team knowledge-sharing session.
>
> I’d appreciate periodic check-ins or mentorship on real project scenarios to ensure I’m aligned with ST expectations.”

This shows ownership, clarity, and initiative—exactly what panels look for in ST candidates.
