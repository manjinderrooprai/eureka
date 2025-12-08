# TalentFlow Orchestrator
Domain: **Industry Impact + HR + Advanced multi-agent system**. 
Tools: watsonx Orchestrate + watsonx.ai.

---

## 1. One-line pitch

> **“TalentFlow Orchestrator” – a multi-agent HR copilot that automates candidate screening, interview scheduling, and onboarding tasks end-to-end using IBM watsonx Orchestrate and Granite models.**

---

## 2. Problem & impact (for your submission)

### Business problem (HR)

Hiring teams waste time on:

* Manually reading CVs and matching to JDs
* Back-and-forth emails to schedule interviews
* Coordinating onboarding tasks across IT, HR, and managers

### Impact you’ll claim

Your agent:

* **Cuts recruiter manual screening time by 60–70%**
* **Reduces time-to-schedule interviews from days to minutes**
* **Automates 80% of onboarding checklist tasks**

You can present these as *estimated* improvements based on your workflow design.

---

## 3. High-level solution overview

### User roles

* **Recruiter / HRBP**
* **Hiring manager**
* **New hire** (optional in demo)

### Core idea

Use **watsonx Orchestrate** as a **multi-agent coordinator** that:

1. Ingests a job description & a batch of candidate profiles.
2. Uses **watsonx.ai Granite model** (via Prompt Lab or API) to:

   * Extract required skills from JD.
   * Rank and summarize candidates.
3. Triggers different **specialized agents**:

   * Screening Agent
   * Interview Scheduler Agent
   * Onboarding Agent
   * Compliance/Policy Agent (checks for bias & policy alignment).

External tools are connected as app integrations or mocked REST APIs:

* Calendar (Outlook/Google mock)
* Email / notification service
* HRIS / ATS mock API
* Document store (e.g., Cloudant / synthetic JSON data)

---

## 4. Multi-agent design in Orchestrate

### 4.1. **Screening Agent**

**Purpose**

* Read job description
* Parse candidate CVs / profiles
* Score & rank candidates, generate shortlists and summaries.

**Knowledge**

* Synthetic HR job descriptions
* Competency framework docs (skills, levels)
* “Good vs weak profile” examples.

**Tools**

* `get_job_description(job_id)` – mock/REST
* `list_candidates(job_id)` – returns profiles from Cloudant or JSON
* `update_candidate_status(candidate_id, status)`

**LLM tasks (watsonx.ai Granite)**

* Extract required skills from JD
* Match profile skills vs JD, calculate fit score
* Generate 3–4 lines reasoning per candidate

**Outputs**

* Shortlist with scores & rationales
* Suggested personalized email templates to shortlisted candidates.

---

### 4.2. **Interview Scheduler Agent**

**Purpose**
Automate scheduling between recruiter, hiring manager, and candidate.

**Knowledge**

* Working hours rules
* Interview types (screening/technical/HR)

**Tools**

* `get_free_slots(user_id)` – mock Calendar API
* `create_meeting(participants, slot, mode)`
* `send_email(to, subject, body)`

**Flow**

1. Takes list of shortlisted candidates from Screening Agent.
2. Proposes 2–3 time slots based on participants’ calendars.
3. Books the final slot and sends calendar invite & email.

---

### 4.3. **Onboarding Agent**

**Purpose**
Once candidate is marked as “Hired”, automatically trigger onboarding tasks.

**Knowledge**

* Onboarding checklist (HR, IT, Facilities)
* Policy docs (leave, code of conduct, security basics)

**Tools**

* `create_ticket(system, description)` – for tasks like laptop, ID card
* `generate_onboarding_pack(candidate_id)` – uses Granite model to create customized welcome pack summary
* `notify_manager(manager_id, message)`

**Flow**

* Picks up event `status = HIRED`.
* Creates task list in HRIS/ticketing system.
* Generates personalized “Welcome Email + summary of key policies”.

---

### 4.4. **Compliance & Responsible AI Agent**

**Purpose**
Enforce HR policies and responsible AI principles.

**Knowledge**

* HR hiring policy
* Non-discrimination guidelines
* Location-specific rules (simplified)

**Roles**

* Review screening prompts & outputs for bias indicators.
* Red-flag any decision that uses protected attributes (gender, age, etc.).
* Produce a short “Decision log” for audit trail.

**Implementation**

* A separate Orchestrate agent that:

  * Receives screening result JSON.
  * Uses Granite (via watsonx.ai) to check:

    > “Are any protected attributes used as reasons for ranking?”
  * If yes → send warning & mark those sections.
  * Logs decisions to a simple “audit log” (Cloudant / file).

