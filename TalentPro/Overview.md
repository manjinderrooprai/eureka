## 🎯 **Overview**
The goal is to build an intelligent platform called **"TalentPro"** that automates the process of **skill assessment, role categorization**, and **talent matching** using AI and analytics.

## 🧠 **Background**

Currently, assessing employee skills and mapping them to appropriate roles/projects is **manual and time-consuming**. The proposed platform will:

* Analyze data from **GitHub**, **resumes**, **internal APIs**, and **Lex (Knowledge Graph)**
* Use **Generative AI** to create a **Skill Proficiency Matrix**
* Enable **talent managers** to interact through a **chatbot** to find suitable profiles

## ⚙️ **Technical Challenges**

1. Extracting insights from **GitHub commit history**
2. Integrating **multiple data sources** (GitHub, internal APIs, Lex KG)
3. Parsing resumes accurately
4. Designing a **skill proficiency scoring algorithm**
5. Implementing a **chatbot** for talent managers
6. Ensuring **scalability and performance**

## 👥 **Key Stakeholders**

* Employees (Developers, Analysts, etc.)
* Talent Managers
* HR
* Learning & Development team

## 💡 **Solution Features**

### ✅ Must-Haves:

1. **GitHub Analysis**

   * Employees select repos
   * Commit history analyzed to build skill matrix
   * Combined with resume and Lex data

2. **Employee Persona**

   * Logs in, provides GitHub ID, uploads resume
   * GenAI processes all data to create:

     * Skill proficiency matrix
     * Role categorization

3. **Talent Manager Persona**

   * Interacts via chatbot
   * Specifies talent needs
   * Chatbot fetches **top 10 matching employee profiles**

4. **Data Integration**

   * Internal API: Enrich skills
   * Lex: Recommend skills from Knowledge Graph
   * Resume Parsing: Extract skills & proficiency

5. **Skill Proficiency Matrix**

   * Categorize skills as:

     * Beginner
     * Competent
     * Proficient
     * Expert

6. **Role Categorization**

   * Map employees to predefined roles like:

     * Developer, Admin, Architect, Tester, BA, DA, etc.

7. **Talent Manager Chatbot**

   * Conversational AI for profile matching and role requirement handling

### ⭐ Good-to-Have:

* **Talent Mapping Ratio Configurator** (e.g., 1:2:5:8 ratio of Expert to Beginner)
* **Enhanced Chatbot UX**

## 🔍 **Existing Solutions for Reference**

* TMS
* LinkedIn Talent Insights

## 🧰 **Technology Requirements**

### ✅ Software:

* **Backend**: Python, FastAPI, LangChain
* **NLP**: spaCy, NLTK
* **LLMs**: Any foundation model
* **Agentic Frameworks**: Semantic Kernel, LangGraph, CrewAI, LlamaStack
* **Vector DBs**: FAISS, Chroma
* **Frontend**: React or Angular

### ✅ Hardware:

* Not specified (assumed cloud/development machine access)

## 🧪 **Testing & Validation**

* **Accuracy Testing**:

  * Input-output validation based on pre-defined queries
* **Datasets Provided** (to be shared separately):

  * Masked Lex JSON (Knowledge Graph)
  * Masked Internal Skills API JSON
  * Sample GitHub repos
  * Sample resumes (PDF/DOCX)

## 🧾 **Evaluation Criteria**

| Category                     | Weight |
| ---------------------------- | ------ |
| Creativity (newness of idea) | 10%    |
| Innovative use of technology | 20%    |
| UX and functionality         | 10%    |
| Simplicity                   | 10%    |
| Feasibility / Impact / Reuse | 30%    |
| Progress in a day            | 10%    |
| Demo & presentation quality  | 10%    |

