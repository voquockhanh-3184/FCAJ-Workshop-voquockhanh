---
title : "Create Lambda Backend API for Examora"
date : 2024-01-01 
weight : 5 
chapter : false
pre : " <b> 5.5. </b> "
---

In this step, we will configure **AWS Lambda** to deploy the Express backend of **Examora**, replacing the traditional server model to optimize cost and enhance scalability.

#### 5.5.1. Objectives

Use **AWS Lambda** as the Backend API to handle the main business logic of the system, including: user profiles, classrooms, exams, questions, submissions, results, and supporting APIs for file uploads/imports.

The Lambda Backend API will:
*   Receive requests from API Gateway.
*   Process the business logic of the Examora system.
*   Retrieve the MongoDB Connection URI from AWS Secrets Manager.
*   Connect to and query the MongoDB Atlas database.
*   Write execution logs to Amazon CloudWatch.
*   Enable request tracing using AWS X-Ray.

![Lambda Backend Architecture](/images/5-Workshop/5.5-Lambda/5.5.2-create-iam-role/LambdaBE5.1.png)

#### Content

1. [Create IAM Role for Lambda Backend API](5.5.2-create-iam-role/)
2. [Create Lambda Function](5.5.3-create-lambda-function/)
3. [Configure Environment Variables for Lambda Function](5.5.4-configure-environment-variables/)
4. [Adjusting Express Backend to Run on Lambda](5.5.5-adapt-express-to-lambda/)
5. [Deploy Backend Code to Lambda](5.5.6-deploy-backend/)
6. [Test Lambda Directly Before Attaching API Gateway](5.5.7-test-lambda/)
