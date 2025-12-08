# 1. Overall architecture (mental diagram)

**Front-end / UX**

* Embedded **HR Chat Assistant** built with **AI assistant builder in watsonx Orchestrate**.

**Orchestrate Agents**

1. **Screening Agent**
2. **Interview Scheduler Agent**
3. **Onboarding Agent**
4. **Compliance & Responsible AI Agent**
5. **Coordinator / HR Assistant** (main chat-facing agent that delegates to others)

**Backend / Tools (Python FastAPI)**

* `GET /jobs/{job_id}`
* `GET /jobs/{job_id}/candidates`
* `POST /candidates/{id}/status`
* `GET /calendar/slots`
* `POST /meetings`
* `POST /tickets`
* `POST /notify`
* `POST /audit-log`

**watsonx.ai**

* Prompt Lab for designing prompts
* Same prompts called programmatically via API inside your tools (or via ADK custom skills).

---

# 2. Agent definitions for Orchestrate

You’ll configure these in **Agent Builder**:

---

## 2.1 Screening Agent

**Name**: `HR Screening Agent`
**Profile / Description (paste into “description” field)**

> You are an HR screening specialist for an enterprise. Your job is to read job descriptions, analyze candidate profiles, and produce structured evaluation results. You extract required skills from the job, compare them with each candidate’s experience, and assign a fit score with short, clear reasoning. You never use sensitive attributes such as gender, age, religion, or marital status for ranking.

**Style**

* Tone: professional, concise, recruiter-friendly
* Behavior:

  * Uses bullet points and tables where possible
  * Explains reasoning in 2–4 sentences per candidate

You can summarize as Orchestrate “style” text:

> Use a professional, neutral HR tone. Prioritize clarity and structure. Present results as ranked lists or tables. Provide short, factual justifications. Do not overuse marketing language.

**Key Instructions**

Add these in “instructions”:

1. Always extract:

   * Required skills
   * Preferred skills
   * Experience range
   * Location / work type if present
2. For each candidate:

   * Compute a **fit_score 0–100**
   * Provide **top_3_reasons** for the score
   * Indicate **risk flags**, e.g. “skills mismatch”, “experience too low”.
3. Never use or mention gender, age, ethnicity, marital status, or other sensitive information in any decision or explanation.
4. Return data in a **JSON-like structure** when invoked by tools and a **human-readable summary** when chatting with users.

**Knowledge to upload**

* A “Competency framework” PDF (your own synthetic doc)
* Example JDs and manually-labeled screening examples

**Tools this agent will call**

* `GetJobDescriptionTool`
* `ListCandidatesTool`
* `UpdateCandidateStatusTool`
* A custom “CallWatsonxModelTool” (if you choose to offload some LLM logic to watsonx.ai directly from backend).

---

## 2.2 Interview Scheduler Agent

**Name**: `Interview Scheduler Agent`

**Profile**

> You are an assistant focused on scheduling interviews between candidates, recruiters, and hiring managers. You find overlapping free slots, propose options, and then confirm a final time. You respect working hours and avoid double-booking.

**Style**

> Be polite and efficient. Use clear time formats and list 2–3 suggested slots. Confirm time zones explicitly. Keep messages short.

**Instructions**

1. When given candidate and participants, always:

   * Fetch their free slots via tool
   * Propose 2–3 overlapping options
2. When a slot is confirmed, always:

   * Create the meeting
   * Send an email/notification with time, participants, and meeting link.
3. If you cannot find overlapping times, suggest alternative days or ask recruiter which participant to prioritize.

**Tools**

* `GetFreeSlotsTool`
* `CreateMeetingTool`
* `SendEmailTool`

---

## 2.3 Onboarding Agent

**Name**: `Onboarding Automation Agent`

**Profile**

> You are an HR onboarding coordinator. Once a candidate is marked as “Hired”, you trigger the onboarding workflow: create IT and facilities requests, generate a personalized welcome pack, and remind the manager and new hire about key tasks.

**Style**

> Friendly but professional. Use checklists and bullet points. Make it easy for HR and the new hire to see what’s done and what’s pending.

**Instructions**

1. When receiving a `Hired` event:

   * Generate an onboarding checklist grouped into HR, IT, Facilities, Manager actions.
   * Create a ticket for each item using tools.
2. Generate:

   * A **Welcome email** to the candidate.
   * A **Summary email** to the manager with tasks and deadlines.
3. Highlight any missing information (e.g., start date not known).

