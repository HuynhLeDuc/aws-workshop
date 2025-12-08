---
title: "Week 11 Worklog"

weight: 2
chapter: false
pre: " <b> 1.11. </b> "
---




---

### Weekly Objectives

**Part 1 – Serverless: Using Amplify Authentication & Storage**

* Understand how Amplify Libraries, Amplify Auth, and Amplify Storage work.
* Integrate Cognito Authentication into a web application.
* Build a file upload system from the frontend and store files in S3 using Amplify Storage.
* Learn the different access levels (public / protected / private).
* Understand the overall architecture involving Cognito + S3 + Amplify.

**Part 2 – Serverless: Building a Front-end that Calls API Gateway**

* Understand the workflow of creating an API Gateway connected to Lambda.
* Build a frontend using JavaScript/React to call API Gateway → Lambda → DynamoDB.
* Test APIs using Postman and direct frontend requests.
* Understand the architecture from front-end → API Gateway → Lambda → DynamoDB.

---

### Tasks to be carried out this week:

| Day | Detailed Tasks                                                                                                                                                                                                                                                                   | Start | Finish | Source                         |
| --- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----- | ------ | ------------------------------ |
| Mon | **Introduction to Amplify & Environment Setup**<br>• Learn Amplify Libraries, CLI, and UI Components.<br>• Initialize a web project for Amplify integration.<br>• Install `@aws-amplify/ui` and `aws-amplify` packages.<br>• Configure AWS environment.                          | 17/11 | 17/11  | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| Tue | **Authentication with Amplify Auth (Cognito)**<br>• Create User Pool & Identity Pool.<br>• Configure Amplify Auth in the frontend.<br>• Build login UI via Amplify UI Components.<br>• Test signup, login, password reset.                                                       | 18/11 | 18/11  | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| Wed | **File Storage with Amplify Storage (S3)**<br>• Create S3 bucket using Amplify.<br>• Configure public/protected/private access levels.<br>• Implement file upload from frontend → S3.<br>• Verify file on S3 console.<br>• Implement list files & get URL functions.             | 19/11 | 19/11  | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| Thu | **Deploy API Gateway connected to Lambda**<br>• Create REST API.<br>• Map methods to Lambda CRUD functions.<br>• Enable CORS for frontend.<br>• Deploy updated Lambda ARN.                                                                                                       | 20/11 | 20/11  | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| Fri | **API Testing with Postman**<br>• Send GET/POST/DELETE requests.<br>• Include Cognito Authorization token.<br>• Check logs in CloudWatch.<br>• Fix CORS and IAM permission issues.                                                                                               | 21/11 | 21/11  | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| Sat | **Integrate Frontend with API Gateway**<br>• Create JavaScript service calling API Gateway.<br>• Attach Cognito token to request headers.<br>• Render data returned from Lambda/DynamoDB.<br>• End-to-end test: Frontend → API → Lambda → DynamoDB.<br>• Cleanup test resources. | 22/11 | 22/11  | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |

---

### Achievements in Week 11 :

 **1. Completed Authentication using Amplify + Cognito**

* User signup/login flows fully implemented.
* Support for verification, login, password reset flows.
* Frontend successfully retrieves JWT token for API Gateway calls.
* Strong understanding of User Pool and Identity Pool.

---

**2. File Upload & Management using Amplify Storage + S3**

* Successfully uploaded files from frontend.
* S3 bucket automatically created by Amplify.
* Verified all 3 access levels:

  * public
  * protected
  * private
* Implemented:

  * upload
  * list files
  * get URL
  * delete file

---

**3. Built a Complete API Gateway for the Document Management System (DMS)**

* Created REST API with CRUD routes.
* Integrated Lambda functions from previous week.
* Fully enabled CORS.
* Tested all endpoints using Postman with Cognito JWT tokens.

---

**4. Frontend Integration with API Gateway**

* Implemented request logic including Cognito tokens.
* Displayed documents retrieved from DynamoDB.
* Successfully executed full workflow:

**Login → Upload File → Save Metadata → Query → Display Data**

---

### Summary of Knowledge Gained

 **Amplify**

* Amplify Auth uses Cognito as backend.
* Amplify Storage simplifies S3 operations.
* Amplify UI provides quick authentication components.

 **Cognito (Authentication)**

* User Pool manages users.
* Identity Pool provides temporary credentials for S3.
* JWT tokens used for API Gateway authentication.

 **S3 (Storage)**

* Objects organized by access levels.
* Direct frontend uploads via Amplify.

 **API Gateway**

* Routes requests to Lambda.
* CORS configuration is crucial for frontend.
* Can enforce Cognito token authentication.

 **Lambda + DynamoDB**

* Lambda handles CRUD logic.
* DynamoDB stores document metadata.
* API Gateway enables frontend queries through Lambda.

---

