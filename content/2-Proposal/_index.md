---
title: "Proposal"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Examora - Online Exam Platform
## An AWS Serverless Solution for Online Examination

### 1. Executive Summary
Examora is an online multiple-choice examination platform designed for three main user groups: administrators, teachers, and students. The system supports user registration and sign-in, class management, exam and question management, Word-based question import, online exam taking, automatic grading, and exam history tracking.

The proposed architecture migrates Examora to an AWS Serverless model. The React/Vite frontend is deployed with AWS Amplify Hosting and connected to a custom domain through Route 53. User authentication is handled by Amazon Cognito, while Amazon SES is used for email OTP and password reset flows. The existing Express backend is packaged and deployed as an AWS Lambda function behind Amazon API Gateway HTTP API with a Cognito JWT Authorizer. MongoDB Atlas remains the primary database to avoid unnecessary schema migration and data restructuring.

File processing and long-running tasks are separated into asynchronous flows. Uploads such as avatars, class images, exam images, question images, and Word files are stored in an S3 Upload Bucket using presigned URLs. Uploaded Word files trigger a Lambda Import Word Processor to parse questions and save them to MongoDB. Exam submissions are decoupled from grading through Amazon SQS and a Lambda Grading Worker, reducing request latency and improving retry capability.

The goal of this proposal is to build a secure, scalable, and practical serverless web platform while preserving the core business logic already implemented in Examora.

### 2. Problem Statement
### What’s the Problem?
The initial version of Examora follows a traditional web application model with a React frontend, Express backend, and MongoDB database. While it supports the main business functions, several limitations appear when moving toward a real deployment environment:

- Self-managed JWT/local-token authentication is harder to scale and does not provide a clean built-in flow for email OTP, password reset, and centralized group-based authorization.
- File uploads through backend/local storage are not suitable for a serverless runtime because Lambda should not be used as persistent file storage.
- Grading directly inside the submission request can slow down the user request and makes retry handling more difficult.
- Word import is a file-processing workload and should not block the main backend request.
- Backend services need clearer secret management, logging, tracing, and IAM-based permission boundaries.
- The frontend needs a simple deployment method that supports custom domain routing and React SPA behavior.

### The Solution
Examora uses an AWS Serverless architecture to separate the system into clear functional blocks:

- Route 53 manages the `examora.click` domain.
- AWS Amplify Hosting deploys the React/Vite frontend and handles rewrite rules for React Router.
- Amazon Cognito manages the user pool, email/password sign-in, and Cognito Groups: `ADMIN`, `TEACHER`, and `STUDENT`.
- Amazon SES sends registration OTP and password reset emails through Cognito.
- Amazon API Gateway HTTP API validates Cognito JWTs before routing requests to the Backend API Lambda.
- AWS Lambda runs the existing Express backend through `serverless-http`.
- MongoDB Atlas remains the main database for users, classes, exams, questions, and results.
- An S3 Upload Bucket stores application files through presigned URLs.
- A Lambda Import Word Processor handles Word file parsing after upload.
- Amazon SQS and a Lambda Grading Worker process exam grading asynchronously.
- AWS Secrets Manager stores the MongoDB URI and sensitive configuration.
- CloudWatch Logs and X-Ray provide logging, debugging, and request tracing.

### 3. Solution Architecture
The Examora architecture is organized into frontend hosting, authentication, core API, upload/import pipeline, grading pipeline, monitoring, and security configuration.

![Examora Architecture](/images/2-Proposal/Examora_Architecture_Final2.png)

### AWS Services Used

- **Route 53**: Manages the `examora.click` domain and points it to Amplify Hosting.
- **AWS Amplify Hosting**: Deploys the React/Vite frontend, serves the SPA, and supports custom domains.
- **Amazon Cognito**: Manages sign-up, sign-in, JWTs, and Cognito Groups.
- **Amazon SES**: Sends OTP and password reset emails.
- **Amazon API Gateway**: Provides the public API endpoint and validates JWTs with a Cognito Authorizer.
- **AWS Lambda**: Runs the Backend API, Import Word Processor, and Grading Worker.
- **Amazon S3 Upload Bucket**: Stores avatars, class images, exam images, question images, and Word import files.
- **Amazon SQS**: Queues grading jobs and decouples submission from grading.
- **AWS Secrets Manager**: Stores the MongoDB URI and sensitive configuration.
- **Amazon CloudWatch**: Collects Lambda logs and runtime errors.
- **AWS X-Ray**: Traces requests and helps analyze latency.
- **AWS IAM**: Applies least-privilege permissions to each Lambda function.
- **MongoDB Atlas**: External managed database used as the primary business database.

