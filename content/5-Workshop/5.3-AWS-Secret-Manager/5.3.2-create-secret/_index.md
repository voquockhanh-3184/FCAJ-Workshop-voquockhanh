---
title : "Create Secret in AWS Secrets Manager"
date : 2024-01-01 
weight : 1
chapter : false
pre : " <b> 5.3.2. </b> "
---

#### Summary:
*   We use AWS Secrets Manager to store the MongoDB Atlas connection details for the Examora project.
*   Instead of hardcoding `MONGO_URI` in the source code or configuration files, the backend Lambda functions dynamically retrieve the `/examora/dev/mongodb` secret at initialization.
*   The secret contains two key-value pairs: `MONGO_URI` and `MONGO_DB_NAME`.
*   In the workshop/dev environment, automatic rotation is disabled to simplify deployment. In a production environment, secrets should be rotated periodically and access restricted strictly using IAM least privilege.

#### Step-by-Step Guide:

1. In the AWS Console search bar, type **Secrets Manager** -> Select **Secrets Manager** -> Click **Store a new secret**.

![Secrets Manager Console](/images/5-Workshop/5.3-AWS-Secret-Manager/5.3.2-create-secret/SecretManage5.1.png)

2. Create a new secret:
- In **Choose secret type** -> Select **Other type of secret**.
- Enter **Key/value** inputs for the secret (add 2 key/value pairs):
  - Key: `MONGO_URI` | Value: `<your MongoDB Atlas connection string>`
  - Key: `MONGO_DB_NAME` | Value: `WebsiteTest2026`
- Under **Encryption key**, keep the default encryption key (`aws/secretsmanager`).
- Click **Next**.

![Choose Secret Type](/images/5-Workshop/5.3-AWS-Secret-Manager/5.3.2-create-secret/SecretManage5.2.png)

3. Set the name for the secret (e.g., `/examora/dev/mongodb`) -> Click **Next**.

![Secret Name](/images/5-Workshop/5.3-AWS-Secret-Manager/5.3.2-create-secret/SecretManage5.3.png)

4. In the **Configure rotation** section -> Disable **Automatic rotation**.
- Review all configuration details -> Click **Store** at the bottom to create the secret.

![Configure Rotation](/images/5-Workshop/5.3-AWS-Secret-Manager/5.3.2-create-secret/SecretManage5.4.png)

5. Secret created successfully:

![Secret Created Successfully](/images/5-Workshop/5.3-AWS-Secret-Manager/5.3.2-create-secret/SecretManage5.5.png)

*   After creating the `/examora/dev/mongodb` secret, note down the **Secret ARN** for use in the subsequent Lambda execution role creation step.
*   Lambda functions that need database access will be granted `secretsmanager:GetSecretValue` permissions on this secret.
*   The specific IAM policy assignment for Lambda to read the secret will be configured during the Lambda Backend API creation step.
