# Fortify — Application Security Testing Platform

### Overview

Fortify is a commercial suite of application security testing (AST) tools that provides static, dynamic and interactive security testing of applications, APIs, web/mobile back-ends and infrastructure. It enables organisations to discover, prioritise and remediate security vulnerabilities in applications across the software development lifecycle (SDLC) . ([DevOps School][1])

---

### History & Evolution

* The product traces back to Fortify Software (founded 2003) which produced SAST tools. ([Wikipedia][2])
* It was acquired by HP (Hewlett Packard) then later Micro Focus. ([Wikipedia][2])
* Now part of OpenText’s portfolio of application security solutions. ([OpenText][3])
* Over time it has expanded from SAST to include DAST, SCA (software composition analysis) and full AppSec program management. ([curatepartners.com][4])

---

### Editions & Technology Types

Fortify supports multiple editions and supports multiple testing technologies:

**Testing technologies supported:**

* SAST (Static Application Security Testing) — analyse source or compiled code for vulnerabilities. ([DevOps School][1])
* DAST (Dynamic Application Security Testing) — analyse running applications (web APIs etc). ([OpenText][5])
* IAST (Interactive Application Security Testing) — monitoring of running application with instrumentation/agent inside (some offerings). ([curatepartners.com][4])
* SCA (Software Composition Analysis) — identify open source/third-party components with known vulnerabilities. ([static.carahsoft.com][6])

**Key Editions:**

* Fortify SAST: (Static Code Analyzer) for source code scanning. ([OpenText][7])
* Fortify DAST: dynamic scanning (also branded under OpenText DAST) for web & APIs. ([OpenText][5])
* Fortify Software Security Center (SSC): management platform for scan results, program governance. ([OpenText][8])
* Fortify On Demand (FoD): SaaS AppSec-as-a-service version. ([OpenText][9])

---

### Use-Cases

The typical use-cases for Fortify include:

1. **Web application vulnerability scanning** – Finding issues like SQL injection, XSS, CSRF in web apps and APIs. ([curatepartners.com][4])
2. **Static code security analysis** – Early detection of insecure coding patterns, logic vulnerabilities before deployment. ([DevOps School][1])
3. **API security testing** – Analyse RESTful, SOAP APIs for vulnerabilities (via DAST modules) ([OpenText][5])
4. **Mobile backend / Web service testing** – Evaluate security for mobile app backends, microservices. ([OpenText][10])
5. **Compliance & governance** – Providing reporting capabilities for regulatory frameworks (OWASP Top 10, PCI DSS, HIPAA etc) ([OpenText][5])
6. **DevSecOps integration** – Integrate security scanning early in CI/CD pipelines (“shift left”), monitor change, prioritise high risk. ([OpenText][3])

---

### Key Features

* Automated crawl & scanning engine for web applications (dynamic) ([OpenText][5])
* Incremental scanning, agent instrumentation support (IAST) ([curatepartners.com][4])
* Centralised governance, dashboards, prioritisation of vulnerabilities ([OpenText][8])
* Broad language/framework support (many languages, many APIs) ([OpenText][3])
* Integration with CI/CD, IDEs, issue trackers for developer feedback loops ([OpenText][7])
* SaaS and on-premises deployment options for flexible infrastructure choices ([OpenText][9])

---

### When & Why to Use Fortify

* When you need a **commercial grade, enterprise AST platform** that supports multiple modalities (SAST + DAST + SCA).
* When you have compliance requirements and need reporting/governance across many applications.
* When you want to integrate security scanning into your DevOps pipeline and manage high volume of assets.
* When you require both code-level analysis **and** runtime/contextual security behaviour analysis.

---

### High-Level Architecture & Setup Notes

* The setup often includes a scanner component (for SAST) that runs on code repositories, builds or CI environments.
* A central management server (SSC) that aggregates results, dashboards, policies. ([OpenText][11])
* DAST components that test live applications, web interfaces, APIs.
* Integration into CI/CD pipelines (Jenkins, Azure DevOps, etc) for automation.
* Deployment: on-premise, cloud, or hybrid depending on enterprise requirements.
* Setup considerations: define which technologies to scan, authentication/authorization, asset inventory, scanning schedule, alerting workflows.

---

### Strengths & Considerations

**Strengths:**

* Broad coverage (languages + frameworks) with enterprise capabilities.
* Strong governance, reporting and compliance support.
* Mature product with many large enterprise customers. ([static.carahsoft.com][6])

**Considerations:**

* Commercial licensing cost (not free).
* Setup/configuration can be complex and may require tuning to reduce false positives.
* Some users report older versions had usability or performance issues. ([Medium][12])