**Tools**

* `CreateTicketTool`
* `NotifyManagerTool`
* `GenerateOnboardingPackTool` (internally calls watsonx.ai to create pack text).

---

## 2.4 Compliance & Responsible AI Agent

**Name**: `HR Compliance & Fairness Agent`

**Profile**

> You are a compliance and responsible AI reviewer for HR decisions. You analyze candidate evaluation outputs, check them against hiring policies, and flag potential bias or policy violations. You produce an audit log that explains why decisions are acceptable or risky.

**Style**

> Analytical, neutral, policy-focused. Refer to “policy section X” if provided. Use short paragraphs and bullet points.

**Instructions**

1. Input: JSON with candidate scores, reasons, and metadata.
2. Tasks:

   * Detect any use of protected attributes (gender, age, religion, etc.) in reasons or implied decisions.
   * Flag if criteria such as “age”, “photo”, “name” or “nationality” seem to influence ranking.
   * Suggest corrected, fairer reasoning if needed.
3. Output:

   * `compliance_status` = PASS / WARN / FAIL
   * List of `issues` with severity and suggestion.
   * Short **audit summary**.
4. Never change candidate scores yourself – instead recommend what HR should review.

**Tools**

* `WriteAuditLogTool`
* The same “CallWatsonxModelTool” or built-in model to actually do the bias check.

---

## 2.5 Coordinator / HR Chat Assistant

**Name**: `TalentFlow Orchestrator`

**Profile**

> You are an HR copilot orchestrating multiple specialist agents to manage hiring workflows end-to-end. You understand recruiter requests in natural language and delegate work to the Screening, Scheduler, Onboarding, and Compliance agents.

**Style**

> Conversational, concise, and proactive. Always explain which step you’re performing. Summarize complex results clearly for busy HR users.

**Instructions**

1. Understand recruiter intent:

   * “Create hiring pipeline”, “screen candidates”, “schedule interviews”, “start onboarding”.
2. Based on intent:

   * Call Screening Agent for ranking.
   * Call Compliance Agent to validate results.
   * If recruiter approves, call Scheduler Agent.
   * Once status is “Hired”, call Onboarding Agent.
3. Always summarize what you did and what is next.
4. If a collaborator agent fails or returns ambiguous output, ask a clarifying question to the recruiter.

**Collaborators**

* Add all four agents above as “collaborator agents” for multi-agent orchestration.

---

# 3. Prompt Lab prompt designs (watsonx.ai)

Choose a **Granite chat model** (e.g. a Granite chat/instruct model that is allowed in the hackathon). Avoid disallowed models (llama-3-405b-instruct, mistral-medium-2502, mistral-small-3-1-24b-instruct-2503). 

You can use **Structured view** in Prompt Lab or just Freeform.

---

## 3.1 JD → Skills & Requirements

**Prompt (system / instruction block)**

> You are an HR job description analyzer.
> Extract a structured representation of this job description.
> Output **only valid JSON** with the following fields:
>
> * role_title (string)
> * role_summary (string)
> * required_skills (array of strings)
> * preferred_skills (array of strings)
> * min_experience_years (number or null)
> * max_experience_years (number or null)
> * location (string or null)
> * employment_type (string or null, e.g. full-time, contract)

**User input example**

> JOB DESCRIPTION:
> [paste the JD]

---

## 3.2 CV → Structured Profile

**Prompt**

> You are a recruiting assistant that parses CVs into structured JSON.
> Given the following CV/resume text, extract:
>
> * candidate_name
> * email
> * phone
> * total_experience_years
> * skills (array of strings)
> * current_title
> * current_company
> * education (array of {degree, major, institution, year})
> * past_roles (array of {title, company, start_year, end_year, key_responsibilities})
>   Output only JSON.

**User input**

> CV:
> [paste candidate profile text]

---

## 3.3 Ranking candidates against a JD

You can chain JD → JSON, CV → JSON in your backend, or do ranking in one prompt.

**Prompt**

> You are an HR expert.
> You get a job description (already structured) and a list of candidate profiles (structured).
> Compare each candidate against the job.
> For each candidate, compute:
>
> * fit_score (0–100)
> * top_3_reasons (array of strings)
> * risk_flags (array of strings, may be empty)
>   Do NOT use protected attributes (age, gender, race, nationality, religion, marital status) in your reasoning.
>   Output JSON with:
>   { "candidates_ranked": [ { "candidate_id": "...", "fit_score": 0-100, "top_3_reasons": [...], "risk_flags": [...] }, ... ] }
>   Sort by fit_score descending.

