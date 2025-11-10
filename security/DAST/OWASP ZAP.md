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

# Quick glossary + purpose

* **Session**

  * **What:** ZAP’s saved workspace (site tree, history, alerts, config).
  * **Why:** persist or share a testing state (so you can pause/resume a pentest or save evidence).
  * **UI:** `File → New Session` / `File → Save Session` / `File → Open Session`.
  * **Automation:** export/import session files when running long analyses or to keep CI evidence.
  * **Tip:** Save a session before/after active scans so you can analyze evidence later.

* **Context**

  * **What:** Logical grouping of URLs/hosts, authentication parameters, users and session-handling rules.
  * **Why:** enables targeting scans to a particular app area, configures authentication and session management for that logical app.
  * **UI:** `Contexts → New Context` → define Included/Excluded URLs, Authentication, Users, Session Tracking.
  * **Automation:** create contexts via the API and add include/exclude regexes so automated scans operate only on intended paths.
  * **Tip:** Use contexts for multi-tenant apps or when a single ZAP instance scans many apps.

* **Scope (in-scope / out-of-scope)**

  * **What:** Which URLs/hosts are allowed for active scanning or automation. Usually expressed as context include/exclude regexes or global in-scope settings.
  * **Why:** prevents accidental scanning of third-party domains and limits noise/false positives.
  * **UI:** In the Sites tree or Context → Include in Context; also use the “In scope” checkbox on entries.
  * **Automation:** set include/exclude rules in a context or pass a flag (e.g., “inScopeOnly”) to API scans.
  * **Tip:** Always define an explicit scope before running active scans to avoid hitting unauthorized targets.

* **Spider / Crawlers**

  * **What:** Discovery crawlers (standard spider, AJAX spider, and API importers) that find links/endpoints.
  * **Why:** build the site tree (surface pages and parameters) so scans know what to test.
  * **UI:** `Spider` tab or `Tools → Spider` / for SPAs use AJAX Spider. For APIs import OpenAPI.
  * **Automation:** call the spider via the REST API or use scripts that first authenticate then spider.
  * **Tip:** Use AJAX spider for JS-heavy SPAs and OpenAPI import for APIs — HTML spider alone often misses dynamic routes.

* **Passive Scan**

  * **What:** Non-intrusive checks performed on observed traffic (no malicious payloads). Detects headers, cookies, information leakage, insecure cookie flags, etc.
  * **Why:** safe to run against production if only passively observing legitimate browsing or test transactions.
  * **UI:** Passive alerts appear automatically in the Alerts pane when ZAP proxies traffic. You can enable/disable specific passive scanners in `Options → Passive Scan`.
  * **Automation:** passive scanning occurs as traffic is recorded; in CI you can exercise flows (functional tests) and then export passive alerts.
  * **Tip:** Combine automated functional tests with passive scanning to catch configuration mistakes without intrusive tests.

* **Active Scan**

  * **What:** Intrusive testing that sends attack payloads to try to exploit vulnerabilities (SQLi, XSS, LFI, etc.).
  * **Why:** finds exploitable runtime vulnerabilities — but can change server state and must be used only on authorized targets.
  * **UI:** Right-click a node in the Site Tree → `Attack → Active Scan` (choose policy and scope). Configure scan policy & strength.
  * **Automation:** run headless via ZAP’s REST API or the docker scripts (zap-api-scan, zap-baseline) in pipelines.
  * **Tip:** tune scan policies and use `inScopeOnly` and authentication so the scanner can reach protected endpoints and avoid harming production.

* **Scan Policy**

  * **What:** A configurable set of active scan rules, attack strength, enabled checks and thresholds (you pick which checks to run and at what aggression).
  * **Why:** reduce noise, shorten scan time, and avoid destructive checks for CI by enabling only the rules you care about.
  * **UI:** `Tools → Options → Active Scan` or `Manage Scan Policies` (ZAP GUI lets you create/save policies).
  * **Automation:** import custom scan policy files into ZAP before running automated scans so the same policy is applied across runs.
  * **Tip:** create separate policies for “quick CI” (high-precision, non-destructive) and “full pentest” (comprehensive, longer, higher risk).

