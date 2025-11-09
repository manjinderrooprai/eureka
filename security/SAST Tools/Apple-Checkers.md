# 🧩 Apple Checkers — Static Code Analysis Platform

### **Overview**

Apple **Checkers** is a self-service **static code analysis tool** developed by Apple Information Security (InfoSec). It helps developers identify **security vulnerabilities early** in the software development lifecycle (SDLC).

It integrates seamlessly with **GitHub Enterprise**, **GitLab**, and **Bitbucket**, allowing engineers and assessors to scan repositories for potential issues in source code and configurations.

Checkers works as part of Apple’s internal **Gatehouse Security Toolkit**, alongside **CheckEngine**, providing both static and dynamic scanning capabilities.

---

## **Key Features**

* **Multi-language support** for static code analysis:

  * Elixir, Go, Java, JavaScript, PHP, Python, Perl, Ruby
* **Integrations**:

  * GitHub Enterprise, GitLab, Bitbucket (OAuth or Access Tokens)
* **Findings & Reporting**:

  * Detailed results categorized by severity
  * Grouped vulnerabilities with file, line, and fix suggestions
* **Live scan monitoring**
* **Administrator dashboards** for managing users and findings
* **Kubernetes YAML scanning** for misconfigurations

---

## **Core Scanners Included**

| **Scanner**              | **Purpose / Language**                     | **Version** |
| ------------------------ | ------------------------------------------ | ----------- |
| Bandit                   | Python security analyzer                   | v1.7.8      |
| Brakeman                 | Ruby on Rails security scanner             | latest      |
| BundlerAudit             | Ruby dependency vulnerabilities            | latest      |
| CargoAudit / CargoClippy | Rust security & linting                    | latest      |
| DawnScanner              | Ruby security auditing                     | latest      |
| DependencyTrack          | Dependency tracking & SBOM analysis        | v4.7.0      |
| Goldfinch                | Sensitive file & secret detection          | latest      |
| Gosec                    | Golang security analyzer                   | v2.22.0     |
| Infer                    | Static analyzer (Java, Objective-C, C)     | v1.2.0      |
| KICS                     | Kubernetes Infrastructure as Code checks   | v1.6.12     |
| NpmAudit                 | JavaScript / Node dependency audit         | latest      |
| PerlCritic               | Perl code quality                          | latest      |
| Semgrep                  | Universal SAST rule engine                 | v1.85.0     |
| ShellCheck               | Shell script analysis                      | v0.10.0     |
| Sobelow                  | Elixir security checks                     | latest      |
| **SonarQube**            | External integration (SAST / Code Quality) | v9.8        |

---

## **Supported Language Versions**

To ensure compatibility with Checkers scanning infrastructure:

| Language | Supported Versions                |
| -------- | --------------------------------- |
| Ruby     | 2.7.2, 3.3.0                      |
| Python   | 3.9.7, 3.11.0                     |
| Perl     | 5.36.0                            |
| NodeJS   | 18.20.4, 20.16.0, 22.5.1          |
| Java     | 1.8, 11.0, 17.0-apple, 21.0-apple |
| Elixir   | 11.15.7                           |
| Golang   | 1.22.5                            |
| PHP      | Version agnostic                  |

---

## **How to Use Checkers**

### **1. Authorization**

Before scanning, you must authorize Checkers to access your repositories.

#### GitHub:

* Go to **Checkers > Code Authorization**
* Click **Authorize**
* Approve the OAuth request for GitHub Enterprise

#### GitLab:

* Generate a **Personal Access Token** with:

  * `api` or `read_api` and `read_user` scopes
* Enter the token in Checkers and click **Save**

#### Bitbucket:

* Generate a token with **Project read permissions**
* Add it in the **Code Authorization** tab

> You can manage, refresh, or revoke authorizations anytime via your profile menu.

---

### **2. Integrate Checkers GitHub App (Optional)**

* Allows **event-driven scans** on Pull Requests (PRs)
* Automatically blocks PR merges if high-severity issues are found
* Displays results directly in GitHub (no need to visit Checkers)
* Scans up to **3,000 files per PR**

  * For larger PRs, use **“New Scan”** manually in Checkers

> Note: SonarQube scans are excluded from PR scans due to build compilation requirements.

---

### **3. Starting a Scan**

1. Navigate to **Checkers Home > New Scan**
2. Enter the **repository name or URL**
3. Choose the **branch** to analyze
4. Click **Scan**
5. Monitor progress in **Logs**
6. View detailed issues under the **Findings** tab once complete

---

## **Understanding Scan Results**

### **Findings Categories**

| Category               | Description                             |
| ---------------------- | --------------------------------------- |
| **Blocker**            | Must be fixed before Gatehouse Check-In |
| **Upcoming Blocker**   | Will soon become mandatory to fix       |
| **Highly Recommended** | Strongly advised (high confidence)      |
| **Uncategorized**      | Low accuracy or unreviewed findings     |

---

### **Severity Levels**

From **Max → Informational**, depending on risk impact.
Each finding includes:

* Description
* Affected file and line
* Number of occurrences
* Suggested remediation

---

### **Sharing & Collaboration**

You can share results by:

* **Downloading** as `.csv`
* **Copying the scan URL** (e.g., `https://checkers.apple.com/scans/<id>`)

---

### **Requesting a Review**

If you suspect a false positive:

1. Go to the **Findings** tab
2. Click **Request Review**
3. Select the issue → Choose a reason → Add comments
4. Click **Submit for Review**
5. InfoSec will review and respond via email or Radar

---

## **Configuration via `checkers.yml`**

Define language versions and build tasks by adding a **`checkers.yml`** file at the root of your repo.

### **Format:**

```yaml
tools:
  <language>:
    version: "<version>"
    task: "<build|package|install|compile|compileJava|compileScala>"  # Java only
    git: "<true|false>"  # Downloads .git directory if true
```

### **Example:**

```yaml
tools:
  java:
    version: "21.0-apple"
    task: build
    git: true
  nodejs:
    version: "20.8.1"
  ruby:
    version: "2.7.2"
```

This ensures Checkers uses the correct runtime and build environment for your project.

---

## **Best Practices**

* Always **commit your `checkers.yml`** for consistent language versioning.
* Address **Blocker** and **Upcoming Blocker** issues promptly.
* Re-run scans after updating dependencies or major code changes.
* Use **Checkers + Gatehouse** together for full security posture coverage.
