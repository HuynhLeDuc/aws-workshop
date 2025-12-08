---
title: "Event 2"

weight: 1
chapter: false
pre: " <b> 4.2. </b> "
---



# Summary Report: “Generative AI with Amazon Bedrock”

### Workshop Objectives

- Provide basic knowledge about Generative AI and its differences from classical Machine Learning.
- Describe in detail the Amazon Bedrock service and Foundation Models.
- Guide to RAG (Retrieval Augmented Generation) techniques to develop intelligent, accurate AI applications and minimize illusion errors.
- Introduce the system of specialized AI services of AWS.
### List of presenters

- **Lam Tuan Kiet** - Senior DevOps Engineer, FPT Software.
- **Danh Hoang Hieu Nghia** - AI Engineer, Renova Cloud.
- **Dinh Le Hoang Anh** - Cloud Engineering Intern, First Cloud AI Journey.

### Main content

#### Transformation trends: Traditional ML models and Background models

- **Traditional ML models**: Focus on specific tasks, require labeled data, complex training/deployment processes for each target.

- **Background models (FM)**: Trained on huge amounts of unstructured data, adaptable for many different tasks such as: Text generation, summarization, Q&A, Chatbot.

### AI ecosystem on AWS platform

- **Amazon Bedrock**: Platform that gathers leading FM models from AWS partners (AI21 Labs, Anthropic, Cohere, Meta, Stability AI,...) and Amazon's own models.

- **AWS Specialized AI Services**: Can be considered as "off-the-shelf solutions", optimized for each specific task without the need to train a model:

- Amazon Rekognition: Object recognition, Face recognition, Emotion recognition, Celebrity recognition, Video analysis - $0.001/image for the first 1 million images.

- Amazon Translate: Real-time multilingual text translation with high accuracy and natural writing style.

- Amazon Textract: Extract structured information (tables, forms) from scanned documents or PDFs.

- Amazon Transcribe: Convert speech to text.

- Amazon Polly: Convert text to speech.

- Amazon Comprehend: Text sentiment analysis, keyword extraction and automatic topic classification.

- Amazon Kendra: Enables natural language search of internal documents.

- Amazon Lookout: Detect anomalies in production lines or industrial equipment for predictive maintenance.

- Amazon Personalize: Build real-time recommendation systems based on machine learning.

#### Prompting Technique: Chain of Thought (CoT)

- Comparison between **Standard Prompting** (directly asking for the result) and **Chain of Thought Prompting**.

- CoT guides the reasoning model step by step to solve complex logic problems, significantly improving accuracy compared to just providing the final answer.

#### RAG (Retrieval Augmented Generation) Technique – Technical Focus

- **Problem**: Solve the "illusion" and lack of updated information of LLM models.

- **Solution**: Combine the retrieval ability (Retrieval) from an external Knowledge Base with the generation ability (Generation) of LLM.
- **Data Ingestion Process**:
1. Raw data (New data) → Chunking.
2. Process via Embedding Model (e.g. Amazon Titan Text Embeddings V2.0).
3. Store as vectors in Vector Repositories (OpenSearch Serverless, Pinecone, Redis...).
- **RetrieveAndGenerate API**: API manages the entire process from receiving user input → creating query embedding → retrieving data → adding context (augment prompt) → generating answers.

### Acquired knowledge
#### About AI Thinking and Cloud

- Understand when to use **Specialized AI Services** for quick, specific problems and when to use **Bedrock/GenAI** for creative, complex problems.

- Master RAG system design thinking: It's not just about calling LLM APIs, but about data management and vectorization to provide the correct context for AI to generate better responses.

#### About Technical Architecture

- **CoT Technique** is the key to optimizing model output without fine-tuning.

- Deep understanding of the role of **Amazon Titan Embeddings V2.0** in converting multilingual text to vectors (supports 100+ languages, flexible vector size 256/512/1024).

### Work application plan
- Amazon Bedrock applications for current projects: Amazon Rekognition to recognize dishes from photos to automatically fill in calorie information; Amazon Comprehend to analyze text to standardize dish names and record calorie data.
- Experiment with applying RAG techniques for current projects.
- Use Bedrock Agents to coordinate tasks such as querying dishes from vector warehouses, calculating calorie targets, and building daily menus.

### Event participation experience
Participating in the Generative AI workshop with Amazon Bedrock provides a practical perspective on how to build modern AI applications, from fundamental theory to practical implementation.

### Practical knowledge from experts
- The speakers clearly presented the data flow in a **RAG** ​​system, helping me visualize the workings behind current Chatbot applications.

- A clear analysis of the difference between **Traditional ML Model** and **Generative AI** helps me reshape the technology selection strategy for upcoming projects.

#### Technology Experience
- Impressed with Bedrock's **RetrieveAndGenerate API** because it significantly reduces manual programming effort for the connection between Vector Warehouse and LLM.

- See the power of **Amazon Titan Embedding** in multi-language support, very suitable for applications in the Vietnamese market.

#### Lessons learned
- RAG is the new standard: To apply AI in businesses, RAG is almost mandatory to ensure data accuracy and security.

- Comprehensive ecosystem: AWS provides everything from infrastructure (Vector Warehouse) to model layer (Bedrock) and application layer (Agents), making deployment much faster.

#### Some Photos When Attending the Event

![Image](/images/2-Proposal/genaigenai.png)
![Image](/images/2-Proposal/genai1.png)
![Image](/images/2-Proposal/genai2.png)
![Image](/images/2-Proposal/genai3.png)

> Overall, the event not only provided technical knowledge but also helped me change the way I think about application design, modernize the system and coordinate more effectively between teams.