* **Authentication & Users (within Context)**

  * **What:** config that tells ZAP how to log in (form-based, HTTP basic, scriptable flows like OAuth) and user identities to scan as.
  * **Why:** many vulnerabilities are only visible after authentication; scans must be able to exercise authenticated flows.
  * **UI:** Context → Authentication → set method; then create Users and Test Authentication.
  * **Automation:** use script-based auth helpers or record login flows; supply credentials via CI secrets.
  * **Tip:** verify login works via ZAP’s “Forced User” or test auth feature before running active scans.

* **Forced User & Session Management**

  * **What:** force outgoing requests to be associated with a particular “user” session (useful for multi-user tests). Session management config maps cookie/session tokens, etc.
  * **Why:** test authorization/business logic by scanning as different users (admin vs regular).
  * **UI:** Context → Session Management and Forced User settings.
  * **Tip:** configure proper session tracking to avoid being logged out mid-scan.

* **Alerts & Reporting**

  * **What:** ZAP categorizes findings (risk levels, description, evidence, references) and can export HTML/JSON/XML reports.
  * **Why:** triage and hand off vulnerabilities to developers with evidence and remediation advice.
  * **Automation:** export reports after scan completion and fail CI build if thresholds exceeded. Use the API to fetch alerts and integrate with ticketing.
  * **Tip:** tune thresholds for CI (e.g., fail on High/Critical only) to reduce noisy pipeline failures.

---

# Typical manual workflow (UI)

1. Start ZAP (GUI).
2. Create a **Session**.
3. Create a **Context** for your app; add include regexes that define **scope**.
4. Configure **Authentication** and create **Users**; test login.
5. Configure **Passive Scan** settings (enable/disable checks you care about).
6. Browse the application through ZAP proxy (or run automated functional tests against the proxy) so the **Spider** and passive scanner populate the Site Tree and alerts.
7. Run **Active Scan** against the in-scope nodes using an appropriate **Scan Policy** and an authenticated user if needed.
8. Review **Alerts**, save **Session**, generate report, and export findings.

---

# Typical automated workflow (CI / headless)

1. Start ZAP in daemon mode (Docker or service).
2. Seed discovery: import OpenAPI or run spider via API; or run functional tests against the staging deployment while ZAP proxies traffic.
3. Ensure authentication: upload login script or configure context users via API.
4. Run active scan (pass `inScopeOnly=true` and the chosen scan policy).
5. Wait for scan to finish; fetch alerts via API and generate HTML/JSON report.
6. Fail the build or create issues if alerts above threshold (e.g., Critical/High) are found.
7. Save session/artifacts for triage.

---

# Useful automation snippets (pattern)

* **API pattern:** ZAP’s management API runs at `http://127.0.0.1:PORT/` and exposes endpoints like `/JSON/<component>/action/<operation>?params...&apikey=APIKEY`. Use this to script: create context, include regex, import auth, run spider, run ascan, fetch alerts.
* **Docker helper:** use `owasp/zap2docker-stable` with built-in scripts `zap-api-scan.py`, `zap-baseline.py` for common CI runs. (These scripts wrap context import, spidering and scanning.)

---

# Practical tuning & safety tips

* **Always** run Active Scans only against authorized targets (staging or explicit test environments).
* Use **scan policies** to exclude destructive checks (file uploads, destructive injections) for CI.
* Use **contexts** + **authentication** to include only protected endpoints you want scanned.
* Use `inScopeOnly` to prevent scans from following external links.
* Balance depth vs time: full active scans are thorough but slow. For CI use a small focused policy and schedule full scans overnight.
* Validate **false positives** manually before reporting. Passive scans help triage low-risk issues quickly.

---

# Troubleshooting 

* ZAP can’t reach JS-rendered links with classic spider → use AJAX spider or run Cypress/Playwright tests through ZAP so dynamic links are exercised.
* If scans are failing to authenticate, record login with the browser proxied through ZAP and convert that to an authentication script.
* If alerts are noisy in CI, create an allowlist of known acceptable low-risk items and fail only on high severity.
* Save sessions and reports from CI runs to preserve evidence for audits.

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