---

# 🧠 Fortify — Application Security Testing Platform

### **Overview**

**Fortify**, developed by **OpenText** (formerly Micro Focus / HP Enterprise Security), is a **comprehensive Application Security Testing (AST)** suite designed to help organizations **identify, prioritize, and remediate security vulnerabilities** in software applications throughout the **Software Development Lifecycle (SDLC)**.

Fortify offers **Static (SAST)**, **Dynamic (DAST)**, **Software Composition (SCA)**, and **Cloud-based (FoD)** testing capabilities, supporting modern **DevSecOps** workflows and compliance frameworks like **OWASP Top 10, PCI DSS, NIST, HIPAA**, and **GDPR**.

---

## 🧩 Core Modules & Architecture

| **Module**                                 | **Type**           | **Purpose**                                                                  |
| ------------------------------------------ | ------------------ | ---------------------------------------------------------------------------- |
| **Fortify Static Code Analyzer (SCA)**     | SAST               | Analyzes source or compiled code to detect vulnerabilities before runtime.   |
| **Fortify WebInspect (DAST)**              | DAST               | Scans live web applications and APIs dynamically for exploitable flaws.      |
| **Fortify Software Security Center (SSC)** | Management Console | Centralized dashboard for scan results, policies, reporting, and governance. |
| **Fortify on Demand (FoD)**                | SaaS / Cloud       | Cloud-hosted version offering SAST, DAST, and SCA as a managed service.      |
| **Fortify Audit Workbench**                | Developer Tool     | GUI tool for manual review, triage, and remediation guidance.                |

---

## ⚙️ Key Features

### **1. Static Application Security Testing (SAST)**

