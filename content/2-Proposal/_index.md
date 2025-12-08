---
title: "Proposal"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# FoodMind Recommender Platform For Prompt-IPoG
## An integrated AWS Serverless solution for personalized meal tracking and recommendations. 

### 1. Executive Summary  
**FoodMind Recommender Platform** is an intelligent web platform designed to serve as a personalized eating assistant. It automatically calculates the user's Total Daily Energy Expenditure (TDEE) based on their profile and leverages **AWS Bedrock (Generative AI)** to allow users to log meals in natural language (e.g., “I just ate a bowl of beef pho”).  
The system also provides intelligent meal recommendations (Breakfast/Lunch/Dinner) by automatically **filtering** dishes according to calorie goals and health constraints (e.g., “allergies”, “gout”).  

The entire solution is built on a **serverless architecture** with AWS Amplify (Frontend), API Gateway, AWS Lambda, and Amazon DynamoDB (Backend). It enables users to receive meal recommendations based on their calculated calorie intake for the day. Data is stored and queried through Amazon DynamoDB, ensuring high performance and flexible scalability.  

The solution emphasizes the combination of AI and real-world data to support smart meal decision-making and offers a **dashboard** for users to track their eating habits effectively.  

### 2. Problem Statement  
**Current Problem**  
Many users struggle to manage their daily diet — they don’t know how many calories to consume or which foods suit their daily health goals. Manual logging and nutritional lookup are time-consuming, inaccurate, and not personalized.  

**Solution**  
FoodMind Recommender Platform applies **AI and AWS Cloud** to automate the entire meal tracking and recommendation process:  

**Goal Automation:** Automatically calculates calorie targets (using the Mifflin-St Jeor formula) when users update their profiles.  

**Recommendation Automation:** Provides a `GET /recommendations` API using **Lambda business logic** to filter dishes from the database based on calorie targets (e.g., lunch < 700 calories) and health restrictions (e.g., avoid “red meat” for gout).  

**AI Logging Automation:** Provides a `POST /log-food` API using **AWS Bedrock** to parse natural language input, extract calories, and store logs.  

**Self-learning Automation:** When users log a new dish (e.g., “bun dau mam tom”) unknown to the system, **AWS Bedrock** estimates its calories and automatically adds it to the knowledge base.  

**Visual Tracking:** The **dashboard (Amplify)** displays a 7-day meal history, helping users monitor and manage their dietary habits.  

Users simply input data — the system understands, analyzes, and recommends suitable meals tailored to personal health goals.  

**Benefits and ROI**  
- Saves time on nutrition tracking, eliminates manual work.  
- Offers highly personalized AI experience.  
- Creates a structured dataset for AI research in food and nutrition.  
- Low cost thanks to serverless architecture.  
- Scalable and reusable for other health-related applications.  
- ROI estimate: payback within 6 months through reduced development time and model reuse.  
- Estimated cost: around **10–15 USD/month**.  

### 3. Solution Architecture  
The platform is fully built on **AI-as-a-Service** combined with **AWS Serverless**, ensuring high performance, security, and scalability. Nutritional data on dishes is stored in **Amazon DynamoDB**, which supports generating meal recommendations based on calculated calorie targets. **Amazon Bedrock** processes user natural language to extract calorie information and log meals in DynamoDB. **AWS Amplify** hosts the Next.js web interface, and **Amazon Cognito** ensures secure user authentication. The architecture is detailed below:

![alt text](/images/2-Proposal/Architecture.jpg)

**AWS Services Used**

- **AWS Amplify:** Deploys and hosts the web interface (Next.js), integrates with GitLab CI/CD for auto build and deploy.  
- **Amazon Route 53 + AWS WAF + Amazon CloudFront:** Edge layer for secure and fast content delivery worldwide.  
- **Amazon Cognito:** Manages user authentication, login, and access control.  
- **Amazon API Gateway:** Provides endpoints for `GET /Recommendation`, `POST /Log`, `GET /Dashboard`, connected to Lambda.  
- **AWS Lambda (Private Subnet):** Handles business logic, calls Bedrock and DynamoDB via VPC Endpoints for security.  
- **AWS Bedrock:** Generates dish descriptions, normalizes meal logs, and stores them in DynamoDB for personalized recommendations.  
- **Amazon DynamoDB:** Stores user data, meal logs, calorie goals, and recommendation data with scalable performance.  
- **AWS Secrets Manager:** Secures credentials (API Keys, Bedrock access) for Lambda and backend.  
- **Amazon CloudWatch & AWS CloudTrail:** Monitors logs, access, and performance; supports incident recovery.  
- **Amazon S3:** Stores system logs and backups.  
- **AWS IAM:** Manages detailed access permissions between services and users.  
- **Amazon VPC:** Isolates Lambda in a private subnet to ensure secure internal communication between Lambda, DynamoDB, and Bedrock.  

