---
title: "Worklog Week 6"
date: 2026-05-29
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---


### Week 6 Objectives:

* Research and implement a centralized monitoring system on AWS to track application operational status, collect logs, and support the debugging process.

* Get familiar with monitoring and error analysis tools:

  * Amazon CloudWatch.
  * AWS X-Ray.

* Build a Continuous Integration and Continuous Deployment (CI/CD) Pipeline to:

  * Automatically test source code.
  * Automatically build the application.
  * Automatically deploy infrastructure to AWS.

* Standardize team workflow by integrating CI/CD with the source control management system.


### Tasks to Implement This Week:

| Day | Task | Start Date | Completion Date | Documentation Source |
| --- | --- | --- | --- | --- |
| Mon | - Research Monitoring systems on AWS: <br>&emsp; + Amazon CloudWatch Logs <br>&emsp; + Log Groups and Log Streams <br>&emsp; + Monitoring Lambda and API Gateway status <br>&emsp; + Analyzing errors through Logs | 2026-05-25 | 2026-05-25 | [AWS CloudWatch Documentation](https://000008.awsstudygroup.com/) |
| Tue | - **Practice AWS X-Ray:** <br>&emsp; + Enable Distributed Tracing <br>&emsp; + Track request flow between services <br>&emsp; + Analyze latency <br>&emsp; + Identify bottlenecks in the system | 2026-05-26 | 2026-05-26 | [AWS X-Ray Documentation](https://000140.awsstudygroup.com/3-build-frontend-pipeline/) |
| Wed | - Research CI/CD Pipeline: <br>&emsp; + Concepts of Continuous Integration and Continuous Deployment <br>&emsp; + Automated build, test, and deploy workflows <br>&emsp; + Overview of GitHub Actions / AWS CodePipeline | 2026-05-27 | 2026-05-27 | [AWS CI/CD Documentation](https://000017.awsstudygroup.com/) |
| Thu | - **Practice Building Pipeline:** <br>&emsp; + Create CI/CD Workflow configuration file <br>&emsp; + Configure trigger on code merge into main branch <br>&emsp; + Run code checks (linting) <br>&emsp; + Perform automated build and testing | 2026-05-28 | 2026-05-28 | [GitHub Actions Documentation](https://000017.awsstudygroup.com/) |
| Fri | - **Automated Deployment to AWS:** <br>&emsp; + Configure AWS Credentials for the Pipeline <br>&emsp; + Connect CI/CD with AWS CDK <br>&emsp; + Automatically deploy Infrastructure to AWS <br>&emsp; + Verify deployment results | 2026-05-29 | 2026-05-29 | [AWS CDK Documentation](https://000017.awsstudygroup.com/) |


### Week 6 Achievements:

* Understood the role of Monitoring systems in cloud application operations.

* Successfully configured Amazon CloudWatch:

  * Centralized log collection for AWS Lambda.
  * Monitored API Gateway execution logs.
  * Analyzed errors using CloudWatch Logs.

* Successfully enabled AWS X-Ray:

  * Tracked request processing flows between services.
  * Observed Distributed Tracing service maps.
  * Analyzed latency of each component.
  * Assisted in identifying system bottlenecks.

* Successfully built the CI/CD Pipeline workflow:

  * Created the Pipeline configuration file.
  * Automated triggers upon changes to the `main` branch.
  * Executed the following steps:
    * Source code linting.
    * Running tests.
    * Building the application.
    * Deploying Infrastructure using AWS CDK.

* Finalized the automated deployment process, reducing manual interventions and ensuring a consistent deployment environment across team members.