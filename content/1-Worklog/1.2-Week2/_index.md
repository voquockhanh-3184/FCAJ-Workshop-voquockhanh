---
title: "Worklog Week 2"
date: 2026-05-01
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

## FCAJ WORKLOG - WEEK 02: SERVERLESS ARCHITECTURE & INTEGRATION

**Performed by:** Vo Quoc Khanh  
**Group:** KQPSV Group  

---

### Week 2 Objectives:

* **Understand Serverless Architecture:** Learn about AWS Serverless components and how services interact to handle a single request.
* **Master Serverless Request Lifecycle:**
  * Client sends a request.
  * Amazon API Gateway receives and routes the request.
  * AWS Lambda processes the business logic.
  * Amazon DynamoDB stores the persistent data.
* **Deploy & Integrate Core Services:**
  * HTTP API on Amazon API Gateway.
  * AWS Lambda Function.
  * Amazon DynamoDB NoSQL Database.
* **Development Experience:** Get hands-on experience building Serverless applications using Node.js.

---

### Tasks to be implemented during this week:

| Day | Tasks | Start Date | Completion Date | Reference (Cloud Journey) |
| :--- | :--- | :--- | :--- | :--- |
| **Day 2** | - Explore Serverless architecture on AWS.<br>- Understand Serverless Computing concepts.<br>- Analyze the workflow: Client → API Gateway → Lambda → DynamoDB. | 27/04/2026 | 27/04/2026 | [Serverless Backend with Lambda, S3, and DynamoDB](https://000078.awsstudygroup.com/) |
| **Day 3** | - Learn AWS Lambda fundamentals.<br>- Understand Lambda Functions, Node.js v24 runtime, and ES Module (`.mjs`).<br>- Configure Execution Roles and IAM Permissions. | 28/04/2026 | 28/04/2026 | [Serverless Automation with AWS Lambda](https://000022.awsstudygroup.com) |
| **Day 4** | - Study Amazon DynamoDB.<br>- Grasp NoSQL Database concepts, Tables, Partition Keys, and write operations. | 29/04/2026 | 29/04/2026 | [NoSQL Database Essentials with Amazon DynamoDB](https://000060.awsstudygroup.com) |
| **Day 5** | - **Hands-on Lab:**<br>&emsp; + Create a DynamoDB Table with Partition Key `userId`.<br>&emsp; + Write a Lambda Function using Node.js v24.<br>&emsp; + Integrate `@aws-sdk/client-dynamodb` to store data. | 30/04/2026 | 30/04/2026 | [Building Serverless CRUD with Lambda and DynamoDB](https://000133.awsstudygroup.com/) |
| **Day 6** | - **Hands-on Lab:**<br>&emsp; + Create an HTTP API on Amazon API Gateway.<br>&emsp; + Configure `POST /users` route and set up CORS.<br>&emsp; + Verify the whole integration using `curl`. | 01/05/2026 | 01/05/2026 | [Building Serverless APIs](https://000066.awsstudygroup.com/) |

---

### Week 2 Achievements:

* **Architectural Knowledge:** Fully understood the operational model and benefits of Serverless Architecture on AWS.
* **Data Persistence:** Successfully created an **Amazon DynamoDB** NoSQL table with `userId` as the Partition Key.
* **Function Deployment:** Successfully built and deployed an **AWS Lambda Function** using **Node.js v24**, utilizing **ES Modules (`.mjs`)** and the modern `@aws-sdk/client-dynamodb`.
* **API Gateway Provisioning:** Successfully configured an **API Gateway HTTP API** with a `POST /users` route and enabled **CORS** for external requests.
* **End-to-End Integration:** Tested the entire integration flow via `curl`. Verified that data sent by the client is properly processed by Lambda and successfully stored in DynamoDB.
