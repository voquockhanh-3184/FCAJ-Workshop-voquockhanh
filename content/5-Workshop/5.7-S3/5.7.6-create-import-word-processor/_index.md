---
title : "Create Lambda Import Word Processor"
date : 2024-01-01 
weight : 6
chapter : false
pre : " <b> 5.7.6. </b> "
---

#### Objectives:
Initialize an independent Lambda function named `examora-import-word-processor-dev` to perform the following operations:
*   Receive event notifications triggered by `.docx` uploads in the S3 bucket.
*   Fetch and read the uploaded Word files from the S3 Upload Bucket.
*   Parse questions from the Word document layout.
*   Save the structured questions into MongoDB Atlas.
*   Log the import trace events to CloudWatch Logs for auditability.

*(For a detailed step-by-step guide on establishing Lambda functions, please refer back to section 5.5)*.

---

#### Configure S3 ObjectCreated Trigger:
We must set up an event notification trigger on the S3 Upload Bucket so that the `examora-import-word-processor-dev` function is automatically invoked whenever a `.docx` file is successfully uploaded.

1. Step-by-Step Instructions:
   * Open the **Amazon S3** console -> select your bucket -> navigate to the **Properties** tab -> scroll down to the **Event notifications** section -> click **Create event notification**.

   ![Event Notification S3](/images/5-Workshop/5.7-S3/5.7.6-create-import-word-processor/LambdaWord1.png)

   * Input the configuration parameters:
     * **Event name**: Choose a descriptive name (e.g., `ImportWordTrigger`).
     * **Prefix** (optional): Set to `imports/word/raw/` to ensure the trigger only responds to raw file uploads.
     * **Event types**: Check the box for **All object create events**.

   ![Event Name Configuration](/images/5-Workshop/5.7-S3/5.7.6-create-import-word-processor/LambdaWord2.png)

   ![Select Event Types](/images/5-Workshop/5.7-S3/5.7.6-create-import-word-processor/LambdaWord3.png)

   * Scroll down to **Destination**:
     * **Destination**: Select **Lambda function**.
     * **Lambda function**: Choose your `examora-import-word-processor-dev` function.
   * Click **Save changes** to apply.

   ![Configure Destination](/images/5-Workshop/5.7-S3/5.7.6-create-import-word-processor/LambdaWord4.png)

2. Implement Backend Processing Logic:
   * The processor codebase should implement the following primary execution logic:
     * `handler(event)`: The main entry point triggered by S3 ObjectCreated notifications.
     * `getS3ObjectBuffer(bucket, key)`: Fetches the file buffer from S3.
     * `parseExamIdFromKey(key)`: Parses the target `examId` from the storage path key.
     * `parseQuestionsFromWord(buffer)`: Utilizes the `mammoth` library to parse Word structure into HTML/text format and extracts questions.
     * `normalizeQuestions(rawQuestions)`: Maps raw questions data to the `BaiGiang.danhSachCauHoi` database schema.
     * `saveQuestionsToMongo(examId, questions)`: Connects to MongoDB Atlas and inserts the questions.
     * `getMongoUriFromSecretsManager()`: Retrieves the database connection URI securely from AWS Secrets Manager.
   * Install the necessary NPM dependencies in the Lambda source folder:
     ```bash
     npm install @aws-sdk/client-s3 @aws-sdk/client-secrets-manager mammoth mongodb
     ```
   * Package the application files into a `.zip` archive and deploy it to the `examora-import-word-processor-dev` Lambda function.

   ![Deploy Lambda Import Word Processor](/images/5-Workshop/5.7-S3/5.7.6-create-import-word-processor/LambdaWord5.png)
