---
title : "Verify Presigned URL Endpoint and S3 Upload"
date : 2024-01-01 
weight : 5
chapter : false
pre : " <b> 5.7.5. </b> "
---

#### Objectives:
Verify that the presigned URL endpoint is securely guarded by API Gateway and the Cognito JWT Authorizer, and confirm that target files uploaded using the presigned URL are successfully written to the S3 Upload Bucket.

---

#### Test Case 1: Invoking Presigned URL Endpoint without a JWT
*   **Expected Result**: API Gateway rejects the request with an HTTP `401 Unauthorized` status.
*   **Actual Result**:

   ![Test Case 1: Request without JWT](/images/5-Workshop/5.7-S3/5.7.5-test-presigned-url-upload/TestURL1.png)

---

#### Test Case 2: Invoking Presigned URL Endpoint with a Valid JWT
*   **Step 1**: Log in to a teacher account on the Examora frontend to obtain the Cognito JWT credentials.
*   **Step 2**: Open browser DevTools -> navigate to the **Console** tab, and dispatch an HTTP request containing the Cognito JWT in the `Authorization` header.
*   **Expected Result**: HTTP Status returns `200` along with a JSON body mapping:
   ```json
   {
     "uploadUrl": "https://...",
     "bucket": "...",
     "objectKey": "imports/word/raw/<teacherId>/<uuid>.docx",
     "method": "PUT",
     "expiresIn": 300
   }
   ```
*   **Actual Result**:

   ![Test Case 2: Request with Valid JWT](/images/5-Workshop/5.7-S3/5.7.5-test-presigned-url-upload/TestURL2.png)

---

#### Test Case 3: Upload File Using the Presigned URL
*   Immediately following Test Case 2, copy and execute the script below in the browser Console to invoke a direct binary PUT request to the S3 Upload Bucket using the signed URL:

```javascript
const input = document.createElement("input");
input.type = "file";
input.accept = ".docx";

input.onchange = async () => {
  const file = input.files[0];

  const res = await fetch(window.examoraUploadUrl, {
    method: "PUT",
    headers: {
      "Content-Type": "application/vnd.openxmlformats-officedocument.wordprocessingml.document"
    },
    body: file
  });

  console.log("S3 upload status:", res.status);
  console.log("S3 key:", window.examoraUploadKey);
};

input.click();
```

*   **Step 1**: Choose a `.docx` file from your local disk using the generated file selector.
*   **Actual Result**: The Console displays `S3 upload status: 200` (success).

   ![Test Case 3: S3 Upload Status Log](/images/5-Workshop/5.7-S3/5.7.5-test-presigned-url-upload/TestURL3.png)

*   **Step 2**: Audit upload storage status in the AWS S3 Console:
    *   Navigate to S3 **Buckets** -> open your bucket -> select **Objects** -> browse to the directory `imports/word/raw/<teacherId>/`.
    *   Verifying that the newly uploaded `.docx` file exists in S3 confirms that the direct upload workflow is functional.

   ![Audit Uploaded Object on S3](/images/5-Workshop/5.7-S3/5.7.5-test-presigned-url-upload/TestURL4.png)
