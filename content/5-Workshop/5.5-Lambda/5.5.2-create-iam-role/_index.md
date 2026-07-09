---
title : "Create IAM Role for Lambda Backend API"
date : 2024-01-01 
weight : 2
chapter : false
pre : " <b> 5.5.2. </b> "
---

An AWS Lambda function requires an **execution role** to access other AWS services. We will create a dedicated execution role for the Lambda Backend API following the principle of least privilege.

#### Step-by-Step Instructions:

1. Navigate to the [Roles](https://us-east-1.console.aws.amazon.com/iam/home?region=ap-southeast-1#/roles) dashboard in the IAM console, then click **Create role**.

2. Configure the Trusted Entity properties:
   * **Trusted entity type**: Select **AWS service**.
   * **Service or use case**: Select **Lambda**.
   * Click **Next**.

   ![Select Trusted Entity](/images/5-Workshop/5.5-Lambda/5.5.2-create-iam-role/LambdaBE5.2.png)

3. Attach the baseline policies for logging and tracing: in the **Permissions policies** section, search for and select:
   * **AWSLambdaBasicExecutionRole**: Grants permission to upload logs to Amazon CloudWatch Logs.
   * **AWSXRayDaemonWriteAccess**: Grants permission to upload trace segments to AWS X-Ray.

   ![Select Permission Policies](/images/5-Workshop/5.5-Lambda/5.5.2-create-iam-role/LambdaBE5.3.png)

4. Name and create the Role:
   * **Role name**: Enter a descriptive name (e.g., `examora-lambda-backend-role`).
   * Review the configuration and click **Create role**.

   ![Name Role](/images/5-Workshop/5.5-Lambda/5.5.2-create-iam-role/LambdaBE5.4.png)

5. Attach Secrets Manager read permissions (to allow connection to MongoDB Atlas):
   * Select the newly created role -> under the **Permissions** tab -> click **Add permissions** -> select **Create inline policy**.
   * Switch to the **JSON** tab and enter the following policy document (replace `<ACCOUNT_ID>` with your AWS Account ID):

   ```json
   {
     "Version": "2012-10-17",
     "Statement": [
       {
         "Sid": "ReadExamoraMongoDBSecret",
         "Effect": "Allow",
         "Action": [
           "secretsmanager:GetSecretValue"
         ],
         "Resource": "arn:aws:secretsmanager:ap-southeast-1:<ACCOUNT_ID>:secret:/examora/dev/mongodb-*"
       }
     ]
   }
   ```
   * *Note*: `/examora/dev/mongodb` corresponds to the secret created earlier in AWS Secrets Manager containing `MONGO_URI` and `MONGO_DB_NAME`.
   * Name the policy (e.g., `examora-lambda-secrets-policy`) -> click **Create policy**.

   ![Attach Inline Policy](/images/5-Workshop/5.5-Lambda/5.5.2-create-iam-role/LambdaBE5.5.png)

The IAM execution role for the Lambda Backend API has been successfully created.
