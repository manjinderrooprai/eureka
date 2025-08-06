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
