---
title : "Clean up resources"
date : 2024-01-01 
weight : 10 
chapter : false
pre : " <b> 5.10. </b> "
---

After successfully completing the workshop and verifying the Examora system integration, we must delete all provisioned AWS resources to optimize costs and prevent unintended billing cycles.

---

#### 1. Delete AWS Amplify Hosting
*   **Remove Custom Domain:**
    *   Navigate to **AWS Amplify** -> open your Frontend app.
    *   From the left-hand menu, choose **Custom domains** -> select your custom domain -> click **Actions** -> click **Delete**.

    ![Remove Custom Domain from Amplify](/images/5-Workshop/5.10-Don-dep-tai-nguyen/GoDomain1.png)

*   **Delete Amplify App:**
    *   Navigate back to the app details page -> select **App settings** in the left menu -> click **Delete app** on the right side -> enter the confirmation text and click **Delete**.

    ![Delete Amplify App](/images/5-Workshop/5.10-Don-dep-tai-nguyen/XoaAmplify.png)

---

#### 2. Delete Amazon Route 53 Configurations
*   **Delete Records:**
    *   Navigate to **Route 53** -> choose **Hosted zones** -> click your domain.
    *   Select all user-created DNS records (e.g., A, CNAME records), **ensuring you preserve the default NS and SOA records** -> click **Delete record**.

    ![Delete DNS Records](/images/5-Workshop/5.10-Don-dep-tai-nguyen/XoaRecord.png)

*   **Delete Hosted Zone:**
    *   Once only the default NS and SOA records remain -> navigate back to the Hosted zones index -> select your domain -> click **Delete hosted zone** -> enter confirmation and delete.

    ![Delete Hosted Zone](/images/5-Workshop/5.10-Don-dep-tai-nguyen/XoaHostedzones.png)

---

#### 3. Delete Amazon API Gateway
*   Navigate to **API Gateway** -> select **APIs** -> click your API instance (e.g., `examora-api`).
*   Click **Delete** on the right side -> enter the API name for confirmation and delete the API.

    ![Delete API Gateway](/images/5-Workshop/5.10-Don-dep-tai-nguyen/XoaAPIGateway.png)

---

#### 4. Remove Triggers Before Deleting Lambdas
*   **Remove S3 Trigger from Lambda Import Word Processor:**
    *   Open `examora-import-word-processor-dev` -> in the Function overview section, select the **S3** trigger -> click **Remove** (or **Delete**).

    ![Delete S3 Trigger](/images/5-Workshop/5.10-Don-dep-tai-nguyen/XoaS3Trigger.png)

*   **Remove SQS Trigger from Lambda Grading Worker:**
    *   Similarly, open `examora-grading-worker-dev` -> select the **SQS** trigger -> click **Remove** to delete the queue integration.

    ![Delete SQS Trigger](/images/5-Workshop/5.10-Don-dep-tai-nguyen/XoaS3SQS.png)

---

#### 5. Delete Lambda Functions
*   Go to **Lambda** -> **Functions** -> select the project Lambda functions:
    *   `examora-backend-api-dev`
    *   `examora-import-word-processor-dev`
    *   `examora-grading-worker-dev`
*   Select **Actions** -> click **Delete** -> confirm the operation.

    ![Delete Lambda Functions](/images/5-Workshop/5.10-Don-dep-tai-nguyen/XoaLambda.png)

---

#### 6. Delete Amazon SQS Queues and Dead-letter Queues (DLQ)
*   Navigate to **Amazon SQS** -> select **Queues**.
*   Select all queues deployed for the project:
    *   `examora-grading-queue-dev`
    *   `examora-grading-dlq-dev`
*   Click **Delete** -> enter the confirmation phrase -> click **Delete**.

    ![Delete SQS Queues](/images/5-Workshop/5.10-Don-dep-tai-nguyen/XoaSQS.png)

---

#### 7. Delete Amazon S3 Buckets
*   Go to **Amazon S3** -> select **Buckets**.
*   Because S3 prevents deletion of non-empty buckets, clear the contents first:
    *   Select your bucket -> click **Empty** -> enter confirmation to clear all uploaded static objects.
    *   Return to the Buckets directory -> select the bucket -> click **Delete** -> enter confirmation.
    *   Repeat this process for all project S3 buckets.

    ![Delete S3 Buckets](/images/5-Workshop/5.10-Don-dep-tai-nguyen/XoaBuckets.png)

---

#### 8. Delete Amazon Cognito User Pools
*   Navigate to **Amazon Cognito** -> select **User pools**.
*   Select your user pool -> click **Delete** -> enter the confirmation string to purge all users and groups database schemas.

    ![Delete Cognito User Pool](/images/5-Workshop/5.10-Don-dep-tai-nguyen/XoaCognito.png)

---

#### 9. Delete Amazon SES Email Identity
*   Open the **Amazon SES** console -> select **Configuration** -> **Identities**.
*   Select the validated email identity used for the project -> click **Delete** -> confirm.

    ![Delete SES Identity](/images/5-Workshop/5.10-Don-dep-tai-nguyen/XoaSES.png)

---

#### 10. Delete AWS Secrets Manager Secret
*   Navigate to **Secrets Manager** -> **Secrets** -> select the MongoDB connection secret.
*   Click **Actions** -> click **Delete secret**.
*   Configure the minimum recovery duration window (e.g., `7 days`) -> click **Schedule deletion**.

    ![Delete Secrets Manager Secrets](/images/5-Workshop/5.10-Don-dep-tai-nguyen/XoaSecret.png)

---

#### 11. Delete Amazon CloudWatch Log Groups
*   Open the **CloudWatch** console -> choose **Log groups** under the **Logs** tab.
*   Select all log groups allocated to the Lambda functions of this project -> click **Actions** -> select **Delete log group(s)** -> confirm the deletion.

    ![Delete CloudWatch Log Groups](/images/5-Workshop/5.10-Don-dep-tai-nguyen/XoaCloudWatch.png)

---

#### 12. Delete IAM Roles and Inline Policies
*   **Note:** Only remove roles created specifically for the Examora deployment.
*   Navigate to **IAM** -> select **Roles**.
*   Search and check the execution roles allocated to the Lambda functions (Backend, Word Processor, and Grading Worker).
*   Click **Delete** -> enter confirmation and delete.

    ![Delete IAM Roles](/images/5-Workshop/5.10-Don-dep-tai-nguyen/XoaIAMRole.png)
