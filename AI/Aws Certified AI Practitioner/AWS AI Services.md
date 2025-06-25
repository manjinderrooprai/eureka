Great! Here's the **extended table** combining **AI/ML tools** and **Security, Compliance & Governance services** relevant for the **AWS Certified AI Practitioner** exam.

---

## ✅ **Complete Table: AI/ML + Security & Governance Services for AWS AI Practitioner**

| **Service Name**                     | **Category**                       | **Definition**                                           | **Use Cases**                                      | **Key Features**                                               |
| ------------------------------------ | ---------------------------------- | -------------------------------------------------------- | -------------------------------------------------- | -------------------------------------------------------------- |
| **Amazon SageMaker**                 | ML Platform                        | Build, train, and deploy custom ML models                | End-to-end ML pipeline                             | Managed Jupyter, pipelines, endpoints                          |
| **SageMaker Autopilot**              | AutoML                             | Automatically train and tune ML models from tabular data | ML for non-experts                                 | Generates notebooks, explainability and bias detection         |
| **SageMaker Clarify**                | Explainability / Fairness          | Detects bias and explains predictions using SHAP         | Fairness audits, regulatory requirements           | Pre- and post-training bias reports, integrated with Autopilot |
| **SageMaker Data Wrangler**          | Data Preparation                   | Visual tool for data preprocessing and transformation    | Feature engineering, cleaning                      | 300+ transforms, integrates with Athena, S3                    |
| **SageMaker Model Cards**            | Model Governance                   | Document model details, risks, and intended use          | Transparency, audits                               | Risk ratings, lineage, metrics                                 |
| **SageMaker Model Dashboard**        | Monitoring & Drift Detection       | View all deployed model performance                      | Detect performance drift, fairness                 | Integrated with Clarify                                        |
| **SageMaker Role Manager**           | Access Control                     | Persona-based IAM role setup for ML                      | Simplified secure access for ML teams              | Role templates, least-privilege policies                       |
| **Amazon Bedrock**                   | Foundation Model Hosting           | Host LLMs via API (e.g., Claude, Llama, Titan)           | Prompt-based GenAI use                             | Fine-tuning, Guardrails, Service Cards                         |
| **Bedrock Guardrails**               | Responsible AI / GenAI Safety      | Set policies to prevent unsafe LLM output                | Remove harmful, biased, or toxic responses         | Filters for profanity, hate, sensitive topics                  |
| **AI Service Cards**                 | Model Transparency (Bedrock)       | Human-readable model summaries for Bedrock models        | Understand model behavior, limitations             | Covers training data, bias, use cases                          |
| **Amazon Kendra**                    | Intelligent Search                 | ML-powered search for enterprise data                    | Internal portals, document search                  | Connectors, semantic ranking                                   |
| **Amazon Personalize**               | Recommendations                    | Build personalized user experiences                      | Product/content recommendations                    | Real-time ranking, behavior-based                              |
| **Amazon Forecast**                  | Time Series Forecasting            | Predict future values from time series data              | Inventory, demand planning                         | Quantile forecasts, supports related time series               |
| **Amazon Rekognition**               | Computer Vision                    | Image and video analysis                                 | Face matching, moderation, object detection        | Real-time or batch analysis                                    |
| **Amazon Comprehend**                | NLP                                | Extract meaning from unstructured text                   | Sentiment, entity, key phrase detection            | Multilingual, topic modeling                                   |
| **Amazon Polly**                     | Text-to-Speech                     | Convert text into lifelike speech                        | Voice assistants, IVR, accessibility               | Neural voices, SSML                                            |
| **Amazon Lex**                       | Conversational AI                  | Build chatbots with speech/text                          | Virtual agents, customer support                   | Same tech as Alexa                                             |
| **Amazon Translate**                 | Translation                        | Real-time text translation                               | Localization, multilingual apps                    | Custom terminology, batch or real-time                         |
| **Amazon Transcribe**                | Speech-to-Text                     | Converts audio to text                                   | Call analytics, subtitles                          | Streaming, speaker labeling                                    |
| **Amazon Titan / Claude / Llama**    | Foundation Models                  | Foundation models via Bedrock                            | Summarization, Q\&A, creative generation           | Prompt APIs, hosted securely                                   |
| **Amazon S3**                        | Storage                            | Scalable object storage                                  | Store datasets, model artifacts                    | Versioning, encryption                                         |
| **Amazon Athena**                    | Serverless SQL                     | Query data in S3 with SQL                                | Ad hoc analysis, model input prep                  | Pay-per-query                                                  |
| **Amazon Glue**                      | Data Integration                   | Serverless ETL                                           | Move data to lake or SageMaker                     | Data catalog, Spark jobs                                       |
| **AWS Lambda**                       | Serverless Compute                 | Run code on-demand                                       | Event-based ML logic                               | Supports Python, Node.js                                       |
| **AWS Step Functions**               | Workflow Orchestration             | Chain steps in ML pipelines                              | Build reproducible ML workflows                    | Visual builder, retries                                        |
| **Amazon QuickSight**                | Visualization & BI                 | Create dashboards for ML insights                        | View predictions, business metrics                 | ML-powered anomaly detection                                   |
| **AWS CloudTrail**                   | Governance / Audit Logging         | Record all AWS API calls and events                      | Track who accessed ML models or data               | Centralized logging, S3 export                                 |
| **AWS Config**                       | Compliance Monitoring              | Continuously monitors AWS resource compliance            | Ensure SageMaker and S3 configurations meet policy | Rule-based auditing, history tracking                          |
| **Amazon Inspector**                 | Security Assessment                | Automated security scanning for EC2 and containers       | Check vulnerabilities in ML compute environments   | CVE checks, integration with ECR                               |
| **AWS Audit Manager**                | Compliance Reporting               | Automates evidence collection for audits                 | Compliance with ISO, SOC, GDPR                     | Frameworks for industry standards                              |
| **AWS Artifact**                     | Compliance Docs & Agreements       | Central portal for AWS compliance reports                | Show SOC, PCI, HIPAA compliance                    | Download security whitepapers and audit reports                |
| **AWS Trusted Advisor**              | Cost, Security, Performance Checks | Recommends best practices across AWS accounts            | Identify risks in ML infrastructure                | Covers security, fault tolerance, cost optimization            |
| **AWS Security Hub**                 | Security Posture Management        | Unified security dashboard                               | Central view for Inspector, GuardDuty, Macie       | Aggregates findings, compliance checks                         |
| **AWS Key Management Service (KMS)** | Encryption                         | Create and manage cryptographic keys                     | Encrypt S3 training data, SageMaker artifacts      | Integration with most AWS services                             |
| **Amazon GuardDuty**                 | Threat Detection                   | Monitors AWS accounts for malicious activity             | Detect unusual activity on SageMaker, S3, IAM      | Uses ML to detect threats                                      |
| **AWS Shield Advanced**              | DDoS Protection                    | Protects applications from large-scale DDoS attacks      | Protect ML APIs and inference endpoints            | Always-on detection, 24/7 DDoS response team                   |
| **Amazon Macie**                     | Data Privacy                       | Detects sensitive data like PII in S3                    | Privacy protection for ML datasets                 | Automated PII classification                                   |

---

### 🧠 Grouped by Function (Exam Tip Sheet):

| **Category**                  | **Services**                                                                                |
| ----------------------------- | ------------------------------------------------------------------------------------------- |
| **ML Build & Train**          | SageMaker, Autopilot, Data Wrangler, Clarify                                                |
| **Foundation Models (GenAI)** | Bedrock, Titan, Claude, Guardrails, AI Service Cards                                        |
| **Vision/NLP/Speech**         | Rekognition, Comprehend, Lex, Polly, Transcribe, Translate                                  |
| **Data Prep & Storage**       | Glue, Athena, S3, Lambda, Step Functions, QuickSight                                        |
| **Governance & Docs**         | Model Cards, Model Dashboard, Role Manager, AI Service Cards, Artifact, Audit Manager       |
| **Monitoring & Security**     | CloudTrail, Config, Inspector, GuardDuty, Shield, KMS, Trusted Advisor, Macie, Security Hub |
| **Compliance Tools**          | Audit Manager, Artifact, Config, Trusted Advisor                                            |


