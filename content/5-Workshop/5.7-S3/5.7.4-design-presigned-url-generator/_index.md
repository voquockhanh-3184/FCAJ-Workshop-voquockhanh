---
title : "Design Lambda Presigned URL Generator"
date : 2024-01-01 
weight : 4
chapter : false
pre : " <b> 5.7.4. </b> "
---

#### Objectives:
Design a presigned URL generation mechanism to allow the Examora frontend to upload files directly to the S3 Upload Bucket, replacing the legacy local server-bound storage directory (`/public/uploads`).

#### Workflow:
`Frontend → API Gateway → Lambda Backend API → generate presigned URL → Frontend upload file directly to S3`


*Note:*
In the Examora architecture, the Lambda Presigned URL Generator represents the utility generating S3 upload signed URLs. This utility is embedded directly within the Lambda Backend API codebase to reuse existing JWT authentication middlewares, group verification logical loops, and database routes.

---

#### Step-by-Step Instructions:

1. Add S3 bucket access inline policy to the Lambda execution role:
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
         "Resource": "arn:aws:s3:::examora-s3-upload-bucket-505284748625-ap-southeast-1-an/*"
       }
     ]
   }
   ```

   ![Add S3 access policy](/images/5-Workshop/5.7-S3/5.7.4-design-presigned-url-generator/LambdaURL2.png)

   * Save the policy name as: `examora-backend-upload-bucket-policy-dev`.

   ![Policy Naming](/images/5-Workshop/5.7-S3/5.7.4-design-presigned-url-generator/LambdaURL3.png)

2. Configure S3 environment variables in the Lambda function console:

   ![Environment Variables Setup](/images/5-Workshop/5.7-S3/5.7.4-design-presigned-url-generator/LambdaURL4.png)

3. Update Lambda Backend Codebase:
   * Install the `@aws-sdk/s3-request-presigner` SDK package in the backend codebase to enable presigning commands:

   ![Install S3 Presigner SDK](/images/5-Workshop/5.7-S3/5.7.4-design-presigned-url-generator/LambdaURL5.png)

   * Add a new endpoint route: `POST /api/uploads/presigned-url`. The route implementation performs:
     * Extracting JWT credentials using the protect authorization middleware.
     * Determining user role scopes from `cognitoGroups`.
     * Selecting target path schema constraints based on `uploadType`.
     * Computing target prefix paths.
     * Generating the signed URL using `PutObjectCommand`.
     * Returning the generated `uploadUrl` to the frontend client.

4. Compress the backend source code directory and upload the updated package to `examora-backend-api-dev` on Lambda.
