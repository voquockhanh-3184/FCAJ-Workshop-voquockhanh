---
title: "Worklog Week 9"
date: 2026-06-19
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---



### Week 9 Objectives:

* Implement user authentication utilizing Amazon Cognito and Amazon SES.
* Migrate the existing Express backend onto AWS Lambda.
* Secure endpoints and protect the API using API Gateway JWT Authorizer.

### Tasks to be Implemented This Week:

| Day | Task | Start Date | Completion Date | Tools / Platforms |
| --- | --- | --- | --- | --- |
| Mon | - **Database Optimization:** <br>&emsp; + Check and verify schemas in MongoDB Compass <br>&emsp; + Create a `unique sparse index` for `cognitoSub` inside the `nguoidungs` collection | 15/06/2026 | 15/06/2026 | [MongoDB Compass](https://www.mongodb.com/docs/compass/) |
| Tue | - **Backend Migration to Lambda:** <br>&emsp; + Wrap the Express.js application into an AWS Lambda handler using serverless-express <br>&emsp; + Adjust database connection logic to run efficiently within a serverless lifecycle | 16/06/2026 | 16/06/2026 | AWS Lambda |
| Wed | - **Authentication Flow Testing:** <br>&emsp; + Test the student registration flow <br>&emsp; + Verify OTP email delivery via Amazon SES <br>&emsp; + Ensure user profiles are accurately synchronized into MongoDB upon verification | 17/06/2026 | 17/06/2026 | [Amazon Cognito](https://docs.aws.amazon.com/cognito/) |
| Thu | - **API Gateway Integration:** <br>&emsp; + Set up Amazon API Gateway as a proxy to the Lambda Backend API <br>&emsp; + Configure a JWT Authorizer linked to the Cognito User Pool | 18/06/2026 | 18/06/2026 | Amazon API Gateway |
| Fri | - **End-to-End API Security Testing:** <br>&emsp; + Perform baseline integration testing on protected routes <br>&emsp; + Validate token decoding, route expiration, and error handling for unauthorized requests | 19/06/2026 | 19/06/2026 | Postman |

### Week 9 Key Results:

* Successfully established a complete registration, login, and secure email OTP authentication loop using Amazon Cognito and SES.
* Optimized database indexing by maintaining data integrity with a unique sparse index for `cognitoSub` tracking.
* Migrated the monolithic Express backend to a functional AWS Lambda Serverless Backend API layer.
* Successfully routing traffic and verifying requests via basic integration tests on Amazon API Gateway.
* Ensured robust profile synchronization mechanisms where verified identities immediately propagate into MongoDB collections.