**User input**

> JOB_STRUCTURE:
> [job JSON]
>
> CANDIDATE_LIST:
> [list of candidate JSON objects]

---

## 3.4 Compliance check prompt

**Prompt**

> You are an HR compliance officer specializing in responsible AI.
> You receive candidate ranking results and their explanations.
> Identify any possible use of protected attributes (gender, age, race, religion, nationality, disability, marital status) in the reasoning, even if implied.
> Mark the output as PASS, WARN, or FAIL and explain why.
> Suggest how to correct any problematic reasoning.
>
> Output JSON:
> {
> "compliance_status": "PASS" | "WARN" | "FAIL",
> "issues": [
> { "candidate_id": "...", "severity": "LOW|MEDIUM|HIGH", "description": "...", "suggested_fix": "..." }
> ],
> "audit_summary": "..."
> }

**User input**

> RANKING_RESULTS:
> [results JSON from previous step]

---

## 3.5 Onboarding pack / welcome email prompt

**Prompt**

> You are an HR onboarding specialist.
> Generate a friendly but professional welcome email and a short onboarding summary for a new hire based on the inputs.
> Output:
>
> * welcome_email_subject
> * welcome_email_body
> * onboarding_summary_for_manager (bullet list)

**User input**

> NEW_HIRE_INFO:
> { "name": "...", "role": "...", "start_date": "...", "manager_name": "...", "location": "...", "key_policies_links": ["...", "..."] }

---

# 4. Tool / API definitions (JSON schemas)

Assume a Python backend using FastAPI.

### 4.1 Job & candidate data

```jsonc
// GET /jobs/{job_id}
{
  "job_id": "JOB-123",
  "title": "Senior Java Developer",
  "description": "Full JD text...",
  "location": "Bangalore",
  "department": "Engineering"
}
```

```jsonc
// GET /jobs/{job_id}/candidates
{
  "job_id": "JOB-123",
  "candidates": [
    {
      "candidate_id": "CAND-001",
      "name": "John Doe",
      "cv_text": "Raw CV text or pre-parsed fields",
      "email": "john@example.com",
      "status": "APPLIED"
    }
  ]
}
```

```jsonc
// POST /candidates/{id}/status
{
  "status": "SHORTLISTED",   // or REJECTED, HIRED
  "reason": "High skills match to Java and microservices"
}
```

---

### 4.2 Calendar & meetings

```jsonc
// GET /calendar/slots?user_id=HR-001&from=2025-12-10&to=2025-12-15
{
  "user_id": "HR-001",
  "slots": [
    { "start": "2025-12-11T10:00:00", "end": "2025-12-11T10:30:00" },
    { "start": "2025-12-11T15:00:00", "end": "2025-12-11T15:30:00" }
  ]
}
```

```jsonc
// POST /meetings
{
  "title": "Interview: Senior Java Developer",
  "participants": ["john@example.com", "hr@example.com", "manager@example.com"],
  "start": "2025-12-11T10:00:00",
  "end": "2025-12-11T10:30:00",
  "location": "Teams/Zoom link"
}
```

---

### 4.3 Tickets & notifications

```jsonc
// POST /tickets
{
  "system": "IT",
  "category": "Laptop Provisioning",
  "description": "Set up laptop for John Doe, Senior Java Developer, joining 15 Dec.",
  "priority": "MEDIUM"
}
```

```jsonc
// POST /notify
{
  "recipient": "manager@example.com",
  "channel": "EMAIL",
  "subject": "New hire onboarding tasks for John Doe",
  "body": "Bullet list of tasks..."
}
```

---

### 4.4 Audit log

```jsonc
// POST /audit-log
{
  "job_id": "JOB-123",
  "timestamp": "2025-12-08T12:30:00Z",
  "compliance_status": "WARN",
  "issues": [
    { "candidate_id": "CAND-003", "description": "Reason mentions age", "severity": "HIGH" }
  ],
  "raw_decision_payload": { /* original ranking JSON */ }
}
```

---

# 5. Python code skeletons

These are **skeletons** – you fill in real watsonx.ai calls by pasting the “View code” snippet from Prompt Lab where indicated (as IBM suggests in the guide). 

---

## 5.1 FastAPI backend with stub tools

