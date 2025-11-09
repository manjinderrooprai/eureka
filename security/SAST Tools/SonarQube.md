# 🧠 SonarQube — Continuous Code Quality and Security Platform

### **Overview**

**SonarQube** is an open-source **static code analysis and code quality management** platform developed by **SonarSource**.
It continuously inspects code quality to detect:

* **Bugs**
* **Security vulnerabilities**
* **Code smells**
* **Duplications**
* **Test coverage gaps**

SonarQube supports **over 30 programming languages** and integrates seamlessly with **CI/CD pipelines** such as **Jenkins**, **GitHub Actions**, and **Azure DevOps**.
It helps enforce **clean code standards** across development teams.

---

## 🧩 **Core Components & Architecture**

| **Component**                   | **Description**                                                                  |
| ------------------------------- | -------------------------------------------------------------------------------- |
| **SonarQube Server**            | Central component hosting the web UI, database connection, and analysis results. |
| **Database (PostgreSQL/MySQL)** | Stores scan results, user data, quality profiles, and history.                   |
| **SonarScanner**                | CLI or plugin used to analyze project code and send results to the server.       |
| **Web UI**                      | Browser-based dashboard to review metrics, vulnerabilities, and trends.          |
| **Elasticsearch**               | Used internally by SonarQube for fast search and indexing.                       |
| **Quality Profiles & Gates**    | Rulesets and thresholds defining project health and release readiness.           |

---

## ⚙️ **Key Features**