### Component Design

- **Frontend**: The React/Vite SPA is built and deployed to Amplify Hosting. It authenticates with Cognito and sends JWTs in the `Authorization` header when calling API Gateway.
- **Authentication**: Amazon Cognito manages user authentication, email OTP codes, and role-based access control (Admin, Teacher, Student), synchronizing user roles to the primary database.
- **Core API**: API Gateway receives frontend requests, validates JWTs, and forwards authorized requests to the Backend API Lambda.
- **Backend API**: The Express backend handles class management, exam management, question management, profile synchronization, uploads, exam history, and submission logic.
- **Upload Pipeline**: The backend generates presigned URLs, the frontend uploads files directly to S3, and the backend stores object keys in MongoDB.
- **Word Import Pipeline**: S3 ObjectCreated events trigger the Import Word Processor Lambda to parse `.docx` files and save questions to MongoDB.
- **Grading Pipeline**: The backend saves submissions as pending grading, sends grading jobs to SQS, and the Grading Worker updates the final result in MongoDB.
- **Monitoring and Security**: Lambda functions send logs to CloudWatch, use X-Ray tracing, read secrets from Secrets Manager, and operate under dedicated IAM roles.

### 4. Technical Implementation
**Implementation Phases**

- **Authentication migration**: Configure Cognito User Pool, SES, Cognito Groups, and update the frontend/backend to use Cognito JWTs.
- **Backend migration to Lambda**: Separate the Express app from `server.listen()`, add a Lambda handler, package the backend, and deploy the Backend API Lambda.
- **API Gateway configuration**: Initialize the HTTP API integrated with the Backend Lambda, configure a secure JWT Authorizer for the endpoints, set up CORS settings, and perform baseline connectivity checks.
- **File upload migration**: Create the S3 Upload Bucket, grant IAM permissions to the Backend API Lambda, implement the presigned URL endpoint, and migrate avatar/image/Word uploads to S3.
- **Asynchronous Word Import**: Deploys a dedicated Lambda function triggered automatically by S3 upload events to parse question documents and store them in the database.
- **Grading separation**: Create the SQS Grading Queue and Grading Worker Lambda, then update the backend to save submissions and send grading jobs to SQS.
- **Frontend deployment**: Build the React/Vite frontend, deploy it to Amplify Hosting, configure React Router rewrites, and connect it to API Gateway.
- **Domain and observability**: Configure Route 53 for `examora.click`, verify CloudWatch Logs and X-Ray, and finalize production environment variables.

**Technical Requirements**

- The React/Vite frontend must use `VITE_BACKEND_URL` pointing to the API Gateway endpoint.
- The Backend Lambda function requires environment variables to configure database connections, reference related AWS service resources, and define allowed CORS origins.
- The MongoDB URI must be stored in Secrets Manager instead of being hard-coded or placed directly in normal environment variables.
- The S3 Upload Bucket remains private and is accessed through presigned PUT/GET URLs.
- API Gateway uses a Cognito JWT Authorizer to reject unauthenticated requests.
- The Backend Lambda function validates the incoming JWT tokens and synchronizes user profiles into the database.
- IAM roles must be separated by function: Backend API, Import Word Processor, and Grading Worker.
- CORS must allow local development, the Amplify domain, and the official custom domain.

### 5. Timeline & Milestones
*   **Pre-Internship:** Plan initial project scope and evaluate the baseline legacy Examora architecture.
*   **Internship Period (April - July):**
    *   **April:** Research and practice using official AWS service documentation and tutorials.
    *   **May:** Plan requirements, design the system architecture, and draft AWS Architecture diagrams for Examora.
    *   **June - July:** Implement the cloud infrastructure, execute integration tests, and compile the project report.