**Component Design**  

- **User Management:** Amazon Cognito controls user access.  
- **Content Delivery & Security:** Route 53 routes domain, WAF prevents web attacks (SQL Injection, DDoS), CloudFront speeds up global delivery.  
- **Web Interface:** Amplify hosts the Next.js app.  
- **Meal Logging & Recommendation:** User input (text) stored in DynamoDB; Lambda recommends dishes based on calorie calculations.  
- **Meal Analysis:** Lambda calls Bedrock to process user input, extract calorie data, and log new dishes in DynamoDB if missing.  
- **Dashboard Display:** Amplify shows calorie charts by day/week/month.  
- **Authentication & Security:** Cognito ensures secure login and user management.  
- **Monitoring & Tracking:** CloudWatch monitors logs and Lambda performance; CloudTrail records API and user activity history.  

### 4. Technical Implementation  
**Implementation Phases**  
- **Research & Design:** Build AI + Cloud pipeline, check feasibility, and design AWS architecture (Weeks 1–5).  
- **Cost Optimization:** Validate AWS service pricing to optimize budget (Week 6).  
- **Development & Deployment:** Load initial data, build Next.js frontend, test APIs, and deploy final product (Weeks 7–11).  

**Technical Requirements**  
- *Calorie Dataset:* Collect initial data and load into DynamoDB using AWS SDK (Boto3).  
- *Recommendation Platform:* Requires knowledge of AWS Amplify (Next.js hosting), S3, Cognito, and Serverless stack (Lambda, DynamoDB, API Gateway), DynamoDB schema (PK, SK), and Bedrock API integration.  

### 5. Roadmap & Milestones  
- **Internship (Jan–Mar):**  
  - **January:** Learn and master AWS services.  
  - **February:** Design and refine architecture.  
  - **March:** Deploy, test, and launch the system.  
- **Post-deployment:** Maintain, enhance recommendations, and expand data within one year.  

### 6. Budget Estimation  
Cost reference: [AWS Pricing Calculator](https://calculator.aws/#/estimate?id=621f38b12a1ef026842ba2ddfe46ff936ed4ab01)  
Or download [budget estimation file](../attachments/budget_estimation.pdf).  

**Infrastructure Cost**

- **AWS Amplify:** 0.50 USD/month (~100 MB, low traffic).  
- **AWS Lambda:** 0.20–0.30 USD/month (100,000 requests/month, avg runtime <1s).  
- **Amazon API Gateway:** 0.10–0.20 USD/month (50,000 REST API requests/month).  
- **Amazon DynamoDB (Paid Plan):** ~0.30 USD/month (50 MB data, ~20,000 requests/month, On-Demand).  
- **Amazon S3 (log/backup):** 0.10 USD/month (<2GB).  
- **AWS Bedrock:** 3.00–5.00 USD/month (a few thousand tokens/month).  
- **CloudWatch + CloudTrail + IAM:** ~0.10 USD/month.  
- **Amazon Cognito:** 0.00 USD/month (<50 active users, Free Tier).  

**Total:** ~4–6 USD/month (~50–75 USD/year).  

### 7. Risk Assessment  
**Risk Matrix**  
- AI misinterpretation — High impact, Low probability.  
- API overload — Medium impact, Low probability.  
- Budget overrun — Medium impact, Low probability.  
- Logic error — Medium impact, Low probability.  

**Mitigation Strategies**  
- AI deviation: Careful prompt engineering.  
- API overload: Request throttling via API Gateway.  
- Budget: AWS budget alerts and service optimization.  
- Logic: Rigorous Lambda testing and validation.  

**Contingency Plan**  
- Manual data collection fallback if AWS outage occurs.  
- Use CloudFormation to restore infrastructure configurations.  

### 8. Expected Outcomes  
**Enhanced User Experience:** Provides a smart meal assistant, removing manual effort in tracking and choosing meals.  

**Practical AI Integration:** Demonstrates real-world AWS Bedrock integration in production-level systems.  

**Nutrition Data Foundation:** Expandable dataset for AI and healthcare research.  

**Scalability:** Extendable to image-based food analysis, AI chat coaching, and mobile applications.  