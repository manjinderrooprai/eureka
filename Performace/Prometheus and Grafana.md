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


### 🧠 **Prometheus — What It Does**

Prometheus is **a metrics collection and storage system**.
It:

* **Scrapes** metrics from your applications, Kubernetes pods, or system exporters.
* **Stores** time-series data (like CPU, memory, HTTP request rates, etc.).
* **Supports** powerful **PromQL** (Prometheus Query Language) for querying data.
* Can **alert** using the Alertmanager component.

✅ Think of Prometheus as **the “database + brain”** of your monitoring stack.

---

### 📊 **Grafana — What It Adds**

Grafana is **a visualization and analytics platform**.
It:

* Connects to Prometheus (and many other data sources like Loki, InfluxDB, CloudWatch, etc.).
* Provides **beautiful, real-time dashboards** for metrics.
* Allows you to create **interactive panels** (graphs, gauges, tables, etc.).
* Supports **alerting and annotations** visually.
* Helps with **collaboration** — sharing dashboards and insights easily.

✅ Think of Grafana as **the “face + eyes”** of your monitoring system.

---

### 🧩 **Together**

| Component      | Role                      | Example                                      |
| -------------- | ------------------------- | -------------------------------------------- |
| **Prometheus** | Collects & stores metrics | “App X has 75% CPU usage right now.”         |
| **Grafana**    | Visualizes those metrics  | Dashboard shows CPU usage graph trending up. |

---

### 🏗️ Example Setup

1. Prometheus scrapes data from:

   * Node Exporter (system metrics)
   * Application metrics (`/metrics` endpoint)
   * K8s metrics-server or custom exporters

2. Grafana connects to Prometheus as a **data source**.

3. You build a dashboard in Grafana to view:

   * CPU, memory, network usage
   * Request latency, error rates, etc.

4. Grafana alerts you when a metric crosses a threshold — using Prometheus data.

---

### ⚙️ In Short

* **Prometheus = collects + stores metrics**
* **Grafana = visualizes + analyzes metrics**

You can use Prometheus *alone* to query metrics (with PromQL),
but **Grafana makes it human-friendly** and production-ready for teams.

---

### Spring (Boot) Java** app with **Micrometer → Prometheus → Grafana

# 1) What you need (short)

* In your Spring Boot app: **Spring Boot Actuator** + **Micrometer Prometheus registry**.
* Prometheus server to **scrape** `/actuator/prometheus`.
* Grafana to visualize dashboards (many community dashboards exist for Spring/JVM).

---

# 2) Spring Boot: dependencies

**Maven**

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
<dependency>
  <groupId>io.micrometer</groupId>
  <artifactId>micrometer-registry-prometheus</artifactId>
</dependency>
```

**Gradle**

```groovy
implementation 'org.springframework.boot:spring-boot-starter-actuator'
implementation 'io.micrometer:micrometer-registry-prometheus'
```

(Actuator auto-configures Micrometer Prometheus endpoint when the registry is on the classpath.)

---

# 3) Spring Boot config (application.yml / application.properties)

**application.yml**

```yaml
management:
  endpoints:
    web:
      exposure:
        include: health,info,prometheus
  endpoint:
    prometheus:
      enabled: true
# optional: if you want actuator on a different port
# management.server.port: 9091
```

Key: expose `prometheus` endpoint so Prometheus can scrape `/actuator/prometheus`.

---

# 4) Example `prometheus.yml` (Prometheus scrape config)

```yaml
global:
  scrape_interval: 15s
  evaluation_interval: 15s

scrape_configs:
  - job_name: 'spring-boot-app'
    metrics_path: '/actuator/prometheus'
    static_configs:
      - targets: ['host.docker.internal:8080']   # <--- app host:port
```

If on Kubernetes, use pod annotations / serviceMonitor instead of static_configs.

---

# 5) Quick Docker Compose (Prometheus + Grafana)

```yaml
version: '3.7'
services:
  prometheus:
    image: prom/prometheus:latest
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml:ro
    ports:
      - "9090:9090"

  grafana:
    image: grafana/grafana:latest
    ports:
      - "3000:3000"
    environment:
      - GF_SECURITY_ADMIN_PASSWORD=admin
    volumes:
      - grafana-storage:/var/lib/grafana

volumes:
  grafana-storage:
```

Add your Spring app as a separate service (or run it locally) and ensure Prometheus target uses the reachable hostname.

---

# 6) Useful PromQL examples

* HTTP request rate (per second):
  `sum(rate(http_server_requests_seconds_count{job="spring-boot-app"}[5m])) by (uri,method,status)`
* 95th percentile latency from histogram:
  `histogram_quantile(0.95, sum(rate(http_server_requests_seconds_bucket{job="spring-boot-app"}[5m])) by (le, uri))`
* JVM heap used:
  `jvm_memory_used_bytes{area="heap"}`

Metric names come from Micrometer/Spring Boot actuator (e.g. `http_server_requests_seconds_*`, `jvm_memory_*`).

---

# 7) Basic alert rule example (Prometheus rule)

```yaml
groups:
- name: spring-app.rules
  rules:
  - alert: HighHeapUsage
    expr: |
      (jvm_memory_used_bytes{area="heap"} / jvm_memory_max_bytes{area="heap"}) > 0.9
    for: 2m
    labels:
      severity: critical
    annotations:
      summary: "High JVM heap usage ({{ $labels.instance }})"
      description: "Heap > 90% for more than 2 minutes"
```

---

# 8) Grafana dashboards to import (ready-made)

Community dashboards you can import by ID (go to Grafana → Dashboards → Import → paste ID):

* **Spring Boot Statistics** — *community Spring Boot dashboard* (Grafana.com).
* **JVM (Micrometer)** — ID often listed as **4701** (JVM Micrometer / Java).
* **JVM Actuator** — ID **9568** (useful for Actuator + Micrometer metrics).

(There are multiple Spring Boot / JVM dashboards on Grafana.com — pick one that matches your metric names and Prometheus job label. Many tutorials show importing dashboard ID 14430 or similar; test a couple to find the layout you like.)

---

# 9) Tips & gotchas

* If Prometheus can’t scrape: confirm the URL (e.g. `/actuator/prometheus`), port, and firewall. A common pitfall is running actuator on a different `management.server.port`.
* For Kubernetes, prefer ServiceMonitors (Prometheus Operator) or pod annotations for automatic scraping.
* Add meaningful `application` / `instance` labels (via `management.metrics.tags`) so dashboards can filter per-app.
* Add custom metrics via Micrometer `MeterRegistry` (counters, timers, gauges) for business KPIs.

---

# 10) Quick example: add a custom counter in code

```java
@Component
public class MyService {
  private final Counter ordersCounter;

  public MyService(MeterRegistry registry) {
    this.ordersCounter = Counter.builder("orders_processed_total")
      .description("Total processed orders")
      .register(registry);
  }

  public void processOrder(Order o) {
    // ... processing
    ordersCounter.increment();
  }
}
```

Micrometer will expose this as `orders_processed_total` to Prometheus automatically.

---

# 11) References / further reading

* Spring Boot Actuator Prometheus endpoint (official docs).
* Micrometer Prometheus integration docs.
* Grafana dashboards for Spring Boot / JVM (search & import on Grafana.com).
* Practical walkthrough (Baeldung).