*   **Post-Implementation:** Monitor, operate, and continuously optimize the serverless application resources.

### 6. Budget Estimation
You can review the cost estimate from the exported AWS Pricing Calculator file.
Or you can download the [Budget Estimation File](/images/2-Proposal/ExamoraCost.pdf).

### Infrastructure Costs

- AWS Amplify: $0.62/month (standard build instance, 1 GB stored data, 60 build minutes/month, 0 SSR requests).
- Amazon Cognito: $0.01/month (1,000 monthly active users, advanced security disabled).
- Amazon API Gateway: $0.01/month (HTTP API, 10,000 requests/month, 2 KB average request size).
- AWS Lambda: $0.00/month (10,000 requests/month, 512 MB ephemeral storage).
- Amazon S3 Standard: $0.16/month (5 GB/month, 5,000 PUT/COPY/POST/LIST requests, 50.000 GET requests).
- Amazon SQS: $0.00/month (low-volume standard queue requests).
- Amazon SES: $0.15/month (1,000 emails/month).
- AWS Secrets Manager: $0.50/month (1 secret, 20,000 API calls/month).
- Amazon Route 53: $0.50/month (1 hosted zone).
- AWS X-Ray: $0.01/month (1,000 requests/month, sampling rate 1).
- Amazon CloudWatch: $0.50/month (1 GB logs ingested and basic metrics/log usage).

Total: $2.46/month, $29.52/12 months.

Note: This is an AWS Pricing Calculator estimate. The actual cost may change depending on region, request volume, uploaded file size, number of users, and generated logs.

### 7. Risk Assessment
#### Risk Matrix

- Incorrect Cognito/JWT configuration: high impact, medium probability.
- CORS mismatch between Amplify domain, local development, and API Gateway: medium impact, high probability during deployment.
- Lambda timeout during Word import or grading: medium impact, medium probability.
- SQS messages not being processed correctly by the worker: high impact, low to medium probability.
- MongoDB Atlas network access or secret configuration error: high impact, medium probability.
- IAM permissions being too broad or missing required actions: high impact, medium probability.
- Unexpected increase in log or file upload cost: medium impact, low probability.

#### Mitigation Strategies

- Validate JWTs at both API Gateway and backend middleware layers.
- Use `FRONTEND_ORIGINS` to manage allowed origins for local development, Amplify, and the official domain.
- Move Word import and grading into dedicated Lambda functions to avoid blocking the main request flow.
- Log detailed metadata (including submission and candidate identifiers) during grading jobs to trace message flows in the message queue.
- Store the MongoDB URI in Secrets Manager and verify `secretsmanager:GetSecretValue` permissions for each Lambda.
- Scope IAM permissions to the required bucket, queue, and secret only.
- Configure CloudWatch log retention and AWS Budget Alerts for long-running environments.

#### Contingency Plans

- If the Grading Worker fails, the submission remains in MongoDB as pending grading and the job can be retried.
- If the Import Word Processor fails, the original Word file remains in the S3 Upload Bucket for reprocessing.
- If Amplify deployment fails, the application can be rolled back to a previous successful build in the Amplify Console.
- If Cognito groups are incorrect, an administrator can update the group in the Cognito Console and the user can sign in again to receive a new JWT.

### 8. Expected Outcomes
#### Technical Improvements

Examora moves from a traditional backend deployment model to an AWS Serverless architecture with centralized authentication, Lambda-based backend APIs, S3-based file uploads, asynchronous Word import, and SQS-based grading. The system reduces dependency on manually operated servers and becomes easier to debug through CloudWatch and X-Ray.

#### Long-term Value

- **Improve Teaching Efficiency & Productivity:** Enables teachers to minimize exam preparation time by automatically importing question banks from existing document files and eliminates manual grading effort through automatic and precise grading mechanisms.
- **Enhance Student Learning Experience:** Provides students with a convenient and user-friendly online testing platform to complete assessments anytime, anywhere, and review immediate grading results to track progress and self-improve.
- **Optimize Infrastructure & Operational Costs:** Helps educational institutions reduce information technology infrastructure expenses by leveraging cloud computing pay-as-you-go pricing, reducing physical server maintenance overhead while ensuring high system availability during large-scale examination periods.

