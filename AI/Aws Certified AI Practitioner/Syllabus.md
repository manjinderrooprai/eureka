Here is the **complete syllabus** for the **AWS Certified AI Practitioner (AIF-C01)** exam, organized **domain-wise**, with **each topic you need to learn clearly listed**:

---

## 🧠 Domain 1: Fundamentals of AI and ML (20%)

### ✅ 1.1 Explain basic AI concepts and terminologies

* Definitions of:

  * AI, ML, Deep Learning, Neural Networks
  * Computer Vision, Natural Language Processing (NLP)
  * Model, Algorithm, Training, Inferencing
  * Bias, Fairness, Overfitting, Underfitting, Large Language Models (LLMs)
* Types of inferencing: batch vs. real-time
* Types of data: labeled/unlabeled, structured/unstructured, image/text/time-series
* Types of ML:

  * Supervised Learning
  * Unsupervised Learning
  * Reinforcement Learning

### ✅ 1.2 Identify practical use cases for AI

* Value of AI/ML: decision support, automation, scalability
* When AI/ML is **not** appropriate (cost-benefit, deterministic outcomes)
* ML techniques by use case:

  * Regression, Classification, Clustering
* Real-world applications: recommendation systems, fraud detection, forecasting
* AWS AI/ML services:

  * SageMaker, Amazon Transcribe, Translate, Comprehend, Lex, Polly

### ✅ 1.3 Describe the ML development lifecycle

* Pipeline stages:

  * Data collection, EDA, preprocessing, feature engineering
  * Model training, hyperparameter tuning, evaluation
  * Deployment and monitoring
* ML model sources: pre-trained vs. custom-trained
* Model deployment: managed API vs. self-hosted
* AWS tools:

  * SageMaker, Data Wrangler, Feature Store, Model Monitor
* MLOps basics: reproducibility, automation, technical debt, retraining
* Model evaluation:

  * Accuracy, F1 score, AUC
  * Business metrics: ROI, cost/user, customer feedback

---

## 🤖 Domain 2: Fundamentals of Generative AI (24%)

### ✅ 2.1 Explain the basic concepts of generative AI

* Key concepts:

  * Tokens, Embeddings, Vectors, Prompt Engineering
  * Transformer models, Diffusion models, Foundation Models
* Generative AI use cases:

  * Text/image/audio/video generation, summarization, translation
  * Code generation, search, chatbots, recommendation
* Lifecycle:

  * Data selection, model selection, pre-training, fine-tuning, evaluation, feedback

### ✅ 2.2 Capabilities and limitations of generative AI

* Advantages: adaptability, responsiveness, simplicity
* Limitations: hallucinations, inaccuracy, lack of interpretability
* Factors for model selection: latency, performance, compliance, capabilities
* Business value metrics: user engagement, efficiency, conversion rate, CLTV

### ✅ 2.3 AWS infrastructure & services for generative AI

* Services:

  * Amazon Bedrock, PartyRock, Amazon Q, SageMaker JumpStart
* Benefits of AWS services:

  * Cost-effective, scalable, fast time-to-market, secure, compliant
* Cost trade-offs:

  * Regional coverage, token-based pricing, performance, redundancy

---

## 🏗️ Domain 3: Applications of Foundation Models (28%)

### ✅ 3.1 Design considerations for foundation model applications

* Model selection criteria:

  * Latency, cost, size, modality, customization, multilingual support
* Inference parameters:

  * Temperature, input/output length
* Retrieval Augmented Generation (RAG): concepts & business use cases
* Vector database services:

  * Amazon OpenSearch, Aurora, Neptune, DocumentDB, RDS for PostgreSQL
* Customization trade-offs:

  * Pre-training, fine-tuning, in-context learning, RAG
* Role of **agents** for multi-step tasks: Agents for Amazon Bedrock

### ✅ 3.2 Prompt engineering techniques

* Concepts: instruction, context, negative prompts, latent space
* Techniques:

  * Zero-shot, One-shot, Few-shot, Chain-of-thought, Templates
* Best practices:

  * Guardrails, specificity, clarity, experimentation
* Risks:

  * Jailbreaking, prompt injection, poisoning, hijacking

### ✅ 3.3 Training and fine-tuning foundation models

* Key elements:

  * Pre-training, fine-tuning, continuous training
* Fine-tuning methods:

  * Transfer learning, instruction tuning, domain-specific training
* Data prep for fine-tuning:

  * Curation, labeling, representativeness, RLHF

### ✅ 3.4 Evaluate foundation model performance

* Evaluation methods:

  * Human evaluation, benchmarks
* Metrics:

  * ROUGE, BLEU, BERTScore
* Business alignment:

  * Productivity, task completion, user engagement

---

## 🛡️ Domain 4: Guidelines for Responsible AI (14%)

### ✅ 4.1 Develop responsible AI systems

* Principles:

  * Fairness, bias, inclusivity, safety, robustness, truthfulness
* Tools:

  * SageMaker Clarify, A2I, Guardrails for Bedrock
* Dataset quality: diversity, balance, curation
* Model risks:

  * Legal concerns (IP, hallucinations, user harm)
* Bias & variance impacts: demographic fairness, accuracy
* Monitoring bias: audits, subgroup analysis, label quality

### ✅ 4.2 Transparent & explainable models

* Transparent vs. black-box models
* Tools:

  * Model Cards, open-source licenses, data transparency
* Trade-offs: interpretability vs. performance
* Human-centered design principles

---

## 🔐 Domain 5: Security, Compliance, Governance (14%)

### ✅ 5.1 Secure AI systems

* AWS services:

  * IAM roles/policies, Macie, PrivateLink, KMS, Secrets Manager
* Security principles:

  * Encryption (at rest/in-transit), data integrity, threat detection
* Best practices:

  * Data quality checks, privacy-enhancing tech, source citation (data lineage)

### ✅ 5.2 Governance and compliance

* Standards:

  * ISO, SOC, Algorithmic Accountability Laws
* AWS governance tools:

  * AWS Config, Audit Manager, Artifact, CloudTrail, Trusted Advisor
* Governance protocols:

  * Data lifecycle, logging, monitoring, retention
  * Team training, policy frameworks, GenAI Security Scoping Matrix

