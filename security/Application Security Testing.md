# Application Security Testing (AST)

## 🧭 **1. What Is Application Security Testing (AST)?**

**Application Security Testing (AST)** refers to a **set of processes and tools** designed to **identify, fix, and prevent vulnerabilities** in software applications throughout the Software Development Life Cycle (SDLC).

👉 The goal:  

> Detect security flaws early — before attackers can exploit them in production.

It includes **static**, **dynamic**, **interactive**, and **runtime** testing approaches that together help ensure applications are **secure by design**.

---

## 🧩 **2. Major Types of Application Security Testing**

Let’s break down the key categories — these are the ones panelists usually expect you to know:

| Type                                                | When It Runs                       | What It Tests                       | Example Tools                                    | Common Findings                                                   |
| --------------------------------------------------- | ---------------------------------- | ----------------------------------- | ------------------------------------------------ | ----------------------------------------------------------------- |
| **SAST (Static Application Security Testing)**      | Before runtime (code-level)        | Source code, bytecode               | SonarQube, Checkmarx, Veracode, Fortify, Semgrep | Hardcoded secrets, SQL injection, XSS, unsafe API calls           |
| **DAST (Dynamic Application Security Testing)**     | During runtime (black-box testing) | Running web app endpoints           | OWASP ZAP, Burp Suite, AppScan, Netsparker       | Authentication flaws, input validation issues, misconfigurations  |
| **IAST (Interactive Application Security Testing)** | During runtime (hybrid)            | Uses instrumentation agents         | Contrast Security, Seeker                        | Combines SAST + DAST insights; detects contextual vulnerabilities |
| **RASP (Runtime Application Self-Protection)**      | In production                      | Application behavior in real time   | Imperva RASP, Signal Sciences                    | Protects against attacks live, logs events                        |
| **SCA (Software Composition Analysis)**             | Build time                         | Open-source dependencies, libraries | Snyk, Black Duck, OWASP Dependency-Check         | Outdated or vulnerable dependencies                               |
| **Penetration Testing**                             | Pre-production / periodic          | Entire system (manual + automated)  | Metasploit, Burp Suite Pro                       | Business logic flaws, chained exploits                            |
| **Fuzz Testing (Fuzzing)**                          | Automated runtime                  | Sends random/malformed inputs       | AFL, Peach Fuzzer                                | Input validation, buffer overflows                                |
| **Cloud Security Posture Testing**                  | Deployment & runtime               | Cloud configurations, permissions   | Prisma Cloud, Wiz                                | Misconfigurations in cloud workloads                              |

---

## ⚙️ **3. Application Security Testing Across SDLC**

| SDLC Phase       | Security Practice                               | Tool Type                      |
| ---------------- | ----------------------------------------------- | ------------------------------ |
| **Requirements** | Define security requirements (OWASP ASVS, NIST) | —                              |
| **Design**       | Threat modeling (STRIDE, DFD)                   | Microsoft Threat Modeling Tool |
| **Development**  | Secure coding, code reviews                     | SAST, SCA                      |
| **Testing / QA** | Functional + security tests                     | DAST, IAST                     |
| **Deployment**   | Security hardening, secrets management          | Infrastructure scanning        |
| **Operations**   | Continuous monitoring                           | RASP, SIEM integration         |

🧠 *Key takeaway:* Security is no longer a one-time test — it’s embedded in the DevSecOps pipeline.

---

## 🔐 **4. Why Application Security Testing Matters**

| Benefit                           | Impact                                      |
| --------------------------------- | ------------------------------------------- |
| **Early vulnerability detection** | Fix cheaper, prevent breaches early.        |
| **Regulatory compliance**         | Meets ISO 27001, PCI-DSS, SOC2, GDPR, etc.  |
| **Customer trust**                | Protects sensitive user and client data.    |
| **Business continuity**           | Reduces downtime due to security incidents. |
| **Developer empowerment**         | Promotes secure coding culture.             |

---

## 🧰 **5. Recommended Learning & Practice Plan**

Since you’re preparing for **ST-level expertise**, here’s a hands-on roadmap for Application Security Testing:

### **Month 1: Foundation**

* Study **OWASP Top 10** vulnerabilities (e.g., Injection, Broken Auth, SSRF).
* Learn SAST + DAST basics and how they differ.
* Tools: Install **SonarQube (SAST)** and **OWASP ZAP (DAST)** locally.

### **Month 2: Implementation**

* Run **SAST** on your project repo → fix identified code issues.
* Deploy a demo app (like Juice Shop or DVWA) → run **DAST** using OWASP ZAP.
* Document findings and mitigations.

### **Month 3: Integration & Reporting**

* Integrate both tools in a **CI/CD pipeline** (GitHub Actions or Jenkins).
* Learn to prioritize findings (false positives, severity levels).
* Create a **Security Testing Report Template** — a professional ST artifact.

---

## 🧾 **6. Talking Points for Your Review Panel**

You can confidently say something like:

> “I’ve strengthened my understanding of Application Security Testing holistically — covering SAST, DAST, and IAST. I’ve implemented SonarQube and OWASP ZAP for static and dynamic testing and explored how to embed these into CI/CD workflows to align with DevSecOps practices.
> My next goal is to extend this into performance benchmarking and create reusable test frameworks for consistent security validation.”
