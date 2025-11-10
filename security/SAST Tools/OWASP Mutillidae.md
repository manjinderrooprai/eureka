# OWASP Mutillidae II

![Image](https://www.researchgate.net/publication/330934873/figure/fig7/AS%3A723707437780993%401549556707302/Creating-an-account-in-Mutillidae.ppm)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1200/1%2AZHQoCbCMkfYbUlp03z9e8g.png)

![Image](https://opengraph.githubassets.com/60c7c543f67b099e15c8d970fa7ae59fce1e1e36a8479bf07685a2d2c0aa323b/webpwnized/mutillidae)

---

### What it is

* Mutillidae II is a free, open-source web application created as a **deliberately vulnerable** site. It’s meant to be a “target” environment for practising web application security testing. ([GitHub][1])
* It includes many different types of weaknesses (e.g., forms with SQL injection, cross-site scripting, file inclusion, web services with flaws) so you can test tools, training, CTFs (capture-the-flag style), labs, etc. ([GitHub][1])
* According to the repo, it contains “over 40 vulnerabilities and challenges, covering each of the OWASP Top Ten from 2007 to 2017.” ([GitHub][1])
* It is built in PHP (majority of code) with HTML/JavaScript front end. ([GitHub][1])
* It provides easy installation on Windows (WAMP/XAMPP), Linux (LAMP), and Docker images. ([GitHub][1])

---

### Use-Cases

Here are some practical use-cases where Mutillidae II can add value:

1. **Training / teaching**

   * If you are teaching web security (for example at a university, corporate training), you can deploy this app and have students intentionally find vulnerabilities, exploit them, learn mitigation.
   * Useful for security awareness training for developers: showing real broken things helps emphasise “what *can* go wrong”.

2. **Hands-on labs / workshops**

   * Workshops on penetration testing, web application security, red-teaming can use this as a lab target.
   * When you want a safe, controlled environment (i.e., not a live production app) to demonstrate attacks.

3. **CTF / Capture-the-Flag (CTF) style events**

   * You can set up challenges (“exploit this form”, “leverage this vulnerability”) around the pre-built vulnerabilities in Mutillidae.
   * Because it includes many known vulnerability types, it’s good for varied difficulty levels.

4. **Testing security tools / scanners**

   * If you have a web vulnerability scanner (automated tool), you can point it at Mutillidae and verify that the scanner picks up known flaws.
   * Helps validate tool coverage or train staff on using those tools.

5. **Developer practice / DevSecOps integration**

   * Developers can practise secure coding by fixing the intentionally vulnerable code—turning insecure code into secure versions.
   * Integration into a CI/CD pipeline: deploy a vulnerable version, scan it, then fix, re-scan.

6. **Demonstrations / Proof of Concept**

   * For demos of attacks (e.g., SQL injection, XSS) you can use this as a reproducible environment.
   * Useful in presentations or when explaining to non-technical stakeholders “this is what an exploit looks like”.

---

### Why it’s useful

* **Low barrier to entry**: Because it’s easy to install (LAMP/WAMP/XAMPP or Docker) you don’t need complex infrastructure.
* **Comprehensive vulnerability coverage**: It spans many vulnerability types including forms, services, file handling etc. So good for broad training.
* **Safe environment**: Since it’s purposely vulnerable, you’re not risking production data. You can experiment, break things, restore easily. The project even offers “one-click system restoration” to default settings. ([GitHub][1])
* **Switchable modes**: You can switch between “secure” and “insecure” modes (so mix of difficulty or demonstration vs challenge). ([GitHub][1])
* **Community and resources**: There is a community around it, tutorials on YouTube, installation guides, etc. ([GitHub][1])

---

### How to use / installation overview

Here’s a simplified step-by-step you could follow:

1. Decide platform: e.g., use Docker (recommended for simplicity) or local LAMP/WAMP/XAMPP.
2. Clone the repository from GitHub: `git clone https://github.com/webpwnized/mutillidae.git`
3. Follow the installation instructions (README-INSTALLATION.md) inside the repo. ([GitHub][1])
4. Ensure you have PHP, MySQL (or equivalent), web server (Apache/Nginx) configured.
5. Configure Mutillidae database (there will be SQL scripts to set up tables, sample data).
6. Navigate in browser to the application. You’ll see a menu of labs or vulnerabilities.
7. Choose a vulnerability (e.g., SQL injection form) and attempt exploit. Then, optionally, switch to “secure mode” and compare how it’s fixed.
8. After finishing, you can “reset” the application to default (one-click) so everyone starts from same state.

---

### Example scenarios

* You run a training for a batch of 10 developers. You deploy Mutillidae and split them into pairs. Each pair picks one vulnerability (e.g., XSS, file inclusion) and they must exploit it and then propose a fix.
* You are building a CI/CD pipeline for your organization’s web apps. As part of the pipeline, you include a job that deploys Mutillidae, runs an automated scanner, fails the pipeline if new vulnerabilities found — so the devs practise remediation.
* You organise a CTF event for InfoSec club: you create a scoreboard, assign points for finding each vulnerability in Mutillidae.
* You are teaching non-technical stakeholders about web risks: open Mutillidae in demonstration mode and show how easy it is to exploit e.g., SQL injection, and then show the “secure” version.

---

### Things to watch / limitations

* Since it’s a **vulnerable** application, you must never expose it publicly “as is” on the Internet unless you understand the risks. It may get compromised (intentionally) and that may cause your machine to become part of malicious activity.
* The vulnerabilities are known / predetermined — so while it’s excellent for training, it may not cover the very latest “zero-day” or extremely obscure exploit types.
* Because it’s written in PHP and structured for training, it may not represent the architecture or security hygiene of modern large-scale apps (microservices, SPA front-ends, cloud native). So while good for fundamentals, you still need additional tools for modern complexities.
* Fixing the code (to move from vulnerable → secure) may require attention and code review; the “secure mode” is helpful but always verify.
* If you’re using it in a corporate environment, ensure you license/comply correctly (it’s GPL-3.0) and ensure no production data is used.
