# Prometheus and Grafana

## 🧭 1. What is **Prometheus**?

**Prometheus** is an **open-source monitoring and alerting system** originally built by SoundCloud and now part of the **Cloud Native Computing Foundation (CNCF)**.

Think of it like a **time-machine for metrics** — it collects numbers (metrics) from your applications and systems **over time** and stores them in a database that you can **query and alert on**.

### 🔹 Key features

| Feature                                | Description                                                                                            |
| -------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| **Time-Series Database (TSDB)**        | Stores metrics as a stream of timestamped values — e.g., CPU usage every 15 seconds.                   |
| **Pull-based model**                   | Prometheus **pulls** data by scraping endpoints (like `/actuator/prometheus` in Spring Boot).          |
| **PromQL (Prometheus Query Language)** | A rich query language for filtering, aggregating, and analyzing metrics.                               |
| **Service discovery**                  | Automatically finds targets in Kubernetes, EC2, Docker, etc.                                           |
| **Alerting**                           | Works with Alertmanager to send alerts (email, Slack, PagerDuty, etc.) when metrics breach thresholds. |

---

## 📊 2. What is **Grafana**?

**Grafana** is an **open-source visualization and dashboard platform**.

It doesn’t collect data — instead, it connects to data sources (like Prometheus, InfluxDB, MySQL, etc.) and helps you **visualize trends** beautifully using graphs, gauges, and heatmaps.

Think of Grafana as **the front-end** for Prometheus metrics.

### 🔹 Key features

| Feature                    | Description                                                                   |
| -------------------------- | ----------------------------------------------------------------------------- |
| **Dashboards**             | Create real-time visualizations for system or application metrics.            |
| **Multi-source support**   | Works not just with Prometheus but also ElasticSearch, Loki, CloudWatch, etc. |
| **Alerting**               | Supports rule-based alerting with rich visualization.                         |
| **Templating & Variables** | Makes dashboards reusable for multiple environments or applications.          |
| **Plugins & Marketplace**  | Ready-made dashboards for JVM, Spring Boot, Kubernetes, and more.             |

---

## ⚙️ 3. How Prometheus & Grafana Work Together

| Step | What Happens                                                                         |
| ---- | ------------------------------------------------------------------------------------ |
| 1️⃣  | Your application (e.g., Spring Boot) **exposes metrics** via `/actuator/prometheus`. |
| 2️⃣  | **Prometheus** periodically scrapes this endpoint and stores metrics.                |
| 3️⃣  | **Grafana** queries Prometheus to fetch and visualize these metrics.                 |
| 4️⃣  | You set up **alerts** either in Prometheus or Grafana for threshold breaches.        |

🧩 **Analogy:**
Prometheus is like a **security camera** recording what happens every second.
Grafana is the **monitor screen** where you watch and analyze those recordings.

---

## 💼 4. Common Use Cases of Prometheus & Grafana

### 🧠 A. Application Performance Monitoring (APM)

* Measure **response times, error rates, throughput**.
* Detect bottlenecks or spikes in latency.
* Example: Monitoring `http_server_requests_seconds` in Spring Boot.

### 🧩 B. Infrastructure Monitoring

* Track **CPU, memory, disk usage** of servers or containers.
* Works seamlessly with **Node Exporter**, **cAdvisor**, **Kube State Metrics**.

### 🧰 C. Kubernetes / Container Monitoring

* Monitor **pod health**, **cluster performance**, **deployment states**.
* Usually combined with **Prometheus Operator** + **Grafana dashboards**.

### ⚙️ D. JVM / Spring Boot Metrics

* Monitor **heap memory**, **GC pauses**, **thread count**, **request latency**, etc.
* Perfect for **Spring Boot Actuator + Micrometer** stack.

### 🏦 E. Business Metrics

* Track domain KPIs like “orders per second”, “payments processed”, etc.
* You can define **custom Micrometer counters** in code and expose to Prometheus.

### 🚨 F. Alerting and Incident Response

* Get notified when critical metrics exceed thresholds.
* Example: Alert if heap usage > 90% for more than 5 minutes.

### 🔍 G. SLA / SLO / SLI Tracking

* Define **Service Level Indicators (SLIs)** like uptime or response latency.
* Measure **SLO compliance** visually over time.

### 📈 H. Historical Trend Analysis

* Compare today’s performance to last week’s.
* Detect degradation patterns or memory leaks.

### 🧪 I. CI/CD Pipeline Health Monitoring

* Measure build/test durations, deployment success rates.
* Integrate with Jenkins or GitHub Actions metrics.

### 🕵️ J. Security / API Rate Tracking

* Observe abnormal access patterns or rate-limit breaches in APIs.

---

## 🌐 5. Example Architecture

```
+--------------------+
|  Spring Boot App   |
| exposes /actuator/ |
|   prometheus       |
+---------+----------+
          |
          | scrape (HTTP)
          v
+--------------------+
|   Prometheus       |
|   stores metrics   |
| + Alertmanager     |
+---------+----------+
          |
          | query (PromQL)
          v
+--------------------+
|     Grafana        |
|  visual dashboards |
+--------------------+
```

---

## 📦 6. Key Tools That Integrate With Prometheus & Grafana

| Tool                   | Purpose                                          |
| ---------------------- | ------------------------------------------------ |
| **Micrometer**         | Java metrics library bridging to Prometheus      |
| **Alertmanager**       | Handles alerts from Prometheus                   |
| **Node Exporter**      | OS-level metrics for Linux/VMs                   |
| **cAdvisor**           | Container-level metrics                          |
| **Kube State Metrics** | Kubernetes object metrics                        |
| **Loki**               | Log aggregation system (Grafana sibling project) |
| **Tempo**              | Distributed tracing (Grafana ecosystem)          |

---

## 📚 7. Example Prometheus Metrics in Spring Boot

| Metric                               | Description                        |
| ------------------------------------ | ---------------------------------- |
| `http_server_requests_seconds_count` | Number of HTTP requests            |
| `http_server_requests_seconds_sum`   | Total time spent handling requests |
| `jvm_memory_used_bytes`              | JVM memory usage                   |
| `process_cpu_usage`                  | CPU load of the app process        |
| `tomcat_sessions_active_current`     | Active Tomcat sessions             |

---

## 🧩 8. Real-World Example

**Scenario:**
Tom manages a loan management system built on Spring Boot.
He uses Prometheus and Grafana to:

* Track API response time to ensure under 300ms latency.
* Set alerts if memory usage spikes beyond 85%.
* Visualize request volumes per customer type.
* Display business KPIs like “loans approved per hour”.

Now Tom’s team can **predict** load issues, **prevent outages**, and **communicate performance metrics** with management using Grafana dashboards.

---

## 🧠 9. In Summary

| Aspect          | Prometheus                           | Grafana                         |
| --------------- | ------------------------------------ | ------------------------------- |
| **Purpose**     | Collect, store, and alert on metrics | Visualize and analyze metrics   |
| **Type**        | Monitoring & alerting system         | Dashboard & analytics UI        |
| **Data Source** | Pulls metrics from endpoints         | Reads data from Prometheus      |
| **Language**    | PromQL                               | Dashboard JSON (visual configs) |
| **Use Cases**   | System & app monitoring, alerting    | Visualization, reporting        |

Would you like me to give you a **combined architecture diagram (visual)** showing Prometheus + Grafana + Spring Boot + exporters + Alertmanager + CI/CD metrics flow?
I can generate it as an image for you.
