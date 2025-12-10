Excellent — now that Gmail is fully working, we can run a **complete end-to-end test** of your entire multi-agent HR system using **TalentFlow Orchestrator**, exactly as the hackathon judges will expect.

Below is the **official full-system test script**, covering:

* Screening
* Compliance check
* Interview scheduling
* Email sending
* Onboarding workflow
* Welcome email sending

You can paste each block **directly into TalentFlow Orchestrator (Preview)**.

---

# ✅ **STEP 1 — Screen Candidates**

Paste:

```
Screen candidates for JOB-2025-JAVA-SR.
```

Expected Orchestrator behavior:

1. Calls HR Screening Agent
2. Receives JSON with:

   * candidate_id
   * candidate_name
   * fit_score
   * top_3_reasons
3. Calls Compliance Agent with that JSON
4. Returns a combined summary:

   * Ranked candidates
   * Fit scores
   * Compliance PASS/WARN/FAIL
5. Stores candidate data for later use

Let me know the output you get.

---

# ✅ **STEP 2 — Ask for Compliance Separately (Optional Check)**

Paste:

```
Check compliance for the screened candidates.
```

Expected:

* Orchestrator uses stored JSON
* Compliance Agent returns:

  * compliance_status
  * issues[]
  * audit_summary

---

# ✅ **STEP 3 — Schedule Interview**

To test scheduling:

```
Schedule an interview with the top candidate for tomorrow at 13:00 IST. 
Use rooprai0044@gmail.com as the candidate email.
```

Expected:

1. Orchestrator checks memory → retrieves the top candidate (Arjun Mehta)
2. Calls Interview Scheduler Agent
3. Scheduler:

   * Applies defaults (30 min, IST, [hr@talentflow.com](mailto:hr@talentflow.com), [manager@talentflow.com](mailto:manager@talentflow.com))
   * Sends interview invitation email via Gmail
4. You receive an email in your inbox
5. Orchestrator summarizes:

```
Interview scheduled for CAND-001 at 13:00 IST tomorrow.
Email sent to rooprai0044@gmail.com.
```

---

# ✅ **STEP 4 — Begin Onboarding**

Paste:

```
Hire CAND-001 for the Senior Java Developer role. 
Start onboarding on 2025-12-20. 
Send the welcome email to rooprai0044@gmail.com.
```

Expected:

1. Orchestrator retrieves candidate_name from memory
2. Asks clarifying questions **only if needed**
3. Calls Onboarding Automation Agent with:

   * candidate_id
   * candidate_name
   * role
   * start_date
   * email
4. Onboarding Agent:

   * Generates onboarding JSON
   * Sends welcome email via Gmail
5. You receive "Welcome to the team!" email
6. Orchestrator returns:

```
Onboarding initiated for Arjun Mehta.
Welcome email sent.
Here is the onboarding plan…
```

---

# 🚀 **STEP 5 — Full Multi-agent Workflow Confirmation**

Finally paste:

```
Summarize the entire hiring workflow for JOB-2025-JAVA-SR.
```

The Orchestrator should produce a clean narrative:

* Screening results
* Compliance results
* Interview details
* Onboarding summary

This is your **hackathon demo “final output”**.

---

# ⭐ YOU ARE NOW READY TO RUN THE FULL TEST

Please run:

### **1. Screen**

### **2. Schedule**

### **3. Onboard**

Paste each Orchestrator output here, and I will verify correctness + fix any inconsistencies instantly.

Ready when you are.
