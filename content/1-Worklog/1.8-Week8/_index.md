---
title: "Worklog Week 8"
date: 2026-06-12
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---


### Week 8 Objectives:

* Define the MVP scope, review the current source code, and finalize the AWS Serverless Hybrid architecture for the Examora project.
* Determine the detailed deployment roadmap by analyzing the frontend and backend module structures.
* Prepare technical documentation for the hybrid model and break down infrastructure tasks into the shared management backlog.

### Tasks to be Implemented This Week:

| Day | Task | Start Date | Completion Date | Tools / Platforms |
| --- | --- | --- | --- | --- |
| Mon | - **Team Meeting & System Code Review:** <br>&emsp; + Evaluate the current state of Frontend & Backend source code <br>&emsp; + Identify reusable modules <br>&emsp; + Analyze the limitations of the legacy architecture | 08/06/2026 | 08/06/2026 | GitHub |
| Tue | - **Self-study the Storage Service Group:** <br>&emsp; + Learn about S3 buckets <br>&emsp; + Manage object keys and prefixes <br>&emsp; + Configure CORS | 09/06/2026 | 09/06/2026 | [AWS Management Console](https://cloudjourney.awsstudygroup.com/) |
| Wed | - **Design Hybrid Architecture:** <br>&emsp; + Draft data flows between API Gateway, Lambda, and the legacy backend <br>&emsp; + Propose cloud integration solutions for the current database <br>&emsp; + Define boundaries for the MVP scope | 10/06/2026 | 10/06/2026 | Draw.io |
| Thu | - **Read MongoDB Atlas Network Access Documentation:** <br>&emsp; + Research serverless application connectivity <br>&emsp; + Implement connection via a public TLS endpoint | 11/06/2026 | 11/06/2026 | [MongoDB Atlas Dashboard](https://www.mongodb.com/docs/atlas/) |
| Fri | - **Standardize Backlog & Finalize Planning:** <br>&emsp; + Break down the architecture diagram into specific infrastructure tasks <br>&emsp; + Finalize the list of modules migrating to Serverless <br>&emsp; + Assign deployment tasks to team members | 12/06/2026 | 12/06/2026 | Jira Software |

### Week 8 Key Results:

* Successfully finalized the MVP scope definition for the Examora project, preventing over-scoping.
* Gained a comprehensive understanding of the current frontend and backend architecture, pinpointing technical bottlenecks for optimization.
* Clearly classified modules to be retained versus modules to be migrated to the AWS Serverless architecture.
* Formulated, standardized, and successfully finalized the initial infrastructure deployment backlog on the team's task management tool.
* Acquired a deep understanding of setting up storage with Amazon S3 and configuring secure network access (IP Whitelisting/TLS) to MongoDB Atlas in a serverless environment.
* Completed the draft blueprint of the AWS Serverless Hybrid architecture, laying the groundwork for Infrastructure as Code (IaC) implementation in the upcoming week.