```python
# app.py
from fastapi import FastAPI
from pydantic import BaseModel
from typing import List, Optional
import datetime as dt

app = FastAPI(title="TalentFlow Backend")

# ---------- MODELS ----------

class Job(BaseModel):
    job_id: str
    title: str
    description: str
    location: Optional[str] = None
    department: Optional[str] = None

class Candidate(BaseModel):
    candidate_id: str
    name: str
    cv_text: str
    email: str
    status: str = "APPLIED"

class JobCandidatesResponse(BaseModel):
    job_id: str
    candidates: List[Candidate]

class StatusUpdate(BaseModel):
    status: str
    reason: Optional[str] = None

class Meeting(BaseModel):
    title: str
    participants: List[str]
    start: dt.datetime
    end: dt.datetime
    location: Optional[str] = None

class Ticket(BaseModel):
    system: str
    category: str
    description: str
    priority: str = "MEDIUM"

class Notification(BaseModel):
    recipient: str
    channel: str
    subject: str
    body: str

class AuditLog(BaseModel):
    job_id: str
    timestamp: dt.datetime
    compliance_status: str
    issues: list
    raw_decision_payload: dict

# ---------- IN-MEMORY MOCK DATA ----------

jobs_db = {
    "JOB-123": Job(
        job_id="JOB-123",
        title="Senior Java Developer",
        description="We need a Senior Java developer with Spring Boot, microservices, REST APIs...",
        location="Bangalore",
        department="Engineering",
    )
}

candidates_db = {
    "JOB-123": [
        Candidate(
            candidate_id="CAND-001",
            name="John Doe",
            email="john@example.com",
            cv_text="8 years Java, Spring Boot, microservices, AWS...",
        ),
        Candidate(
            candidate_id="CAND-002",
            name="Jane Smith",
            email="jane@example.com",
            cv_text="4 years Java, React, microservices, Docker...",
        ),
    ]
}

# ---------- ENDPOINTS ----------

@app.get("/jobs/{job_id}", response_model=Job)
def get_job(job_id: str):
    return jobs_db[job_id]

@app.get("/jobs/{job_id}/candidates", response_model=JobCandidatesResponse)
def get_job_candidates(job_id: str):
    return JobCandidatesResponse(job_id=job_id, candidates=candidates_db[job_id])

@app.post("/candidates/{candidate_id}/status")
def update_candidate_status(candidate_id: str, payload: StatusUpdate):
    # Just log / update in memory for now
    for job_id, cand_list in candidates_db.items():
        for cand in cand_list:
            if cand.candidate_id == candidate_id:
                cand.status = payload.status
    return {"ok": True}

@app.get("/calendar/slots")
def get_free_slots(user_id: str, from_date: str, to_date: str):
    # Return dummy slots
    return {
        "user_id": user_id,
        "slots": [
            {"start": "2025-12-11T10:00:00", "end": "2025-12-11T10:30:00"},
            {"start": "2025-12-11T15:00:00", "end": "2025-12-11T15:30:00"},
        ],
    }

@app.post("/meetings")
def create_meeting(meeting: Meeting):
    # In real life, call Outlook/Google Calendar API here
    return {"ok": True, "meeting_id": "MEET-001"}

@app.post("/tickets")
def create_ticket(ticket: Ticket):
    # Store/log ticket
    return {"ok": True, "ticket_id": "TICKET-001"}

@app.post("/notify")
def notify(notification: Notification):
    # Send email or Slack message here
    return {"ok": True}

@app.post("/audit-log")
def write_audit_log(log: AuditLog):
    # Persist log to DB
    return {"ok": True}
```

Run:

```bash
uvicorn app:app --reload
```

Now each endpoint can be exposed in **Orchestrate as a tool** (HTTP integration).

---

## 5.2 Pattern for calling watsonx.ai from Python

From Prompt Lab:

1. Build your prompt until you’re happy.
2. Click **“View code” (</>)** and copy the **Python** sample – the guide says the editor provides cURL/Node.js/Python snippets. 
3. Wrap that sample in a helper function, for example:

