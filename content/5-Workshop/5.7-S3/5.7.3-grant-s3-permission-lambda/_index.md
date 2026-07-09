---
title : "Grant S3 Access to Lambda Backend API"
date : 2024-01-01 
weight : 3
chapter : false
pre : " <b> 5.7.3. </b> "
---

To enable the Lambda Backend API to sign and generate S3 Presigned URLs, we must append the required S3 permissions to the Lambda function's IAM execution role and configure the S3 bucket details in the function's environment variables.

#### Step-by-Step Instructions:

1. Create S3 Inline Policy:
   * Navigate to the **IAM** console -> select **Roles** -> search for and open the Lambda execution role (e.g., `examora-lambda-backend-role`).
   * In the **Permissions** tab -> click **Add permissions** -> choose **Create inline policy**.

   ![Add Permissions Inline Policy](/images/5-Workshop/5.7-S3/5.7.3-grant-s3-permission-lambda/IAMpermissions1.png)

   * Choose the **JSON** editor option and paste the following policy:

   ```json
   {
     "Version": "2012-10-17",
     "Statement": [
       {
         "Sid": "ExamoraUploadBucketObjectAccess",
         "Effect": "Allow",
         "Action": [
           "s3:PutObject",
           "s3:GetObject"
         ],
         "Resource": "arn:aws:s3:::<UPLOAD_BUCKET_NAME>/*"
       }
     ]
   }
   ```
   *(Ensure you replace `<UPLOAD_BUCKET_NAME>` with the S3 bucket name created in section 5.7.1)*.

   ![JSON Policy Editor](/images/5-Workshop/5.7-S3/5.7.3-grant-s3-permission-lambda/IAMpermissions2.png)

   * Click **Next**.
   * Set the policy name to: `examora-backend-upload-bucket-policy-dev`.
   * Click **Create policy** to finalize.

   ![Policy Name Definition](/images/5-Workshop/5.7-S3/5.7.3-grant-s3-permission-lambda/IAMpermissions3.png)

   ![Policy Attached Successfully](/images/5-Workshop/5.7-S3/5.7.3-grant-s3-permission-lambda/IAMpermissions4.png)

2. Register S3 Configurations as Lambda Environment Variables:
   * Navigate to the **Lambda** dashboard -> open the `examora-backend-api` function -> click the **Configuration** tab -> choose **Environment variables** in the left menu -> click **Edit**.
   * Add the following environment variables:
     * `UPLOAD_BUCKET_NAME` = `<Your S3 Bucket Name>`
     * `UPLOAD_BUCKET_REGION` = `ap-southeast-1`
   * Click **Save** to apply the configuration.

   ![Register S3 Environment Variables](/images/5-Workshop/5.7-S3/5.7.3-grant-s3-permission-lambda/EnvBucket1.png)
