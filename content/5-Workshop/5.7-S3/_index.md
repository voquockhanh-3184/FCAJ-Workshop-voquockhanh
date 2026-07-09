---
title : "Configure S3 Upload Bucket and Presigned URL"
date : 2024-01-01 
weight : 7 
chapter : false
pre : " <b> 5.7. </b> "
---

#### Objectives:
*   Create an **S3 Upload Bucket** to store user avatars, class covers, exam images, and raw Word documents directly from the client without routing static binary assets through the Lambda Backend API, reducing compute overhead on the serverless backend.
*   Implement secure direct uploads from the Frontend to Amazon S3 using **Presigned URLs**.


#### Sections:
1. [Create S3 Upload Bucket and Configure CORS](5.7.1-create-s3-bucket/)
2. [S3 Prefix Naming Conventions for File Organization](5.7.2-prefix-convention/)
3. [Grant S3 Access to Lambda Backend API](5.7.3-grant-s3-permission-lambda/)
4. [Design Lambda Presigned URL Generator](5.7.4-design-presigned-url-generator/)
5. [Verify Presigned URL Endpoint and S3 Upload](5.7.5-test-presigned-url-upload/)
6. [Create Lambda Import Word Processor](5.7.6-create-import-word-processor/)