```python
# watsonx_client.py
import requests
import os

WATSONX_ENDPOINT = os.environ["WATSONX_ENDPOINT"]  # from Developer access section
PROJECT_ID = os.environ["WATSONX_PROJECT_ID"]
MODEL_ID = os.environ["WATSONX_MODEL_ID"]

def get_iam_token(api_key: str) -> str:
    resp = requests.post(
        "https://iam.cloud.ibm.com/identity/token",
        headers={"Content-Type": "application/x-www-form-urlencoded"},
        data={
            "grant_type": "urn:ibm:params:oauth:grant-type:apikey",
            "apikey": api_key,
        },
    )
    resp.raise_for_status()
    return resp.json()["access_token"]

def call_watsonx(prompt: str, api_key: str) -> str:
    token = get_iam_token(api_key)
    headers = {
        "Authorization": f"Bearer {token}",
        "Content-Type": "application/json",
    }

    # >>> Paste the JSON body and URL from the Prompt Lab "View code" snippet here <<<
    body = {
        # "input": prompt,
        # "parameters": {...},
        # "model_id": MODEL_ID,
        # "project_id": PROJECT_ID,
    }

    resp = requests.post(
        f"{WATSONX_ENDPOINT}/ml/v1/text/generation",  # adjust to what Prompt Lab shows
        headers=headers,
        json=body,
    )
    resp.raise_for_status()
    result = resp.json()
    # Extract text according to the structure of the returned object
    return result["results"][0]["generated_text"]
```

Then in your screening tool, call `call_watsonx(...)` with the structured prompt you defined.

This avoids you having to guess the exact IBM API format; you follow the official code snippet coming from Prompt Lab (as the guide recommends). 

---

# 6. Documentation & pitch content

Here’s ready-to-adapt text for README/slides.

---

## 6.1 Problem statement (slide 1)

> Hiring teams in large enterprises spend huge amounts of time on manual, repetitive tasks – reading CVs, scheduling interviews, and coordinating onboarding. These steps are fragmented across tools (email, calendars, HRIS) and lack traceability. As a result, time-to-hire is high, candidate experience is inconsistent, and HR has little visibility into how decisions are made.

---

## 6.2 Solution (slide 2)

> **TalentFlow Orchestrator** is an AI-powered HR copilot built on **IBM watsonx Orchestrate** and **IBM watsonx.ai**. It orchestrates multiple specialized agents that:
>
> * Automatically screen and rank candidates against job descriptions
> * Schedule interviews by coordinating calendars
> * Trigger onboarding workflows once a candidate is hired
> * Run compliance checks to ensure decisions are fair and responsible

---

## 6.3 Architecture (slide 3–4)

Bullet points:

* **Front-end**: Orchestrate AI assistant builder embedded chat.
* **Orchestrate agents**: Screening, Scheduler, Onboarding, Compliance, Coordinator.
* **Backend tools**: Python FastAPI microservice exposing REST APIs consumed as Orchestrate tools.
* **watsonx.ai**: Granite model for JD parsing, CV parsing, ranking, onboarding email generation, and compliance text analysis.

Add an architecture diagram with arrows: Recruiter → Chat Assistant → Agents → Tools → watsonx.ai.

---

## 6.4 Responsible AI (slide 5)

* Synthetic HR datasets; no PII, no client data.
* Compliance Agent checks for use of protected attributes in reasoning.
* Decision logs stored via `/audit-log` endpoint for auditability.
* Instructions to agents explicitly forbid bias based on gender, age, ethnicity, religion, etc.
* Model selection aligned with hackathon guidelines (no disallowed models).

---

## 6.5 Impact (slide 6)

You can estimate:

* **60–70% reduction** in recruiter time spent on initial screening.
* **Automatic interview scheduling** reduces back-and-forth emails from days → minutes.
* **Standardized onboarding** reduces missed tasks and improves new-hire experience.
* **Transparent decision logs** improve trust and audit readiness.

---

## 6.6 Demo flow (slide 7–8)

1. Recruiter:

   > “Create a hiring pipeline for Senior Java Developer and show me the top 3 candidates.”
2. Coordinator:

   * Calls Screening Agent → rankings
   * Calls Compliance Agent → PASS/WARN
   * Shows ranked list + explanations in chat.
3. Recruiter:

   > “Schedule interviews with the top 2 candidates this week with me and the hiring manager.”
4. Scheduler Agent:

   * Fetches free slots, proposes them, creates meetings.
5. Recruiter:

   > “Mark candidate CAND-001 as hired and start onboarding.”
6. Onboarding Agent:

   * Shows created tickets and generated welcome email.

Capture screen recordings / screenshots of each step.

---

If you’d like, next I can:

* Draft **exact example data** (sample JDs, CVs, onboarding checklist), or
* Help you write the **tool configuration text** to paste into Orchestrate when you register each HTTP tool.
