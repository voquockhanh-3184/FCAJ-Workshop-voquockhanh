---
title: "Worklog Week 10"
date: 2026-06-26
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Week 10 Objectives:

* Migrate the file upload flow to the S3 Upload Bucket using Presigned URLs.
* Decouple the Word document import feature into a separate AWS Lambda function for asynchronous processing.

### Tasks to be Implemented This Week:

| Day | Task | Start Date | Completion Date | Tools / Platforms |
| --- | --- | --- | --- | --- |
| Mon | - **S3 Prefix Convention Design:** <br>&emsp; + Propose and define the prefix naming conventions in the S3 Upload Bucket <br>&emsp; + Categorize paths for avatars, class images, exam images, question images, and Word imports | 22/06/2026 | 22/06/2026 | [cloudjourney.awsstudygroup.com](https://000057.awsstudygroup.com/) |
| Tue | - **Presigned URL Generation Setup:** <br>&emsp; + Implement S3 Presigned URL generation logic inside the main Backend API <br>&emsp; + Restrict and validate file types and sizes before generating upload tokens | 23/06/2026 | 23/06/2026 | AWS SDK / Node.js |
| Wed | - **Asynchronous Lambda Handler Development:** <br>&emsp; + Develop a standalone Lambda function dedicated to parsing `.docx` files <br>&emsp; + Integrate a text/document parsing library within the serverless environment | 24/06/2026 | 24/06/2026 | AWS Lambda / S3 Trigger |
| Thu | - **File Upload Integration & Prefix Verification:** <br>&emsp; + Test uploading `.docx` files using the generated Presigned URLs <br>&emsp; + Verify that the uploaded objects appear correctly under the `imports/word/raw/` prefix in S3 | 25/06/2026 | 25/06/2026 | [Amazon S3 User Guide](https://docs.aws.amazon.com/AmazonS3/latest/userguide/) |
| Fri | - **End-to-End Async Import Testing:** <br>&emsp; + Test the full asynchronous flow from S3 event triggers to the Lambda processor <br>&emsp; + Validate that extracted questions are correctly parsed and saved into the MongoDB cluster | 26/06/2026 | 26/06/2026 | MongoDB Atlas / CloudWatch |

### Week 10 Key Results:

* Successfully operationalized S3 Presigned URLs for all core file upload flows, enhancing application performance and offloading backend traffic.
* Enforced structural data organization where files are systematically stored under their designated S3 prefixes.
* Developed an asynchronous Word Import Lambda capable of parsing raw `.docx` structures independently.
* Achieved successful integration where parsed questions and exam structures are seamlessly extracted and persisted into MongoDB collections.