---

### 4.5. **Coordinator / HR Chat Assistant**

In **AI assistant builder**, expose a chat UI where the recruiter can say:

* “Create a new hiring pipeline for Java Developer.”
* “Show me top 5 candidates for Job-123 and schedule interviews this week.”
* “What onboarding tasks are pending for new hires this month?”

This **assistant uses the child agents** above as collaborators.

---

## 5. Technical architecture (IBM stack)

### watsonx Orchestrate

* **Agent Builder** for each agent profile, style, tools, and collaborator links.
* **Multi-agent orchestration** via “Add collaborator agents”.
* **Embedded chat / web widget** for your demo.

### watsonx.ai

* **Prompt Lab** to prototype:

  * JD → skill extraction prompts
  * CV → structured profile extraction
  * Ranking / summarization prompts
* Then **export prompt code** (Python/Node/curl) and wire it into Orchestrate via ADK / custom tool.

### Frameworks (optional but nice)

Use **LangChain** or **LangGraph** as your backend orchestration layer when calling watsonx.ai APIs, then wrap them as tools in Orchestrate. The hackathon guide lists official tutorials for these. 

---

## 6. Data plan (respecting hackathon rules)

To stay compliant:

* Use **synthetic HR data** that you generate yourself:

  * Fake names, emails, profiles
  * Generic job descriptions (no real company IP)
* Store them in:

  * Cloudant
  * JSON in a small backend / local file for mocks

You explicitly **do not** use:

* Real candidate data
* Social media profiles
* Any confidential HR data

You can mention this explicitly in your submission.

---

## 7. Implementation roadmap for the hackathon

### Phase 1 – MVP (Day 1–2)

1. Set up:

   * Access IBM Cloud & watsonx Orchestrate + watsonx.ai (Dallas region).
2. In watsonx.ai Prompt Lab:

   * Create prompts for JD skill extraction and candidate ranking.
   * Save Prompt Session for reuse.
3. In Orchestrate:

   * Build **Screening Agent**:

     * Profile, style, Granite model, knowledge docs.
     * Mock tools for `get_job_description`, `list_candidates`.
   * Test via Orchestrate Chat.

### Phase 2 – Multi-agent + Scheduling (Day 2–3)

1. Add **Interview Scheduler Agent** and required tools.
2. Configure **Coordinator Assistant** that:

   * Accepts recruiter intent and delegates to the right agent.
3. Wire up basic calendar/email mocks (can just log “meeting created” to a console or table).

### Phase 3 – Onboarding + Compliance (Day 3–4)

1. **Onboarding Agent** with ticket creation + onboarding email generation.
2. **Compliance Agent** to validate decisions & produce simple audit logs.
3. Demonstrate responsible AI flow:

   * Show a biased example → agent flags it.
   * Show a corrected, compliant result.

### Phase 4 – Polish & Demo (Day 4–5)

* Create 2–3 clean demo scenarios:

  1. New role creation → shortlist & schedule interviews.
  2. Hiring event → automated onboarding.
  3. Compliance check → bias detection.
* Prepare slides:

  * Problem, architecture, agents, demo screenshots, metrics.

---

## 8. Storytelling for judges (how you’ll present)

Structure your pitch:

1. **Problem** – “HR teams spend X hours per week on manual hiring steps.”
2. **Solution** – “TalentFlow Orchestrator, built on IBM watsonx Orchestrate + watsonx.ai.”
3. **Architecture** – Show agents & tools diagram.
4. **Demo** – Live run-through of the 3 scenarios above.
5. **Impact** – Time saved, faster hiring, better candidate experience.
6. **Responsible AI** – Compliance Agent, audit logs, no PII, synthetic data.
7. **Scalability** – Can extend to internal mobility, performance reviews, etc.

---

## 9. What I can do for you next

In the next messages I can:

* Draft **exact agent descriptions, styles, and instructions** for Orchestrate.
* Design **Prompt Lab prompts** for:

  * JD → skills
  * CV → structured info
  * Candidate ranking & summarization
* Sketch **pseudo-API schemas** for tools (JSON request/response) you can implement or mock.
* Help you write **documentation & pitch deck content**.

If you tell me:

* Whether you’ll use **Python or Node** for APIs/tools
* Which calendar/email system you want to mock (Google vs Outlook vs generic),

I’ll generate **concrete prompt text + code skeletons** you can plug into watsonx.ai and Orchestrate.
