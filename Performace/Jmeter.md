# Apache JMeter

Apache JMeter is an open-source Java application for load testing and functional testing of services — primarily web (HTTP/HTTPS) but also FTP, JDBC, JMS, SMTP, LDAP and more. It simulates many virtual users (threads) making requests, measures performance (response times, throughput, errors) and generates reports.

# Typical use cases

* Load and stress testing web applications and APIs.
* Performance benchmarking and capacity planning.
* Regression/performance tests in CI pipelines (non-GUI mode).
* Functional testing of protocols supported by JMeter (DB queries, mail, FTP).
* Simulating concurrent users for single-page apps, microservices, or backend APIs.

# Requirements (quick)

* Java runtime (JRE/JDK) installed: Java 8 or later (use `java -version` to confirm).
* Sufficient CPU/memory on test machine(s) — for large loads use dedicated load generators or distributed testing.

---

# Install JMeter — step-by-step

## 1) Download (all OS)

1. Go to the Apache JMeter download page (binary archive).
2. Download the latest binary (zip/tgz).
   *(If you prefer package managers see below.)*

## 2) Install on Windows

1. Make sure Java is installed and `java -version` works.
2. Extract the ZIP to `C:\apache-jmeter-<version>\`.
3. Run GUI: `C:\apache-jmeter-<version>\bin\jmeter.bat`.
4. (Optional) Add `...\bin` to PATH for convenience.

## 3) Install on macOS

Option A — Homebrew (easy):

```bash
brew install jmeter
```

Option B — manual:

1. Ensure Java is installed (`java -version`).
2. Download and extract the tgz; open Terminal and run:

```bash
cd apache-jmeter-<version>/bin
./jmeter
```

## 4) Install on Linux

1. Ensure Java is installed: `sudo apt install openjdk-11-jdk` (Debian/Ubuntu) or use your distro package manager.
2. Extract the downloaded tar.gz:

```bash
tar -xzf apache-jmeter-<version>.tgz
cd apache-jmeter-<version>/bin
./jmeter
```

## 5) Headless / CI usage

You do **not** run GUI in CI. Use non-GUI (recommended for load tests) — example below.

---

# First test — step-by-step (HTTP GET example)

### 1) Launch JMeter GUI

Run `jmeter` (or `jmeter.bat`) to open the GUI.

### 2) Create a Test Plan

* Right-click **Test Plan** → **Add → Threads (Users) → Thread Group**.

  * Set **Number of Threads (users)** = 10
  * **Ramp-Up Period (sec)** = 10
  * **Loop Count** = 5 (or Forever unchecked)

### 3) Add an HTTP Request Sampler

* Right-click **Thread Group** → **Add → Sampler → HTTP Request**.

  * Server Name or IP: `example.com`
  * Protocol: `https` (or `http`)
  * Path: `/`
  * Method: `GET`

### 4) Add a Listener to see results

* Right-click **Thread Group** → **Add → Listener → View Results in Table** (or **Aggregate Report**, **Summary Report**, **View Results Tree** for debugging).

> Note: Listeners in GUI are fine for debugging small tests; avoid heavy listeners in load runs.

### 5) Add Assertions or Timers (optional)

* **Assertion**: Right-click HTTP Request → Add → Assertions → Response Assertion (to verify response code or body).
* **Timer**: Add → Timer → Constant Timer (simulate think time).

### 6) Save Test Plan

File → Save as `my_test.jmx`.

### 7) Run (GUI)

Click the green Start button. View results in the Listener you added.

---

# Non-GUI / Real load test (recommended)

Run load tests from terminal to avoid GUI overhead.

Example: run test and save results:

```bash
# run test non-gui and save .jtl
jmeter -n -t my_test.jmx -l results.jtl
```

Generate an HTML dashboard from results (either during run or after):

```bash
# generate dashboard after run
jmeter -g results.jtl -o /path/to/dashboard-output
# or run and produce dashboard in one step:
jmeter -n -t my_test.jmx -l results.jtl -e -o /path/to/dashboard-output
```

* `-n` = non-GUI, `-t` = test file, `-l` = results log, `-e` = generate report, `-o` = output folder (must not exist or must be empty).

---

# Distributed testing (basic idea)

* Master (controller) and multiple slave/jmeter-server instances to generate more load.
* Start `jmeter-server` on remote machines and configure `remote_hosts` in master `bin/jmeter.properties`.
* Use `Remote Start` or `-r` option: `jmeter -n -t test.jmx -r -l results.jtl`.

(Distributed testing needs synchronized clocks, same JMeter version on all nodes, and sufficient network throughput.)

---

# Important listeners & result types

* **Aggregate Report** — averages, percentiles, throughput, error %.
* **Summary Report** — quick summary lines.
* **View Results Tree** — full request/response (use only for functional debugging).
* **HTML Dashboard** — production-quality charts and metrics for reports.

---

# Useful elements (quick reference)

* **Thread Group** — users/threads.
* **HTTP Request** — sampler to call HTTP/HTTPS endpoints.
* **CSV Data Set Config** — feed usernames/passwords/rows from CSV.
* **Assertions** — check response codes/content.
* **Timers** — add latency between requests.
* **Pre/Post Processors** — extract data (JSON/Regex), set variables.
* **Config Elements** — HTTP Header Manager, Cookie Manager, Cache Manager.
* **Listeners** — display/store results.

---

# CLI common commands (examples)

* Non-GUI run: `jmeter -n -t test-plan.jmx -l results.jtl`
* Generate HTML report from .jtl: `jmeter -g results.jtl -o /path/to/report`
* Run distributed remote tests: `jmeter -n -t test.jmx -r`
* Print JMeter version: `jmeter --version` (or check `bin/jmeter -v`)

---

# Best practices / tips

* **Never** use GUI for large load runs — it consumes memory/CPU and distorts results. Use non-GUI.
* Warm up the system before measuring steady state.
* Use monitors (CPU, memory, JVM GC, network) on target servers while load testing.
* Keep test machines separate from target servers.
* Parameterize requests (CSV Data Set) for more realistic testing.
* Use appropriate ramp-up and realistic think times (Timers).
* Use Sufficient sampling (high throughput) but keep result logging minimal — store only metrics needed.
* Correlate tokens or session IDs via Post Processors (Regex/JSON Extractor).
* Record workflows with the **HTTP(S) Test Script Recorder** for complex UIs (be mindful of HTTPS certificates).

---

# Common troubleshooting

* **“Java not found” / can't start JMeter**: ensure Java is installed and `JAVA_HOME` (or PATH) set. `java -version` must show Java 8+.
* **OutOfMemoryError**: increase JMeter heap in `bin/jmeter` / `bin/jmeter.bat` (look for `HEAP` or `-Xmx`) or move listeners to non-GUI.
* **403/401 from target**: missing headers, CSRF token or authentication — add HTTP Header Manager, Cookie Manager, and extract/submit tokens.
* **High CPU on load generator**: scale out to more load generators or reduce GUI listeners.
* **Distributed testing connection issues**: ensure ports (1099, etc.) are open and same JMeter versions on all nodes.

---

# Small end-to-end example (HTTP POST with CSV data)

1. Add **CSV Data Set Config** (filename: `users.csv`, variable names: `user,passwd`, recycle: true).
2. Add **HTTP Request**: Method POST, Path `/login`, Body Data: `username=${user}&password=${passwd}` and add **Content-Type: application/x-www-form-urlencoded** via **HTTP Header Manager**.
3. Add **Response Assertion**: expected text `Welcome` or response code `200`.
4. Run in non-GUI:

```bash
jmeter -n -t login_test.jmx -l login_results.jtl -e -o login_report
```

5. Open `login_report/index.html` in a browser.