* **Multi-language support** (Java, JavaScript, Python, C#, Go, PHP, etc.)
* **Security scanning (SAST)** — OWASP, CWE, and SANS compliant rules.
* **Code duplication detection**
* **Quality Gates** — automatic build pass/fail logic based on code quality metrics.
* **Pull Request decoration** — integrates with GitHub, GitLab, Bitbucket, etc.
* **LDAP and token-based authentication**
* **Role-based access control (RBAC)**
* **Extensible via plugins** (Coverage, Dependency Check, etc.)

---

## 🚀 **SonarQube Installation and Setup (macOS/Linux)**

### **1. Prerequisites**

| Component      | Recommended Version                                 |
| -------------- | --------------------------------------------------- |
| **Java**       | 17 (Eclipse Adoptium / Temurin)                     |
| **PostgreSQL** | 14.x or later                                       |
| **Ports**      | Default `9000`, configurable via `sonar.properties` |
| **Memory**     | Minimum 2GB RAM                                     |
| **User**       | Non-root user recommended (e.g., `sonarqube`)       |

---

### **2. Install via tarball**

```bash
# Download and extract
wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-10.5.1.zip
unzip sonarqube-10.5.1.zip -d /opt/
mv /opt/sonarqube-10.5.1 /opt/sonarqube
```

---

### **3. Configure SonarQube**

Edit `/opt/sonarqube/conf/sonar.properties`:

```bash
# Network settings
sonar.web.host=127.0.0.1
sonar.web.port=9000

# Database
sonar.jdbc.username=sonar
sonar.jdbc.password=your_password
sonar.jdbc.url=jdbc:postgresql://localhost/sonarqube
```

---

### **4. Start SonarQube**

```bash
cd /opt/sonarqube/bin/macosx-universal-64
./sonar.sh start
```

Check logs:

```bash
tail -f /opt/sonarqube/logs/web.log
```

Access UI:
👉 [http://localhost:9000](http://localhost:9000)

**Default credentials:**

```
Username: admin
Password: admin
```

---

### **5. Change Default Port (Optional)**

Modify in `/opt/sonarqube/conf/sonar.properties`:

```bash
sonar.web.port=9002
```

Restart SonarQube:

```bash
./sonar.sh restart
```

---

### **6. Run as a Brew Service (macOS)**

To manage SonarQube via Homebrew:

```bash
brew services start sonarqube
brew services stop sonarqube
brew services list
```

If SonarQube is not installed via brew:
Create a **launchd service plist** manually:

```bash
sudo cp /opt/sonarqube/misc/macosx-universal-64/homebrew.mxcl.sonarqube.plist ~/Library/LaunchAgents/
launchctl load ~/Library/LaunchAgents/homebrew.mxcl.sonarqube.plist
```

---

## 🔍 **SonarScanner Setup**

### **1. Install Scanner**

```bash
brew install sonar-scanner
```

or download manually:

```bash
wget https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-5.0.1.zip
unzip sonar-scanner-cli-5.0.1.zip -d /opt/
export PATH=$PATH:/opt/sonar-scanner/bin
```

---

### **2. Verify Installation**

```bash
sonar-scanner -v
```

---

### **3. Run a Scan**

In your project directory:

```bash
sonar-scanner \
  -Dsonar.projectKey=my_project \
  -Dsonar.sources=src \
  -Dsonar.host.url=http://localhost:9000 \
  -Dsonar.login=your_token
```

> Generate your token from SonarQube UI → **My Account → Security → Tokens**

---

## 🧱 **Integrating SonarQube with Jenkins**

### **1. Prerequisites**

* Jenkins running (e.g., via `brew services start jenkins-lts`)
* SonarQube server up and reachable (e.g., `http://localhost:9000`)
* Jenkins has **Gradle** or **Maven** installed

---

### **2. Install SonarQube Plugin in Jenkins**

1. Go to **Manage Jenkins → Plugins → Available Plugins**
2. Search for **SonarQube Scanner for Jenkins**
3. Install and restart Jenkins

---

### **3. Configure Global SonarQube Server**

Go to **Manage Jenkins → Configure System → SonarQube Servers**

Add:

* **Name**: `Sonar-server`
* **Server URL**: `http://localhost:9000`
* **Server Authentication Token**: Paste token from SonarQube UI

---

### **4. Configure Sonar Scanner in Jenkins**

Go to **Manage Jenkins → Global Tool Configuration → SonarQube Scanner**

Add new installation:

* Name: `sonar-scanner`
* Path: `/Users/<your-username>/Library/Application Support/Jenkins/tools/hudson.plugins.sonar.SonarRunnerInstallation/sonar-scanner`

---

### **5. Jenkins Pipeline (Declarative Example)**

```groovy
pipeline {
    agent any

    tools {
        gradle 'gradle-8.4'
    }

    environment {
        SONARQUBE = credentials('sonar-token')
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/your-org/your-repo.git'
            }
        }

        stage('Build') {
            steps {
                sh './gradlew clean build -x test'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('Sonar-server') {
                    sh './gradlew sonarqube -x test'
                }
            }
        }

        stage('Quality Gate') {
            steps {
                timeout(time: 2, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}
```

---

### **6. Freestyle Project Configuration**

For simpler jobs:

* Add **Invoke Gradle Script** or **Execute Shell**
* Use task:

  ```bash
  gradle clean build sonarqube -x test \
    -Dsonar.projectKey=my_project \
    -Dsonar.host.url=http://localhost:9000 \
    -Dsonar.login=your_token
  ```
* Add **Post-build Action → SonarQube Scanner Analysis**

---

### **7. Troubleshooting Jenkins Integration**

| Error                                                                | Root Cause                              | Solution                                  |
| -------------------------------------------------------------------- | --------------------------------------- | ----------------------------------------- |
| `Cannot run program "gradle": No such file or directory`             | Gradle not configured in Jenkins        | Add Gradle in **Global Tool Config**      |
| `Unauthorized (401)`                                                 | Invalid or expired token                | Regenerate and update Jenkins credentials |
| `SonarScanner exited with code 3`                                    | Compilation failure or missing binaries | Ensure project builds before analysis     |
| `Your project contains .java files, please provide compiled classes` | Missing binaries path                   | Add `-Dsonar.java.binaries=build/classes` |

---

## 📊 **Understanding SonarQube Dashboard**

| Section            | Description                                                     |
| ------------------ | --------------------------------------------------------------- |
| **Overview**       | Project summary (lines of code, issues, maintainability rating) |
| **Issues Tab**     | Lists vulnerabilities, bugs, code smells                        |
| **Quality Gate**   | Pass/fail status based on thresholds                            |
| **Measures**       | Detailed metrics: coverage, duplications, complexity            |
| **Activity**       | Timeline of past scans and trends                               |
| **Administration** | Manage project-level settings, profiles, and permissions        |

---

## 🧠 **Best Practices**

1. **Integrate early** — run SonarQube analysis with every PR or CI build.
2. **Fix new issues immediately** — enforce “Clean as You Code” principle.
3. **Use Quality Gates** — define minimum thresholds for:

   * 0 new critical bugs
   * 80%+ code coverage
   * < 3% duplication
4. **Automate token refreshes** with Jenkins credentials.
5. **Regularly clean up** Sonar logs and database indexes to maintain performance.

---

## 🔐 **Security Considerations**

* Use **HTTPS** for SonarQube connections.
* Restrict access to **admin** dashboards.
* Rotate **tokens** periodically.
* Integrate with **LDAP** or **SSO** for centralized authentication.
* Regularly update SonarQube and plugins for latest security patches.

---

## 🧩 **Comparison with Apple Checkers**

| Feature             | SonarQube                             | Apple Checkers                          |
| ------------------- | ------------------------------------- | --------------------------------------- |
| Type                | Open-source SAST and quality analysis | Apple internal static analysis          |
| Scope               | Multi-language, extensible            | Security-focused for Apple environments |
| Deployment          | Self-hosted or SaaS                   | Apple internal only                     |
| Jenkins Integration | Native                                | Indirect (via scripts)                  |
| Use Case            | Code maintainability and compliance   | Security validation for Apple products  |

---

## 📚 **References**

* [SonarQube Official Documentation](https://docs.sonarsource.com/)
* [SonarScanner CLI](https://docs.sonarsource.com/sonarqube/latest/analyzing-source-code/scanners/sonarscanner/)
* [SonarQube Jenkins Plugin](https://plugins.jenkins.io/sonar/)
* [Quality Gate Best Practices](https://docs.sonarsource.com/sonarqube/latest/user-guide/quality-gates/)
