---
title: "Worklog Week 11"
date: 2026-07-06
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---


### Week 11 Objectives:

* Decouple the exam grading logic from the submission request using an SQS Grading Queue and a Lambda Grading Worker.
* Establish an asynchronous, event-driven architecture to optimize exam submission processing and handle high-concurrency traffic.

### Tasks to be Implemented This Week:

| Day | Task | Start Date | Completion Date | Tools / Platforms |
| --- | --- | --- | --- | --- |
| Mon | - **SQS Queue Configuration:** <br>&emsp; + Provision and configure the Amazon SQS Grading Queue <br>&emsp; + Set up dead-letter queues (DLQ) and retry policies for failed grading tasks | 29/06/2026 | 29/06/2026 | AWS Management Console |
| Tue | - **Submission Logic Refactoring:** <br>&emsp; + Refactor backend submission handling to immediately save submissions with a "grading" status <br>&emsp; + Implement message publishing payload to push grading jobs into the SQS queue | 30/06/2026 | 30/06/2026 | AWS SDK / Node.js |
| Wed | - **Frontend Submission & SQS Integration Testing:** <br>&emsp; + Test exam submissions triggered from the frontend client <br>&emsp; + Verify the initial "grading" status update in MongoDB and validate the message payload sent to SQS | 01/07/2026 | 01/07/2026 | [Amazon SQS Developer Guide](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-basic-architecture.html) |
| Thu | - **Lambda Grading Worker Development:** <br>&emsp; + Create a standalone Lambda Grading Worker triggered by SQS events <br>&emsp; + Write grading logic to evaluate scores, calculate correct/incorrect counts, and format answer breakdowns | 02/07/2026 | 02/07/2026 | AWS Lambda |
| Fri | - **Worker Evaluation & MongoDB Verification:** <br>&emsp; + Inspect and verify the final grading output after worker execution <br>&emsp; + Validate accurate database persistence for score metrics, itemized correct/incorrect statuses, and detailed choice analysis | 03/07/2026 | 03/07/2026 | MongoDB Compass |

### Week 11 Key Results:

* Successfully decoupled the heavy grading operation from the main user request thread, drastically reducing API response latency.
* Configured the Amazon SQS Grading Queue infrastructure to serve as a reliable buffer for high-volume exam submissions.
* Developed and deployed the AWS Lambda Grading Worker to parse asynchronous payloads and update final outcomes independently.
* Verified seamless end-to-end processing where submissions shift dynamically from "grading" to fully assessed schemas in MongoDB Compass.