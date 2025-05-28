# Roadmap

## 🚧 **PHASE 1: PLANNING & ENVIRONMENT SETUP**

### 🔹 Objectives:

* Understand problem statement & stakeholder needs
* Define high-level architecture
* Set up development environment

### ✅ Tasks:

* Set up GitHub repo, branch policies
* Choose tech stack:

  * **Python (FastAPI)** for backend
  * **React** for frontend
  * **LangChain / Semantic Kernel / CrewAI** for GenAI workflows
  * **FAISS/Chroma** for vector storage
* Prepare mock APIs & JSONs for testing
* Get sample data from problem owners

## 📊 **PHASE 2: DATA INGESTION & ENRICHMENT**

### 🔹 Objectives:

* Integrate multiple data sources
* Parse and normalize skills data

### ✅ Tasks:

1. **Resume Parsing**

   * Extract skills, education, experience
   * Use NLP libraries: `spaCy`, `PyPDF2`, `docx2txt`

2. **GitHub Commit Analysis**

   * Use GitHub API to get commit history
   * Analyze for skill keywords (file types, keywords, commit messages)

3. **Infosys Lex Integration**

   * Parse Lex JSON to identify skill relationships from Knowledge Graph

4. **Internal Skill API Integration**

   * Ingest masked JSONs and map to employees

5. **Data Model**

   * Normalize data to common format:

     ```json
     {
       "employee_id": "E123",
       "skills": {
         "Java": "Proficient",
         "React": "Competent"
       },
       "source": ["Resume", "GitHub", "Lex", "Internal API"]
     }
     ```

## 🤖 **PHASE 3: AI/LLM & SKILL MATRIX ENGINE**

### 🔹 Objectives:

* Use GenAI to create a skill proficiency matrix and map roles

### ✅ Tasks:

1. **Skill Scoring Algorithm**

   * Combine weights from different sources
   * Map to 4 levels: Beginner, Competent, Proficient, Expert

2. **Role Categorization Engine**

   * Use rules + LLM to classify employees into:

     * Developer, Tester, Admin, Architect, Analyst, etc.

3. **Top Match Engine**

   * Generate matching scores between talent requirement & profiles
   * Use vector search if needed for semantic matching

4. **GenAI Wrappers**

   * Use **LangChain / Semantic Kernel** to call LLMs (OpenAI, LLaMA, etc.)
   * Use **Prompt templates** and **tool agents**

## 🛠️ **PHASE 4: BACKEND DEVELOPMENT**

### 🔹 Objectives:

* Build APIs to power the platform

### ✅ Tasks:

* **FastAPI Services**

  * `/upload-resume`
  * `/analyze-github`
  * `/generate-skill-matrix`
  * `/get-matching-profiles`
  * `/role-categorization`
* **Authentication**

  * Basic login/session for employee & talent manager
* **Vector DB Integration**

  * Store embeddings from GitHub/resume/skills

## 🌐 **PHASE 5: FRONTEND DEVELOPMENT**

### 🔹 Objectives:

* Build Employee and Talent Manager interfaces

### ✅ Employee Persona UI:

* Login → Upload Resume → Enter GitHub ID → Select Repos
* View Skill Matrix & Role Prediction

### ✅ Talent Manager Persona UI:

* Login → Chatbot Interface → Specify Role Needs
* View Top 10 Matching Profiles

### ✅ Tech:

* **ReactJS** + **Tailwind CSS** or **MUI**
* State Management: Redux / Zustand

## 💬 **PHASE 6: CHATBOT DEVELOPMENT**

### 🔹 Objectives:

* Build conversational interface for Talent Managers

### ✅ Tasks:

* Use **LangChain agents** or **LLMs** (GPT, Claude, etc.)
* Chatbot Flow:

  1. Clarify number of employees
  2. Ask for skill-level expectations
  3. Respond with top 10 matches (and expert\:beginner ratio if configured)
* Use OpenAI functions, CrewAI tools, or LlamaStack for tool-based flows

## 🧪 **PHASE 7: TESTING, VALIDATION & DEPLOYMENT**

### ✅ Functional Testing:

* Test all endpoints with mock data
* Validate skill matrix and role prediction accuracy

### ✅ Chatbot Testing:

* Test queries like:

  * “I need 3 experts in Python and 5 beginners in React”
  * “Find me backend developers with Kubernetes knowledge”

### ✅ Dataset Testing:

* Use:

  * Masked Lex JSON
  * Masked Employee Skillset JSON
  * GitHub commit history
  * Sample resumes

### ✅ Evaluation:

* Build presentation showing:

  * Architecture diagram
  * Skill Matrix samples
  * Chatbot conversation flows
  * Matching algorithm logic

### ✅ Deployment (Optional):

* Deploy backend on **Render / Vercel / EC2**
* Use Docker if needed

## 🧱 **Timeline Suggestion (7 Days)**

| Day   | Focus Area                             |
| ----- | -------------------------------------- |
| Day 1 | Planning, Setup, Mock APIs             |
| Day 2 | Resume Parsing, GitHub Analysis        |
| Day 3 | Skill Scoring Engine, Lex Integration  |
| Day 4 | Role Categorization, FastAPI Endpoints |
| Day 5 | Frontend (Employee + Talent Manager)   |
| Day 6 | Chatbot Development, LLM Integration   |
| Day 7 | Testing, Tuning, Demo Prep             |

