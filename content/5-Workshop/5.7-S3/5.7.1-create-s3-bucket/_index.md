---
title : "Create S3 Upload Bucket and Configure CORS"
date : 2024-01-01 
weight : 1
chapter : false
pre : " <b> 5.7.1. </b> "
---

#### Step-by-Step Instructions:

1. Create S3 Bucket:
   * Navigate to the **Amazon S3** management console -> choose **Buckets** in the left navigation pane -> click **Create bucket**.
   * Configure the primary parameters:
     * **Bucket name**: Enter a globally unique name (e.g., `examora-s3-upload-bucket`).
     * **AWS Region**: Choose `ap-southeast-1` (Singapore).
     * Keep all other parameters at their default values -> scroll to the bottom and click **Create bucket**.

   ![Create S3 Bucket](/images/5-Workshop/5.7-S3/5.7.1-create-s3-bucket/S3UpLoad6.2.png)

2. Configure S3 CORS Policy:
   * Once the bucket is provisioned, click on the bucket name -> navigate to the **Permissions** tab.
   * Scroll down to the **Cross-origin resource sharing (CORS)** configuration panel -> click **Edit**.

   ![Configure CORS S3](/images/5-Workshop/5.7-S3/5.7.1-create-s3-bucket/S3UpLoad6.3.png)

   * Paste the following JSON schema:

   ```json
   [
     {
       "AllowedHeaders": ["*"],
       "AllowedMethods": ["PUT", "GET", "HEAD"],
       "AllowedOrigins": ["http://localhost:5173"],
       "ExposeHeaders": ["ETag"],
       "MaxAgeSeconds": 3000
     }
   ]
   ```

   * Click **Save changes** to apply the configuration.

   ![Save CORS S3 Settings](/images/5-Workshop/5.7-S3/5.7.1-create-s3-bucket/S3UpLoad6.4.png)

#### Explanation:
Configuring the CORS policy on the S3 Upload Bucket allows cross-origin requests from the React frontend application (running locally at `http://localhost:5173` or in production) to directly upload objects to S3 via presigned URLs, bypassing browser Same-Origin Policy blocks.
