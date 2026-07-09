---
title : "Configure SQS and Lambda Grading Worker"
date : 2024-01-01 
weight : 8 
chapter : false
pre : " <b> 5.8. </b> "
---

#### 5.8.1. Overview:
In the *Exam Submission & Grading Pipeline*, Examora incorporates **Amazon SQS Grading Queue** and **Lambda Grading Worker** to decouple the grading computation from the student's submit-exam HTTP request/response loop (asynchronous grading).

When a student submits their exam answers, the Lambda Backend API does not grade the attempt synchronously. Instead, it validates the request structure, saves the attempt in a `PENDING_GRADING` status, and dispatches a grading job message to the SQS queue. Subsequently, the Lambda Grading Worker is triggered to consume the job from SQS, fetch exam structures from MongoDB Atlas, calculate scores, and update the attempt records.

![Asynchronous Grading Pipeline](/images/5-Workshop/5.8-SQS-Lambda-Grading-Worker/5.8.1-overview/SQS1.png)

#### Sections:
1. [Create SQS Grading Queue](5.8.2-create-sqs-queue/)
2. [Create Lambda Grading Worker](5.8.3-create-lambda-grading-worker/)
3. [Verify SQS and Lambda Grading Worker Pipeline](5.8.4-test-grading-pipeline/)
