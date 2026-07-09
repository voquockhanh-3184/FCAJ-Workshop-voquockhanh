---
title : "Create Lambda Grading Worker"
date : 2024-01-01 
weight : 3
chapter : false
pre : " <b> 5.8.3. </b> "
---

#### Step-by-Step Instructions:

1. Create IAM Execution Role for the Grading Worker:
   * Define the Role name: `examora-grading-worker-lambda-role-dev`.
   * Add an **Inline policy** to allow consuming messages from SQS and retrieving the MongoDB connection string from Secrets Manager:

   ```json
   {
     "Version": "2012-10-17",
     "Statement": [
       {
         "Sid": "ReadGradingQueueMessages",
         "Effect": "Allow",
         "Action": [
           "sqs:ReceiveMessage",
           "sqs:DeleteMessage",
           "sqs:GetQueueAttributes",
           "sqs:ChangeMessageVisibility"
         ],
         "Resource": "arn:aws:sqs:ap-southeast-1:<ACCOUNT_ID>:examora-grading-queue-dev"
       },
       {
         "Sid": "ReadMongoDBSecret",
         "Effect": "Allow",
         "Action": [
           "secretsmanager:GetSecretValue"
         ],
         "Resource": "arn:aws:secretsmanager:ap-southeast-1:<ACCOUNT_ID>:secret:/examora/dev/mongodb-*"
       }
     ]
   }
   ```
   *(Ensure you replace `<ACCOUNT_ID>` with your AWS Account ID)*.

   ![Attach IAM Policy to Grading Worker](/images/5-Workshop/5.8-SQS-Lambda-Grading-Worker/5.8.3-create-lambda-grading-worker/LambdaGrandWork1.png)

2. Create the Lambda Grading Worker Function:
   * Function name: `examora-grading-worker-dev`.
   * **Runtime**: Select `Node.js 22.x` (matching the Lambda Backend API environment).
   * **Permissions**: Assign the execution role created in the previous step (`examora-grading-worker-lambda-role-dev`).

   ![Initialize Lambda Function](/images/5-Workshop/5.8-SQS-Lambda-Grading-Worker/5.8.3-create-lambda-grading-worker/LambdaGrandWork2.png)

3. Attach SQS Trigger to Lambda Grading Worker:
   * Open the `examora-grading-worker-dev` console page -> click **Add trigger**.
   * Select **SQS** as trigger type -> under **SQS queue**, choose `examora-grading-queue-dev`.
   * Click **Add** to save.

   ![Configure SQS Trigger](/images/5-Workshop/5.8-SQS-Lambda-Grading-Worker/5.8.3-create-lambda-grading-worker/SQSTrigger1.png)

   ![SQS Trigger Attached Successfully](/images/5-Workshop/5.8-SQS-Lambda-Grading-Worker/5.8.3-create-lambda-grading-worker/SQSTrigger2.png)

4. Update Codebase Implementation:
   * **Backend API (Publishing grading jobs):** Refactor the exam submission endpoint logic:
     * Authenticate token credentials using JWT middleware.
     * Validate that the caller is a `STUDENT`.
     * Audit exam attempt constraints.
     * Store the attempt in MongoDB with `PENDING_GRADING` status.
     * Publish the grading payload to SQS with the following structure:
       ```json
       {
         "attemptId": "<attemptId>",
         "examId": "<examId>",
         "studentId": "<studentId>",
         "submittedAt": "2026-07-06T10:00:00.000Z"
       }
       ```
     * Return an HTTP `202 Accepted` status code to the frontend to minimize response latency.

   * **Lambda Grading Worker (Processing SQS grading messages):** Implement the worker event consumer:
     * Intercept SQS trigger events.
     * Loop and parse individual SQS records inside `event.Records`.
     * Extract the `attemptId`, `examId`, and `studentId` details from the message payload.
     * Connect to MongoDB Atlas utilizing credentials retrieved from AWS Secrets Manager.
     * Query answer patterns and corresponding test keys.
     * Evaluate correct/incorrect choices and compute the score.
     * Save the result metrics into MongoDB Atlas.
     * Update the attempt status fields to `GRADED`.

   * **Code Deployment:**
     * Compress the backend code directory and upload the `.zip` packages to both Lambda functions.
     * Configure the Lambda Grading Worker's **Handler** path to: **`src/lambdas/gradingWorker/handler.handler`**.
