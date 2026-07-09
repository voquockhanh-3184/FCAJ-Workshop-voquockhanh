---
title : "Create SQS Grading Queue"
date : 2024-01-01 
weight : 2
chapter : false
pre : " <b> 5.8.2. </b> "
---

To implement the message queuing pipeline, we need to create two SQS queues: the primary processing queue (`examora-grading-queue-dev`) and a **Dead-letter Queue (DLQ)** to store messages that repeatedly fail processing to facilitate troubleshooting.

#### Step-by-Step Instructions:

1. Create Dead-letter Queue (DLQ):
   * Navigate to the **Amazon SQS** dashboard -> select **Queues** -> click **Create queue**.
   * Configure the DLQ settings:
     * **Type**: Select `Standard`.
     * **Name**: Enter `examora-grading-dlq-dev`.
     * Keep all other default settings -> click **Create queue**.

   ![Configure SQS DLQ](/images/5-Workshop/5.8-SQS-Lambda-Grading-Worker/5.8.2-create-sqs-queue/SQS2.png)

   ![DLQ Created](/images/5-Workshop/5.8-SQS-Lambda-Grading-Worker/5.8.2-create-sqs-queue/SQS3.png)

2. Create SQS Grading Queue (Primary Queue):
   * Click **Create queue** again to set up the primary queue.
   * Configure the primary queue settings:
     * **Type**: Select `Standard`.
     * **Name**: Enter `examora-grading-queue-dev`.
     * Scroll down to the **Dead-letter queue** panel -> select **Enabled**.
     * **Choose queue**: Select the DLQ created in the previous step (`examora-grading-dlq-dev`).
     * **Maximum receives**: Enter `3` (messages failing more than 3 processing attempts will be redirected to the DLQ).
   * Click **Create queue** to finish.

   ![Create SQS Grading Queue with DLQ](/images/5-Workshop/5.8-SQS-Lambda-Grading-Worker/5.8.2-create-sqs-queue/SQS4.png)

3. Record Queue URL and ARN Values:
   * Select your primary queue from the list and record the following attributes:
     * **Queue URL** (e.g., `https://sqs.ap-southeast-1.amazonaws.com/<ACCOUNT_ID>/examora-grading-queue-dev`)
     * **Queue ARN** (e.g., `arn:aws:sqs:ap-southeast-1:<ACCOUNT_ID>:examora-grading-queue-dev`)

4. Grant SQS Send Permissions to Lambda Backend API:
   * Since the Lambda Backend API needs to publish grading events to SQS, we must add `sqs:SendMessage` permissions to its execution role.
   * Go to the Lambda Backend's IAM execution role -> select **Permissions** -> click **Add permissions** -> select **Create inline policy** and write the JSON schema:

   ```json
   {
     "Version": "2012-10-17",
     "Statement": [
       {
         "Sid": "SendGradingJobToSQS",
         "Effect": "Allow",
         "Action": [
           "sqs:SendMessage"
         ],
         "Resource": "arn:aws:sqs:ap-southeast-1:<ACCOUNT_ID>:examora-grading-queue-dev"
       }
     ]
   }
   ```
   *(Ensure you replace `<ACCOUNT_ID>` with your AWS Account ID)*.
   * Name the policy: `examora-backend-send-grading-policy-dev`.

   ![Add SQS Send Message Permission Policy](/images/5-Workshop/5.8-SQS-Lambda-Grading-Worker/5.8.2-create-sqs-queue/SQS5.png)

5. Configure SQS URL Environment Variable in Lambda:
   * Access the Lambda Backend API dashboard -> navigate to the **Configuration** tab -> select **Environment variables** -> click **Edit**.
   * Add the following environment variable:
     * `GRADING_QUEUE_URL` = `<Your SQS Queue URL>`
   * Click **Save** to persist.

   ![Register SQS URL Environment Variable](/images/5-Workshop/5.8-SQS-Lambda-Grading-Worker/5.8.2-create-sqs-queue/SQS6.png)
