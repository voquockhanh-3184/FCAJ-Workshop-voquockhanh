---
title : "Verify SQS and Lambda Grading Worker Pipeline"
date : 2024-01-01 
weight : 4
chapter : false
pre : " <b> 5.8.4. </b> "
---

#### Step-by-Step Instructions:

1. Launch the Frontend Application Locally and Take an Exam:
   * Start your local React frontend server -> authenticate using a student account.
   * Open the exams catalog -> select any exam -> choose answer options for the questions.

   ![Student Taking an Exam](/images/5-Workshop/5.8-SQS-Lambda-Grading-Worker/5.8.4-test-grading-pipeline/TestSQS1.png)

2. Submit Exam and Await Results:
   * Once answers are selected -> click **Submit**.
   * The application alerts the user that the exam was submitted successfully and is currently being graded.
   * Because the Backend API returns an HTTP `202 Accepted` code and pushes the transaction metadata directly to SQS, the Lambda Grading Worker calculates the scores asynchronously in the background. The user interface updates to display the final grade within a few seconds without requiring a manual page refresh.

   ![Successful Exam Submission](/images/5-Workshop/5.8-SQS-Lambda-Grading-Worker/5.8.4-test-grading-pipeline/TestSQS2.png)

   ![Grades Displayed after Background Processing](/images/5-Workshop/5.8-SQS-Lambda-Grading-Worker/5.8.4-test-grading-pipeline/TestSQS3.png)

3. Verify Logs on Amazon CloudWatch:
   * Go to the CloudWatch Logs console for the `examora-grading-worker-dev` Lambda function -> open the latest Log Stream.
   * Verify that the worker parsed the SQS message payload, established database connections, executed the scoring rules, and updated the document attributes successfully.

   ![CloudWatch Logs analysis](/images/5-Workshop/5.8-SQS-Lambda-Grading-Worker/5.8.4-test-grading-pipeline/TestSQS4.png)

#### Summary:
The verification test proves that the asynchronous exam grading pipeline using **Amazon SQS** and **AWS Lambda** works as designed. Isolating the grading execution logic from frontend HTTP loops optimizes backend response times and prevents serverless connection exhaustion when multiple students submit exams at the same time.
