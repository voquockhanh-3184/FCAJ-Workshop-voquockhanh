---
title: "Worklog Week 4"
date: 2026-05-15
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

## FCAJ WORKLOG - WEEK 04: INFRASTRUCTURE AS CODE WITH AWS CDK

**Performed by:** Vo Quoc Khanh  
**Group:** KQPSV Group  

---

### Week 4 Objectives:

* Learn about Infrastructure as Code (IaC) and how to manage AWS infrastructure through source code instead of manual operations on the AWS Console.
* Transition the deployment process from a Click-ops model to an automated model using AWS CDK.
* Build and manage Serverless infrastructure with source code, which helps to:
  * Easily reuse configurations.
  * Synchronize the development environment across team members.
  * Reduce configuration drift during deployment.
* Optimize costs during the learning and practice process:
  * Use resources that fit within the AWS Free Tier.
  * Limit Lambda resources such as Memory and Timeout.
  * Avoid unnecessary charges.

---

### Tasks to be implemented during this week:

| Day | Tasks | Start Date | Completion Date | Reference (Cloud Journey) |
| :--- | :--- | :--- | :--- | :--- |
| **Day 2** | - Learn about Infrastructure as Code (IaC):<br>&emsp;+ IaC concepts<br>&emsp;+ Benefits of managing infrastructure with code<br>&emsp;+ Comparison between Click-ops and IaC<br>&emsp;+ Overview of AWS CDK | 11/05/2026 | 11/05/2026 | [Cloud Development Kit (AWS CDK) Essentials](https://000038.awsstudygroup.com) |
| **Day 3** | - **Hands-on: Install AWS CDK:**<br>&emsp;+ Install the AWS CDK CLI via npm<br>&emsp;+ Initialize a CDK project with TypeScript<br>&emsp;+ Configure the AWS Account and Region | 12/05/2026 | 12/05/2026 | [Cloud Development Kit (AWS CDK) Essentials](https://000038.awsstudygroup.com) |
| **Day 4** | - **Hands-on: Initialize the CDK environment:**<br>&emsp;+ Run the `cdk bootstrap` command<br>&emsp;+ Create supporting resources for the deployment process<br>&emsp;+ Check the status of the CDK environment | 13/05/2026 | 13/05/2026 | [Infrastructure as Code Workshop Series](https://000102.awsstudygroup.com) |
| **Day 5** | - **Build Serverless infrastructure with AWS CDK:**<br>&emsp;+ Define a DynamoDB Table via code<br>&emsp;+ Configure `PAY_PER_REQUEST` for DynamoDB<br>&emsp;+ Create a Lambda Function<br>&emsp;+ Configure Runtime, Memory, Timeout, and Environment Variables | 14/05/2026 | 14/05/2026 | [AWS CDK Advanced](https://000076.awsstudygroup.com) |
| **Day 6** | - **Deploy and test the infrastructure:**<br>&emsp;+ Create an API Gateway connected to Lambda<br>&emsp;+ Deploy the CDK Stack to AWS<br>&emsp;+ Verify the resources created on the AWS Console | 15/05/2026 | 15/05/2026 | [AWS CDK Advanced](https://000076.awsstudygroup.com) |

---

### Week 4 Achievements:

* Understood the concept of Infrastructure as Code (IaC) and the role of managing infrastructure through source code in Cloud projects.

* Understood the difference between:
  * Manual deployment via the AWS Console (Click-ops).
  * Automated deployment using IaC tools.