* Scans source code, bytecode, or binaries for security weaknesses.
* Supports 30+ languages (Java, C#, Python, JavaScript, Go, etc.)
* Detects vulnerabilities like:

  * SQL Injection
  * Cross-site scripting (XSS)
  * Insecure deserialization
  * Hardcoded credentials
* Integrates directly with IDEs (Eclipse, IntelliJ, Visual Studio).

### **2. Dynamic Application Security Testing (DAST)**

* Black-box testing for web and API endpoints.
* Simulates real-world attacks during runtime.
* Detects authentication, session, and input validation issues.
* Supports crawling & scanning of web apps, REST/SOAP APIs.

### **3. Software Composition Analysis (SCA)**

* Detects vulnerabilities in open-source dependencies.
* Identifies license risks and outdated libraries.
* Integrates with build systems like Maven, Gradle, npm.

### **4. Centralized Governance with SSC**

* Unified dashboard to manage results from multiple scans.
* Custom policies, role-based access, and quality gates.
* Integration with Jira, ServiceNow, and other ticketing systems.

### **5. DevSecOps Integration**

* Jenkins, GitHub Actions, Azure DevOps, GitLab CI/CD, Bamboo.
* REST APIs for automation and reporting.
* Pre-build and post-build scan triggers.
* “Shift-Left” strategy—catch vulnerabilities early in the pipeline.

---

## 🧰 Supported Languages & Frameworks

Fortify supports a wide range of languages and frameworks including:

* **Web**: Java, JavaScript, TypeScript, PHP, Python, Ruby, .NET, Go.
* **Mobile**: Android (Java/Kotlin), iOS (Swift/Objective-C).
* **API**: REST, SOAP, GraphQL.
* **Infrastructure as Code (IaC)**: YAML, Dockerfiles, Terraform (via SCA).

---

## 🚀 Installation & Setup

### **1. Prerequisites**

| Requirement | Recommendation                   |
| ----------- | -------------------------------- |
| OS          | Windows Server, Linux, macOS     |
| Java        | JDK 11+                          |
| Database    | PostgreSQL or SQL Server for SSC |
| Memory      | 4–8 GB RAM minimum               |
| User        | Non-root user recommended        |

---

### **2. Installing Fortify Static Code Analyzer (SCA)**

```bash
# Extract installer
tar -xvf Fortify_SCA_and_Apps_<version>.tar.gz
cd FortifySCAAndApps

# Run installer
./install.sh
```

Verify:

```bash
sourceanalyzer -version
```

---

### **3. Running a Static Scan**

Example for Java code:

```bash
# Step 1: Translate source code
sourceanalyzer -b myproject src/**/*.java

# Step 2: Scan translated code
sourceanalyzer -b myproject -scan -f results.fpr
```

Open results in **Audit Workbench**:

```bash
auditworkbench results.fpr
```

---

### **4. Fortify Software Security Center (SSC) Setup**

1. Install and configure a web server (Tomcat recommended).
2. Deploy SSC WAR file.
3. Connect SSC to the database (PostgreSQL/MySQL).
4. Upload `.fpr` files from SCA or WebInspect for aggregation.
5. Access dashboard:
   `http://<server>:8080/ssc`

---

### **5. Fortify on Demand (FoD) Setup**

For SaaS users:

* Sign in at: [https://portal.fortify.com](https://portal.fortify.com)
* Upload code or configure CI pipeline.
* Retrieve API token for automation.
* Review findings and reports in FoD dashboard.

---

## 🔗 Jenkins Integration

### **1. Install Fortify Plugin**

* Go to **Manage Jenkins → Plugins → Available Plugins**
* Search for **Fortify Plugin** → Install → Restart Jenkins.

### **2. Configure Fortify Tools**

**Global Tool Configuration → Fortify Installation**

* Add name: `Fortify_SCA`
* Path to `sourceanalyzer` binary.

### **3. Jenkins Pipeline Example**

```groovy
pipeline {
    agent any

    tools {
        jdk 'jdk-11'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/example/repo.git'
            }
        }

        stage('Static Scan') {
            steps {
                sh 'sourceanalyzer -b appscan src/**/*.java'
                sh 'sourceanalyzer -b appscan -scan -f results.fpr'
            }
        }

        stage('Upload to SSC') {
            steps {
                sh 'fortifyclient uploadFPR -url http://localhost:8080/ssc -authtoken <token> -file results.fpr -project "MyProject" -version 1.0'
            }
        }
    }
}
```

---

## 📊 Interpreting Results

| **Metric**                         | **Description**                                                     |
| ---------------------------------- | ------------------------------------------------------------------- |
| **Critical / High / Medium / Low** | Severity rating of detected issues.                                 |
| **Kingdom**                        | Category of vulnerability (e.g., Input Validation, Authentication). |
| **Confidence Level**               | Likelihood that the finding is accurate.                            |
| **Remediation Guidance**           | Steps to fix the vulnerability with code samples.                   |

Reports can be exported in:

* HTML / PDF
* XML / CSV
* Upload to SSC dashboard

---

## 🧠 Best Practices

1. **Integrate Early** — run SAST scans during pull requests or pre-merge.
2. **Automate DAST** — scan staging environments before release.
3. **Baseline Scans** — maintain a clean baseline to compare new findings.
4. **Triage False Positives** — use Audit Workbench for manual review.
5. **Combine with SCA** — ensure dependency security and license compliance.
6. **Regularly Update Rules** — keep rulepacks up to date with new CVEs.

---

## 🔐 Security & Compliance

* Supports **OWASP Top 10**, **CWE**, **SANS 25**, **NIST 800-53** standards.
* Helps maintain compliance for **PCI DSS**, **GDPR**, **HIPAA**, **ISO 27001**.
* Encrypted communication (HTTPS) for SSC & FoD connections.
* Role-based access controls and audit logs for traceability.

---

## 🧩 Fortify vs. Other Tools

| **Feature**          | **Fortify**                          | **SonarQube**                  | **AppScan**                     |
| -------------------- | ------------------------------------ | ------------------------------ | ------------------------------- |
| Ownership            | OpenText (formerly Micro Focus)      | SonarSource                    | HCL Software                    |
| Focus                | Enterprise-grade AST (SAST/DAST/SCA) | Code Quality & Maintainability | AppSec scanning with compliance |
| SAST                 | ✅                                    | ⚠️ Basic (via plugins)         | ✅                               |
| DAST                 | ✅ (WebInspect)                       | ❌                              | ✅                               |
| SCA                  | ✅                                    | ⚠️ Community plugins           | ✅                               |
| CI/CD Integration    | ✅                                    | ✅                              | ✅                               |
| Cloud Version        | Fortify on Demand                    | SonarCloud                     | AppScan on Cloud                |
| Compliance Reporting | Advanced                             | Moderate                       | Advanced                        |
| Best Fit For         | Enterprises with large portfolios    | Dev teams                      | Security compliance teams       |

---

## 📚 References

* [OpenText Fortify Official Site](https://www.opentext.com/products/fortify-on-demand)
* [Fortify Static Code Analyzer Docs](https://www.microfocus.com/en-us/products/static-code-analyzer-sast/overview)
* [Fortify Jenkins Plugin](https://plugins.jenkins.io/fortify/)
* [OWASP Top 10 Compliance Reference](https://owasp.org/www-project-top-ten/)
