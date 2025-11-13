## What is a Benchmark in Performance Testing?

A benchmark is a standard or reference point against which the performance of an application is measured. After running performance tests (e.g., with 50,000 users) and gathering metrics like response time, throughput, and latency, you need a benchmark to determine if the application's performance is good, bad, or excellent.

## 5 Steps to Decide the Benchmark

The video outlines a five-step process for establishing performance testing benchmarks:

### 1. Understand the Requirements
* **Consult Stakeholders:** Talk to the business team, project team, and application owners.
* **Gather Expectations:** Determine the expected user load (e.g., 50,000 concurrent users) and the expected response time under that load (e.g., less than 2 seconds).
* **Identify Specific Metrics:** Ask about other important metrics like throughput, latency, or error percentage.
* **Check Industry Standards:** Consider any regulatory requirements or industry-specific standards for your application type.

### 2. Identify Key Performance Indicators (KPIs)
The standard KPIs to check during performance testing include:
* Response time (min, max, average)
* Throughput (e.g., requests per second)
* Error rate (percent of failed requests)
* Latency (time for a request to be processed)
* Resource utilization (CPU, memory, disk usage)

### 3. Determine Benchmark Values
You can source your benchmark values from several places:
* **Industry Standards:** For example, Google's recommendation for web page load time is often 3 seconds or less.
* **Historical Data:** Use results from previous performance tests.
* **Production Logs:** If no tests exist, analyze real-world production logs to see user loads and corresponding application responses.
* **Business Requirements:** The business team may have specific expectations for response time or throughput.
* **Competitor Analysis:** You can also compare the performance of similar applications.

### 4. Categorize Performance
* Create simple categories like "excellent," "good," "fair," or "poor."
* Define these categories with clear metrics. For example, "Excellent" might be: response time < 1s, throughput > 100 requests/sec, and error rate < 1%.
* This simplifies communication with stakeholders, who don't need to see the entire raw data report.

### 5. Validate with Stakeholders
* Once you have defined the benchmark values and categories, share them with all stakeholders.
* Ensure everyone agrees on these standards and get written approval before you begin performance testing.

**Final Note:** It is recommended to run performance tests in a separate, dedicated environment, not on the production environment.
