---
title: "Worklog Week 9"

weight: 1
chapter: false
pre: " <b> 1.9. </b> "
---

---

### Weekly Objectives

**Part 1 – EC2 Cost Optimization with Lambda Function**

* Understand the automated Start/Stop EC2 model for cost optimization.
* Create tags to identify EC2 instances that need to be automatically started/stopped.
* Write a Lambda Function to automatically Start/Stop EC2 based on tags.
* Integrate EventBridge Scheduler to trigger Lambda on schedule.
* Validate actual behavior through CloudWatch Logs.
* Clean up resources after testing.

**Part 2 – EC2 Cost Optimization with Savings Plan**

* Understand what Savings Plans are and how they reduce costs.
* Distinguish between Compute Savings Plans and EC2 Instance Savings Plans.
* Understand USD/hour commit model and how the estimator calculates commitments.
* Learn the proper AWS process for purchasing a Savings Plan.
* Calculate cost using AWS Pricing Calculator.

---

### Tasks to be carried out this week:

| Day | Detailed Tasks                                                                                                                                                                                                                                                                              | Start Date | Completion Date | Reference       |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ | ---------- | ------------- |
| 2   | **Introduction & analysis of the EC2 cost optimization model**<br>• Understand the wastefulness when EC2 runs 24/7 but is used only for a few hours/day.<br>• Analyze the model: User → EventBridge → Lambda → EC2 API.<br>• Categorize workloads suitable for Auto Start/Stop.<br>• Explore risks and limitations of stopping/starting EC2. | 03/11  | 03/11      | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 3   | **Create tags to identify instances for automation**<br>• Create Tag Key: `Schedule`.<br>• Create Tag Values: `office-hours`, `training-only`, `weekend-shutdown`.<br>• Apply tags to the EC2 instances that need cost optimization.<br>• Validate via AWS CLI: `describe-instances --filters tag:Schedule=office-hours`. | 04/11  | 04/11      | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 4   | **Create IAM Role for Lambda Function**<br>• Create role name: `LambdaEC2ScheduleRole`.<br>• Attach policy: `AmazonEC2FullAccess` (for training).<br>• Attach logging permission: `AWSLambdaBasicExecutionRole`.<br>• Verify trust relationship: `lambda.amazonaws.com`. | 05/11  | 05/11      | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 5   | **Create Lambda Function for Start/Stop EC2**<br>• Write Python code using boto3: StartInstances & StopInstances.<br>• Logic to filter EC2 by `<Schedule>` tag.<br>• Log instance IDs that were started/stopped for verification.<br>• Manually test using “Test event”. | 06/11  | 06/11      | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 6   | **Create EventBridge Scheduler for automation**<br>• Create a rule to start EC2 at 8:00 AM.<br>• Create a rule to stop EC2 at 18:00 PM.<br>• Assign Lambda Function as the target.<br>• Check actual logs in CloudWatch Logs. | 07/11  | 07/11      | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 7   | **Validate results & clean up resources**<br>• Test if EC2 starts/stops correctly on schedule.<br>• Check CloudWatch Logs to debug permission errors.<br>• Remove EventBridge Rules, Lambda Function, IAM Role after completion.<br>• Review EC2 cost before and after optimization. | 08/11  | 08/11      | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |

---

### Achievements in Week 9 :

**1. EC2 Cost Optimization with Lambda**

* Successfully implemented automatic EC2 start/stop according to business hours.
* Understood and used Tags to group EC2 instances for cost optimization.
* Wrote Lambda Function to automatically Start/Stop EC2 using boto3.
* Automated the process using EventBridge Scheduler on a fixed schedule.
* Generated detailed logs: started/stopped instance IDs, execution time, permission errors.
* Reduced 50–70% EC2 costs for workloads operating only a few hours per day.

---

**2. Cost Optimization with Savings Plans**

* Fully understood that Savings Plans operate based on USD/hour commitment.
* Computed appropriate commitment amount using AWS Pricing Calculator.
* Differentiated between the two Savings Plan types:

  * **Compute Savings Plan** → most flexible.
  * **EC2 Instance Savings Plan** → highest discount.

* Learned the correct process for purchasing and applying Savings Plans.
* Understood benefits: up to 66% cost savings when applied correctly.

---
### Summary of Knowledge Gained

**AWS Lambda + EC2 Automation**

* Automated EC2 start/stop using Lambda.
* Used Boto3 to call EC2 control APIs.
* EventBridge Scheduler used for periodic triggers.
* CloudWatch Logs used for analysis and debugging.

**AWS Savings Plans**

* Method of committing costs to reduce AWS infrastructure expenses.
* Best suited for workloads that run 24/7.
* Differences between Compute vs. EC2 Instance Savings Plans.
* Combining Auto Scheduling + Savings Plans for maximum optimization.
