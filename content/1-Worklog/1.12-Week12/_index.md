---
title: "Week 12 Worklog"

weight: 2
chapter: false
pre: " <b> 1.12. </b> "
--- 


-

### Weekly Objectives

**Part 1 – Introduction to Amazon Bedrock & Foundation Models**

* Understand Amazon Bedrock architecture and key services.
* Learn how to access and use foundation models (FM) via Bedrock.
* Explore model options: Claude, Llama, Mistral, Amazon Titan...
* Learn the difference between text generation, embeddings, and multimodal models.

**Part 2 – Building an AI Agent with Bedrock Agent**

* Understand what a Bedrock Agent is and how it works.
* Learn the concept of:

  * Action groups
  * Knowledge bases
  * Orchestration
  * Lambda function integration
* Configure an AI Agent capable of calling external tools via Lambda.

**Part 3 – Using Knowledge Bases for Enterprise Search**

* Create a Knowledge Base with vector embeddings.
* Connect Bedrock KB to S3 documents.
* Test semantic search and RAG (Retrieval Augmented Generation).
* Integrate the KB into the Bedrock Agent.

**Part 4 – Front-end Integration with Bedrock Agent**

* Build a web UI chat application to communicate with the Bedrock Agent.
* Implement streaming responses.
* Pass user input → Agent → (KB, Lambda Tools) → Response.
* Deploy frontend using Amplify Hosting.

---

### Tasks to be carried out this week:

| Day | Detailed Tasks                                                                                                                                                                                       | Start | Finish | Source                         |
| --- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----- | ------ | ------------------------------ |
| Mon | **Learn Fundamentals of Amazon Bedrock**<br>• Explore model catalog.<br>• Test Claude / Llama 3 in Playground.<br>• Compare pricing & capabilities.<br>• Learn Bedrock API basics.                   | 24/11 | 24/11  | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| Tue | **Build First Bedrock Text Generation App**<br>• Write Lambda calling Bedrock InvokeModel API.<br>• Test temperature, max token params.<br>• Build small CLI app using SDK.                          | 25/11 | 25/11  | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| Wed | **Create Bedrock Agent**<br>• Set up agent configuration.<br>• Add instructions & guardrails.<br>• Create Action Group backed by Lambda.<br>• Connect agent to DynamoDB test table.                  | 26/11 | 26/11  | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| Thu | **Build Knowledge Base (RAG System)**<br>• Create S3 bucket for documents.<br>• Configure embeddings (Titan Embeddings G1).<br>• Test semantic Q&A with PDF/CSV files.<br>• Integrate KB into Agent. | 27/11 | 27/11  |[cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| Fri | **End-to-End AI Agent Testing**<br>• Chat: Agent → KB → Lambda → Return Answer.<br>• Fix permission issues (IAM, kms).<br>• Test multi-turn conversation.<br>• Add fallback and error handling.      | 28/11 | 28/11  | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |                 |
| Sat | **Frontend Chat App using Amplify**<br>• Build React chat UI.<br>• Connect UI to Bedrock Agent API via API Gateway.<br>• Implement streaming output.<br>• Deploy using Amplify Hosting.              | 29/11 | 29/11  | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |

---

### Achievements in Week 12 :

 **1. Strong Understanding of Amazon Bedrock & Foundation Models**

* Learned how to call models using the SDK.
* Tested multiple model families.
* Understood use cases: text generation, summarization, code, embeddings.

---

 **2. Built a Fully Functional AI Agent**

* Agent can understand user intent.
* Uses Action Groups to execute Lambda functions.
* Supports multi-step reasoning and orchestration.
* Agent can retrieve data from DynamoDB via Lambda.

---

 **3. Implemented Knowledge Base with RAG**

* Created a vector store from S3 documents.
* Successfully ran semantic search and contextual Q&A.
* Integrated KB into the agent → more accurate answers.

---

 **4. Created a Web Chat Interface Connected to Bedrock**

* Built a React chat interface.
* Integrated API Gateway for secure communication.
* Implemented real-time response streaming.
* Successfully connected UI → Agent → KB → Lambda → Response.

---

### Summary of Knowledge Gained

 **Amazon Bedrock**

* Provides secure access to leading foundation models.
* Fully managed, scalable, and enterprise-ready.
* Supports text, embeddings, and multimodal models.

 **Bedrock Agents**

* AI Agent can hold conversation, manage context, and call tools.
* Action groups allow integration with real backend systems.
* Guardrails help enforce safety & content filtering.

**Knowledge Bases**

* Vector embeddings enable semantic search.
* KB + Agent = RAG-powered conversational system.
* Automatic sync with S3 documents.

 **Integration & Deployment**

* Lambda for executing backend logic.
* API Gateway for secure access to frontend.
* Amplify for hosting the chat application.

---

