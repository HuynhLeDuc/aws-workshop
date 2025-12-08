---
title: "Week 10 Worklog"
weight: 2
chapter: false
pre: " <b> 1.10. </b> "
---

---

### Weekly Objectives

**Part 1 – Build the backend for the Document Management System (DMS) using Lambda + DynamoDB**

* Understand the overall architecture of the Document Management System.
* Design the DynamoDB table according to real-world access patterns.
* Build Lambda functions for document CRUD operations (Create, Read, Query, Delete).
* Configure IAM Roles for Lambda following the principle of least privilege.
* Test APIs using test events and CloudWatch Logs.
* Prepare the foundation for integrating API Gateway and Amplify in the next week.

**Part 2 – Understand how the DMS will scale in upcoming weeks**

* Understand how Cognito Authentication and Amplify Storage will be integrated.
* Identify the role of DynamoDB Streams for the search engine using OpenSearch.
* Understand the process of deploying the entire backend using AWS SAM.
* Understand the expected CI/CD pipeline using AWS CodePipeline.

---

### Tasks to be carried out this week:

| Day | Detailed Tasks                                                                                                                                                                                                                                                                                                                                                       | Start | End | Source |
| --- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ | ------ | ------ |
| 2   | **Analyze the overall DMS architecture**<br>• Understand the application goals: upload, view, download, delete, and search documents.<br>• Identify main components: Lambda, DynamoDB, S3, Cognito, API Gateway.<br>• Analyze workflow: Upload → Save metadata → Search processing.<br>• List all required backend API endpoints.                                            | 11/10 | 11/10 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 3   | **Design DynamoDB Table for Document Metadata**<br>• Create table `Documents` with PK = `userId`, SK = `documentId`.<br>• Design attributes: filename, fileType, size, tags, createdAt, updatedAt.<br>• Analyze access patterns: Query by user, Get by documentId, filter by tag.<br>• Prepare sample data and test via AWS Console + CLI.                                   | 11/11 | 11/11 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 4   | **Create IAM Role for Lambda Functions**<br>• Create role `DMSLambdaRole`.<br>• Grant DynamoDB CRUD permissions: GetItem, Query, PutItem, DeleteItem.<br>• Grant CloudWatch Logs permissions.<br>• Validate Trust Policy: `lambda.amazonaws.com`.<br>• Test assume role using Lambda test environment.                                                                     | 11/12 | 11/12 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 5   | **Develop CreateDocument Lambda Function**<br>• Validate user input.<br>• Auto-generate `documentId` using UUID.<br>• Save metadata into DynamoDB using `put_item`.<br>• Add input/output logging for monitoring.<br>• Test using Lambda test events + CloudWatch Logs.<br>• Improve exception handling: missing fields, DynamoDB errors.                                       | 11/13 | 11/13 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 6   | **Develop GetDocuments & GetDocumentById Lambda Functions**<br>• Implement query to fetch all documents by userId.<br>• Support pagination using LastEvaluatedKey.<br>• Implement GetDocumentById to fetch single document details.<br>• Return structured JSON for frontend use.<br>• Test using sample DynamoDB data.                                                | 11/14 | 11/14 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 7   | **Develop DeleteDocument Lambda Function & Cleanup**<br>• Verify document existence before deletion.<br>• Delete metadata using `delete_item`.<br>• Prepare logic for deleting real files from S3 (scheduled for next week).<br>• Log the delete process for observability.<br>• Clean up test resources and remove unnecessary records.                                | 11/15 | 11/15 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |

---

### Achievements in Week 10 :

**1. Completed DynamoDB table with optimal design**

* Fully built the `Documents` table meeting the needs of a Document Management System.
* Designed PK/SK optimized for querying by user and retrieving detailed items.
* Prepared a scalable data model for future integration with OpenSearch or DynamoDB Streams.

---

**2. Successfully developed all Lambda CRUD functions**

* CreateDocument – create new documents.
* GetDocuments – query documents by userId.
* GetDocumentById – retrieve a document by documentId.
* DeleteDocument – delete documents safely.
* All functions follow Serverless best practices with full logging and safe retries.

---

**3. Applied best practices for security and logging**

* IAM Roles strictly follow the least privilege principle.
* CloudWatch Logs used to trace all execution flows.
* Clear error handling: input validation, DynamoDB errors, missing items.

---

**4. Fully understood the DMS architecture and prepared for next week**

* Mastered the workflow: Authentication → API → Storage → Metadata.
* Understood how Lambda will integrate with API Gateway in Week 11.
* Built a solid technical foundation for next week’s Amplify Storage + Authentication implementation.

---

### Summary of Knowledge Gained

**AWS DynamoDB**
* Designing tables based on access patterns.
* Proper use of Partition/Sort keys.
* Query, PutItem, GetItem, DeleteItem with Boto3.

**AWS Lambda**
* Writing serverless CRUD functions.
* Creating optimized IAM Roles + policies.
* Logging using CloudWatch Logs.
* Production-grade error handling.

**DMS Architecture**
* Metadata stored in DynamoDB.
* Actual files stored in S3.
* Authentication handled by Cognito.
* APIs orchestrated through Lambda + API Gateway.

---
