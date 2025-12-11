# 1. **Test All Agents Individually First**

This ensures each agent works before combining them.

## **1.1 Test: Google Drive Utility Agent (GDUA)**

This must be tested first because the entire workflow depends on resume access.

### **Test 1: List files**

Prompt the GDUA directly:

```
List all files in this folder: <your_folder_url_or_ID>.
```

Expected:

* Returns file IDs, names, MIME types.

### **Test 2: Retrieve one file**

```
Retrieve and summarize the resume: <file_name>.
```

Expected:

* The agent fetches, exports (if Google Doc), and returns a clean summary.

### **Test 3: Summarize all resumes**

```
List and summarize all resumes in folder <folder_id>.
```

Expected:

* Returns structured summaries for each resume.

If this agent passes all tests → your Drive connection + scopes + token + tools are correct.

---

## **1.2 Test: HR Screening Agent**

Call it **alone** with your own resume summaries.

Example:

```
Screen candidates for JOB-2025-JAVA-SR using the following resume summaries:
- Candidate A: 6 years Java, Spring Boot...
- Candidate B: 4 years Java...
```

Expected:

* Ranked shortlist
* Fit scores
* Reasoning and risk flags

---

## **1.3 Test: HR Compliance & Fairness Agent**

```
Check compliance for this screening result:
<insert screening JSON>
```

Expected:

* PASS / WARN / FAIL
* Issues list
* Clean explanation

---

## **1.4 Test: Interview Scheduler Agent**

Simulate scheduling with manual inputs:

```
Schedule an interview for CAND-001 with interviewer hr@company.com tomorrow at 3pm IST.
```

Expected:

* Ask for confirmation
* Upon confirmation, send email via Gmail connector
* Return ICS data

---

## **1.5 Test: Onboarding Automation Agent**

```
Start onboarding for CAND-001 (John Doe) starting 2025-01-20 at john.doe@company.com for Software Engineer role.
```

Expected:

* Onboarding plan JSON
* Welcome email ready or sent

If these 5 agents all behave correctly → **you are ready for system integration.**

---

# 2. **Test the TalentFlow Orchestrator in Isolation (Without Delegation)**

Before connecting specialist agents, test **intent detection only**.

### Test prompts:

```
Screen candidates for JOB-2025-JAVA-SR.
Schedule interviews for top candidates.
Hire CAND-001 and start onboarding.
```

Expected:

* Orchestrator recognizes correct agent to call
* Asks for missing inputs (folder, job_id, date, email)
* Does NOT perform tasks itself
* Does NOT invent tools or agents

If intent routing is correct → move to full integration.

---

# 3. **Full Integrated Workflow Testing**

Now connect all agents and test the complete pipeline.

---

## **3.1 End-to-End Test: Screening Workflow**

Use Orchestrator (not individual agents):

### Test Prompt:

```
Screen all candidates for JOB-2025-JAVA-SR using resumes from my Google Drive folder.
```

Expected workflow behind the scenes:

1. Orchestrator asks for folder (if needed)
2. Calls Google Drive Utility Agent → summaries
3. Calls HR Screening Agent → shortlist
4. Calls Compliance Agent → PASS/WARN/FAIL
5. Returns combined result

If Orchestrator calls agents in the wrong order → update instructions.

---

## **3.2 End-to-End Test: Interview Scheduling Workflow**

After screening:

```
Schedule interviews for the top 2 candidates.
```

Expected:

1. Orchestrator identifies candidates
2. Asks for confirmation
3. Calls Interview Scheduler Agent
4. Returns schedule summary + ICS

---

## **3.3 End-to-End Test: Onboarding Workflow**

After screening:

```
Hire all candidates for JOB-2025-JAVA-SR and start onboarding.
```

Correct behavior:

1. Orchestrator checks if screening exists
2. If missing, re-runs Drive → Screening → Compliance
3. Asks for start date
4. Asks for email domain
5. Asks for confirmation
6. Calls Onboarding Agent for each candidate
7. Returns onboarding summary

If you see:

* Orchestrator skipping Drive Utility Agent
* Orchestrator skipping screening
* Missing resume summaries

Then the Orchestrator instructions must be corrected.

---

# 4. **System Validation Checklist**

Use this to verify everything is configured correctly:

| Component                  | What to Validate                      | Status                |
| -------------------------- | ------------------------------------- | --------------------- |
| Google Drive Utility Agent | Can list, retrieve, summarize resumes | Should pass first     |
| OAuth Connection           | Token refresh works                   | Fix scopes if failing |
| HR Screening Agent         | Accepts summaries, produces shortlist | Independent test      |
| Compliance Agent           | Flags issues correctly                | Independent test      |
| Scheduler Agent            | Sends Gmail emails                    | Independent test      |
| Onboarding Agent           | Generates onboarding package          | Independent test      |
| Orchestrator               | Delegates correctly                   | Final stage           |

**“Give me the debugging checklist”** or
**“Generate test resumes.”**
