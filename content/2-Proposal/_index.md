---
title: "Proposal"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---


# FoodMind Recommender Platform For Prompt-IPoG
## A Unified AWS Serverless Solution for Intelligent Restaurant Recommendation Based on User Experience

### 1. Executive Summary  
**AI Food Recommender Platform** is an intelligent web platform designed to help users discover suitable restaurants based on real data from customer reviews and emotions. The platform uses an AI Sentiment Analysis model deployed on Amazon SageMaker, combined with AWS Bedrock to process raw data (user reviews, restaurant descriptions), creating a standardized database for recommendation.

The web interface is built on AWS Amplify (Next.js), allowing users to search and explore restaurants through an intelligent embedding-based search bar. Data is stored and queried via Amazon RDS, ensuring high performance and flexible scalability.  
The solution focuses on the integration of AI and real-world data to support decision-making in finding restaurants based on user emotions, experiences, and preferences.

### 2. Problem Statement  
**Current Problem**  
With the growing number of restaurants, finding a place that fits personal preferences and needs becomes difficult. Many applications like Google Maps mainly show restaurant lists based on ratings or ads, without truly personalized experiences. Users often have to read dozens of reviews to understand food quality, service, or atmosphere. Sentiment and description analysis are still manual and lack personalization capability.

**Solution**  
The AI FoodMind Recommender platform uses user reviews from Google Maps, then:  
- **Amazon S3** stores the collected raw data.  
- **AWS Bedrock** processes the raw data to generate descriptions, embeddings, and extract related aspects (food type, emotion, service quality, price level, etc.).  
- **Amazon SageMaker** deploys a Sentiment Analysis model from Hugging Face to analyze the sentiment in reviews.  
- **Amazon RDS** stores the processed data and embeddings for semantic search.  
- **AWS Amplify** deploys the web UI (Next.js) and integrates Amazon Cognito for user management.  
- **AWS Lambda** and **API Gateway** connect the frontend, backend, and AI model.

The system allows users to search in natural language such as “good pho, fast service in District 3”, and receive suitable results based on emotions, quality, and real descriptions.

**Benefits and ROI (Return on Investment)**  
- Optimize restaurant search experience through emotional factors instead of rating only.  
- Create a standardized database for AI research in the food and user behavior domain.  
- Low cost thanks to serverless architecture (using AWS free tier).  
- ROI estimate: payback within 6 months through time-saving development and reuse of existing AI models.  
- Estimated cost: about 15–20 USD/month.

### 3. Solution Architecture  
The platform applies an AI-as-a-Service architecture combined with AWS Serverless, ensuring scalability, cost optimization, and easy maintenance. Data is temporarily stored in Amazon S3, then processed by AWS Lambda and AWS Bedrock for normalization, description generation, and embedding creation. Amazon SageMaker is used to analyze sentiment in reviews, and results are stored in Amazon RDS. AWS Amplify hosts the web interface (Next.js) and Amazon Cognito ensures secure user authentication. The architecture is detailed below:

![FoodMind Recommender Platform Architecture](/images/2-Proposal/Architecture.png)

**AWS Services Used**  
- **AWS Lambda**: Handles application logic and calls AI services (3 functions).  
- **Amazon S3**: Stores raw data.  
- **Amazon SageMaker**: Deploys sentiment model from Hugging Face.  
- **Amazon API Gateway**: Communicates with the web application.  
- **AWS Bedrock**: Generates descriptions, embeddings, and normalizes data.  
- **Amazon RDS (PostgreSQL)**: Stores standardized restaurant data and embeddings.  
- **AWS Amplify**: Hosts the Next.js web interface.  
- **Amazon Cognito**: Manages users and authentication.  

**Component Design**  
- **Data Collection**: Collect raw data and store temporarily in Amazon S3.  
- **Model Deployment**: Deploy sentiment model on SageMaker Endpoint.  
- **Data Processing**: AWS Bedrock and SageMaker retrieve data from Amazon S3, process, and store results in Amazon RDS.  
- **Backend Construction**: Lambda, API Gateway, and RDS connection.  
- **Web Interface**: Hosts Next.js app with intelligent search for restaurant recommendation based on user experiences.  
- **User Management**: Amazon Cognito manages user access.  

### 4. Technical Implementation  
**Implementation Stages**  
- Research and design architecture: Build AI + Cloud pipeline, validate feasibility, and design AWS architecture diagram (first 5 weeks).  
- Cost estimation and optimization: Adjust architecture for cost efficiency (Week 6).  
- Development, Testing, and Deployment: Store raw data, process and store clean data using AWS services, then build web interface with Next.js, test performance, and deploy (Week 7–11).

**Technical Requirements**  
- *User experience data*: Includes reviews, ratings, services, atmosphere, etc. Schedule Lambda to fetch data monthly and process new data.  
- *Recommendation platform*: Requires knowledge of AWS Amplify (Next.js hosting), Lambda, S3 (2 buckets), Cognito, Bedrock, RDS, API Gateway. Use AWS CDK/SDK for programming. Next.js helps reduce Lambda load for the web app.  

### 5. Timeline & Milestones  
- *Internship (January–March)*:  
  - January: Study AWS and upgrade hardware.  
  - February: Design and adjust architecture.  
  - March: Implement, test, and deploy the platform.  
- *Post-deployment*: Monitor, improve recommendation system, and expand dataset within 1 year.

### 6. Budget Estimation  
You can view the cost estimation on [AWS Pricing Calculator](https://calculator.aws/#/estimate?id=621f38b12a1ef026842ba2ddfe46ff936ed4ab01)  
or download the [budget estimation file](../attachments/budget_estimation.pdf).  

**Infrastructure Costs**

- AWS Amplify: 0.50 USD/month (~100 MB, low traffic).  
- AWS Lambda: 0.20 USD/month (100,000 requests/month, avg runtime <1s).  
- Amazon API Gateway: 0.10 USD/month (50,000 REST API requests/month).  
- Amazon RDS (PostgreSQL): 0.00 USD/month (Free Tier 750 hours/month).  
- AWS S3 (Standard): 0.10 USD/month (2 GB data).  
- Amazon SageMaker Endpoint: 4.00 USD/month (~100 hours/month).  
- AWS Bedrock: 3.00 USD/month (a few thousand tokens/month).  
- Amazon Cognito: 0.00 USD/month (<50 active users, Free Tier).  

**Total**: ~8 USD/month, ~96 USD/year  

### 7. Risk Assessment  
*Risk Matrix*  
- Network outage: Medium impact, Medium probability.  
- API request overload: Medium impact, Medium probability.  
- Sentiment data bias: High impact, Low probability.  
- Budget overrun: Medium impact, Low probability.  

*Mitigation Strategies*  
- Network: Local storage on Raspberry Pi with Docker.  
- API overload: Limit access through API Gateway.  
- Sentiment bias: Periodically recalibrate the model.  
- Cost: AWS budget alerts and service optimization.  

*Contingency Plan*  
- Revert to manual data collection if AWS outage occurs.  
- Use CloudFormation to restore cost-related configurations.  

### 8. Expected Outcomes  
**Enhanced user experience**: Restaurant recommendations based on emotions and real descriptions.  
**Practical AI integration**: Applying Bedrock + SageMaker in a complete product system.  
**Reusable data foundation**: For research on emotional AI and customer behavior.  
**Scalability**: Expand to include factors like “location,” “culinary trends,” and “seasonal dishes.”  
