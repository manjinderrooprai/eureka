✅ Complete **synthetic HR dataset** (JD + CVs)
✅ Full **workflows** for your multi-agent system
✅ **Tool configuration blueprint** (exact text to paste into Orchestrate)
✅ **Prompts**, **agent instructions**, and **API payloads**
✅ **Demo script** for your final recording
✅ **Architecture diagram (text version)**
✅ **Pitch deck outline**
✅ **Evaluation-ready submission text**

---

# **PART 1 — Synthetic HR Dataset (Fully Compliant with Hackathon Rules)**

The hackathon guide states that you must use your **own synthetic dataset** and **no PII / no confidential data**.


Below is a fully synthetic, clean dataset you can use **as-is**.

---

## **1.1 Job Description (Synthetic)**

**Job ID:** `JOB-2025-JAVA-SR`
**Role:** Senior Java Developer
**Department:** Engineering
**Location:** Bangalore
**Job Description Text:**

> We are looking for a Senior Java Developer with strong experience in building scalable backend services using Spring Boot and microservices. The candidate must have deep knowledge of REST APIs, database design, and CI/CD. Experience with cloud platforms and containerization is preferred. The role involves collaborating with cross-functional teams and delivering high-quality code in an agile environment.

### **Extractable Structured Fields**

* Required Skills:

  * Java, Spring Boot, Microservices
  * REST API design
  * SQL & Database design
  * CI/CD pipelines
* Preferred Skills:

  * Docker, Kubernetes
  * AWS or IBM Cloud
  * Messaging systems (Kafka, RabbitMQ)
* Experience:

  * 5–8 years
* Employment Type:

  * Full-time
* Location:

  * Bangalore

---

## **1.2 Candidate Profiles (Synthetic)**

### **Candidate 1**

**ID:** `CAND-001`
**Name:** Arjun Mehta
**Email:** [arjun.mehta@example.com](mailto:arjun.mehta@example.com)
**CV Text:**

> 7+ years of experience in Java backend development. Strong knowledge of Spring Boot, microservices, REST API architecture, AWS Lambda, DynamoDB, and CI/CD using Jenkins. Successfully led a team of 3 engineers. Experience with Docker and Kubernetes for deployment.

---

### **Candidate 2**

**ID:** `CAND-002`
**Name:** Riya Nair
**Email:** [riya.nair@example.com](mailto:riya.nair@example.com)
**CV Text:**

> 5 years of experience in Java, Spring MVC, Hibernate, and microservices. Built scalable services for e-commerce platforms. Familiar with Docker, basic AWS (EC2), and GitHub Actions for CI/CD. Experience working in agile teams.

---

### **Candidate 3**

**ID:** `CAND-003`
**Name:** Dev Kumar
**Email:** [dev.kumar@example.com](mailto:dev.kumar@example.com)
**CV Text:**

> 3 years of backend development experience. Strong core Java and REST APIs. Limited experience with Spring Boot. Eager to learn microservices and cloud technologies.

(This one will show how the screening agent handles low experience.)

---

# **PART 2 — Multi-Agent Workflow Logic (End-to-End)**

Below is the full workflow of your system:

---

## **2.1 Recruiter Use Case Flow**

### **Step 1:**

Recruiter says:

> “Create pipeline for Senior Java Developer and screen all candidates.”

### **Coordinator Agent → Screening Agent**

1. Calls:

   * `GET /jobs/JOB-2025-JAVA-SR`
   * `GET /jobs/JOB-2025-JAVA-SR/candidates`
2. Screening agent:

   * Extracts JD skills
   * Parses each CV
   * Scores each candidate
   * Generates reasons + risks

---

### **Step 2 — Compliance Agent Review**

Coordinator sends the ranked list to the **Compliance Agent**:

* Checks for bias
* Marks PASS / WARN / FAIL
* Sends JSON + short audit summary

---

### **Step 3 — Interview Scheduling**

Recruiter says:

> “Schedule interviews with top 2 candidates this week.”

Scheduler agent:

1. Calls:

   * `GET /calendar/slots?user_id=HR001`
   * `GET /calendar/slots?user_id=MANAGER001`
2. Finds overlap
3. Creates meeting:

   * `POST /meetings`
4. Sends invite email using:

   * `POST /notify`

---

### **Step 4 — Hiring & Onboarding**

Recruiter:

> “Mark CAND-001 as hired and start onboarding.”

Onboarding agent:

1. Creates tickets:

   * Laptop
   * ID card
   * Tool access
2. Sends:

   * Welcome pack (via watsonx.ai)
   * Summary to manager

---

# **PART 3 — Tools to Configure in Orchestrate (Exact Text to Paste)**

These go into **watsonx Orchestrate → Tools → Add Tool → HTTP Tool**.

---

## **3.1 Tool: Get Job Description**

**Name:** GetJobDescriptionTool
**Method:** GET
**URL:**

```
http://<your-backend-host>/jobs/{job_id}
```

**Path Parameter:**

* `job_id` — string

**Response Example (paste in sample):**

```json
{
  "job_id": "JOB-2025-JAVA-SR",
  "title": "Senior Java Developer",
  "description": "We are looking for a Senior Java Developer...",
  "location": "Bangalore",
  "department": "Engineering"
}
```

---

## **3.2 Tool: List Candidates**

**Name:** ListCandidatesTool
**Method:** GET
**URL:**

```
http://<your-backend-host>/jobs/{job_id}/candidates
```

**Response Example:**

```json
{
  "job_id": "JOB-2025-JAVA-SR",
  "candidates": [
    {
      "candidate_id": "CAND-001",
      "name": "Arjun Mehta",
      "email": "arjun.mehta@example.com",
      "cv_text": "7+ years..."
    }
  ]
}
```

---

## **3.3 Tool: Update Candidate Status**

**Name:** UpdateCandidateStatusTool
**Method:** POST
**URL:**

```
http://<your-backend-host>/candidates/{candidate_id}/status
```

**Body Example:**

```json
{
  "status": "SHORTLISTED",
  "reason": "Strong match to JD"
}
```

---

## **3.4 Tool: Get Free Slots**

**Name:** GetFreeSlotsTool
**Method:** GET
**URL:**

```
http://<your-backend-host>/calendar/slots
```

**Query Parameters:**

* `user_id`
* `from_date`
* `to_date`

**Response Example:**

```json
{
  "user_id": "HR001",
  "slots": [
    { "start": "2025-12-11T10:00:00", "end": "2025-12-11T10:30:00" }
  ]
}
```

---

## **3.5 Tool: Create Meeting**

**Name:** CreateMeetingTool
**Method:** POST
**URL:**

```
http://<your-backend-host>/meetings
```

**Body Example:**

```json
{
  "title": "Interview for Senior Java Developer",
  "participants": ["candidate@example.com", "hr@example.com"],
  "start": "2025-12-11T10:00:00",
  "end": "2025-12-11T10:30:00",
  "location": "Zoom link here"
}
```

---

## **3.6 Tool: Notify / Send Email**

**Name:** SendEmailTool
**Method:** POST
**URL:**

```
http://<your-backend-host>/notify
```

---

## **3.7 Tool: Create Ticket**

**Name:** CreateTicketTool
**Method:** POST
**URL:**

```
http://<your-backend-host>/tickets
```

---

## **3.8 Tool: Audit Log**

**Name:** WriteAuditLogTool
**Method:** POST
**URL:**

```
http://<your-backend-host>/audit-log
```

