# OWASP ZAP

OWASP ZAP is a free, open-source **Dynamic Application Security Testing (DAST)** tool — a proxy-based scanner that tests **running** web apps and APIs by crawling them and sending attack payloads to reveal runtime vulnerabilities (SQLi, XSS, auth/logic issues, misconfigurations, etc.). It’s maintained by OWASP and a volunteer community and is broadly used by developers, QA, pentesters and DevSecOps teams.

---

# Key concepts / capabilities

* **Proxy + Interception** — ZAP runs as a man-in-the-middle proxy so it can intercept, view and modify HTTP(S)/WebSocket traffic between a browser (or test runner) and the target app. This lets it observe application behavior and craft attacks.
* **Spider / Crawlers** — automated crawlers discover pages, links and API endpoints (seeded from a URL or an OpenAPI spec). 
* **Passive scanning** — analyses observed traffic (no active tampering) and flags issues that can be detected safely from responses. 
* **Active scanning** — sends specially crafted attack requests to attempt to exploit vulnerabilities (this is intrusive and should only be used against systems you own/are authorized to test). 
* **API scanning** — ZAP can import OpenAPI/Swagger/GraphQL specs and run API-focused scans (there’s a dedicated API scan workflow and scripts). 
* **Add-ons & scripting** — extensible via add-ons and script engines (JavaScript, Python, etc.) so you can add checks, authentication flows, or custom rules. 
* **Automation / Headless mode & REST API** — ZAP exposes a programmatic API so it can run headless (daemon) and be automated from CI pipelines or orchestration scripts. 

---

# Architecture & components (how ZAP is built / how it works)

1. **Browser / Client → ZAP Proxy → Target web app**

   * You configure your browser or test runner to use ZAP as an HTTP(S) proxy. ZAP records requests/responses and the Site Tree (discovered URLs). From there, its spider and scanners operate. (MitM proxy pattern.) 

2. **Core engine / Site Tree**

   * Stores discovered pages, params, cookies, and evidence. Passive and active scan rules operate against items in the Site Tree.

3. **Spider / AJAX Spider / API Importer**

   * Several discovery tools: classic HTML link spider, AJAX/DOM spider for JS apps, and OpenAPI importer for APIs. Use the right crawler for SPAs/APIs.

4. **Passive scanner & Active scanner modules**

   * Passive scanner runs by default on observed traffic. The active scanner runs attack modules (SQLi tests, XSS payloads, etc.) and requires explicit execution. Active scans may change server state. 

5. **Add-ons & scripting layer**

   * Extend functionality: authentication helpers (form-auth, OAuth), WebSocket utilities, additional vulnerability checks, reporting exporters, and CI helpers. 

6. **REST API & Docker**

   * ZAP provides a programmatic API (start/stop scans, import OpenAPI, get alerts) and official Docker images + example scripts for headless CI execution.

---

# Common use-cases

* **Developer/QA local testing** — run ZAP desktop, browse the app through the proxy, observe passive alerts, then run targeted active scans on dev/staging. Good for exploratory security testing during feature development. 
* **Automated DAST in CI/CD** — run ZAP headless in a pipeline (Docker + ZAP API) after deployment to test runtime security; fail build if high-severity alerts found. Useful for catching regressions before production. 
* **API security scanning** — import OpenAPI/Swagger/GraphQL spec and run an API-tuned scan to find auth flaws, injection issues and broken access controls. 
* **Penetration testing / bug bounty labs** — pentesters use ZAP’s active scanning + manual request tampering to validate and exploit logic flaws. 
* **Security training / CTFs** — campaign-style labs and training environments to teach web vulnerabilities (practical exploitation and remediation). 

---

# Integrations & deployment patterns

* **Desktop + GUI** — perfect for interactive testing, manual request editing and learning. 
* **Daemon + REST API** — run headless in CI (start ZAP daemon, seed URLs or import OpenAPI, run spider, then active scan, export report). 
* **Docker images** — official Docker images include scripts (api-scan) tailored for CI pipelines and API scanning. Use in GitHub Actions / GitLab CI / Jenkins. 
* **CI gating example** — common pattern: deploy staging, run automated functional tests (to exercise flows), then run ZAP spider/active scan and fail the pipeline on critical alerts. Community provides sample GitHub Action integrations.

---

# Operational notes & best practices

* **Only scan authorised targets** — active scanning is intrusive and can break or modify application state. Only run against apps you own or have explicit permission to test.
* **Use API / OpenAPI import for APIs** — better coverage for API endpoints than pure HTML spidering. 
* **Authentication & complex flows** — configure ZAP’s authentication helpers (form auth, scripts) or use automated login scripts so scans can reach authenticated pages. 
* **Tune scan policies** — reduce noise and false positives by tailoring which rules to run (important for CI to avoid blocking on low-priority issues). 
* **Combine with SAST/IAST** — DAST finds runtime issues; combine with SAST/IAST for fuller coverage and to reduce false positives. 

---

# Quick example — run a simple headless API scan with Docker

(Assumes Docker available; replace `TARGET_URL` / `OPENAPI_URL`)

```bash
# pull official ZAP image
docker pull owasp/zap2docker-stable

# run API scan using included script (example)
docker run --rm -v $(pwd):/zap/wrk/:rw owasp/zap2docker-stable zap-api-scan.py \
  -t https://your-api.example.com/openapi.json \
  -f openapi \
  -r zap-report.html
```

Or run daemon + API calls:

```bash
# start zap daemon
docker run -u root -p 127.0.0.1:8090:8090 -d owasp/zap2docker-stable zap.sh -daemon -port 8090

# use zap cli or scripts to call Spider/Active scan via REST API (see docs).
```

Docs & script examples: ZAP docs and Docker api-scan script. ([ZAP][4])

---

# Limitations & caveats

* **Can’t find everything** — DAST cannot reliably detect business logic flaws or some auth issues; it’s most effective for input validation and server misconfigurations. Combine tools/methods.
* **False positives** — tune rules and validate findings manually before triage.
* **Resource & time** — thorough active scans can take long and may stress staging environments; schedule scans appropriately. 
---

# When to use ZAP vs other approaches

* **Use ZAP** when you need a community-driven, flexible, no-cost DAST that you can extend, script and integrate into pipelines. Great for web apps/APIs and for teams who want ownership of their scanning. 
* **Complement with SAST/IAST/RASP** for source-level, runtime in-app insights, and runtime protection respectively. ]

---

# Recommended next steps (pick one)

1. **Quick start**: run the ZAP desktop, configure your browser proxy, browse your staging app and watch passive alerts. (Docs: Getting started).
2. **CI prototype**: run the Docker `zap-api-scan.py` against an OpenAPI spec for one service and produce an HTML report.
3. **Lab / training**: use Mutillidae or another intentionally vulnerable app and practise intercepting, passive/active scanning and manual verification. 
