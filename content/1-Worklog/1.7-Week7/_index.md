---
title: "Worklog Week 7"
date: 2026-06-05
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---


### Week 7 Objectives:

* Finalize the project idea, select a specific application topic, and begin preparing the project proposal documentation.
* Draft the overall system architecture design and research the NoSQL DynamoDB database modeling approach.
* Initialize and synchronize the team's shared working environment (Project Kick-off).

### Tasks to Be Implemented During This Week:

| Day | Task | Start Date | Completion Date | Tools / Platforms |
| --- | --- | --- | --- | --- |
| Monday | - **Team Brainstorming & Topic Finalization:** <br>&emsp; + Discuss ideas and evaluate each member's strengths to select a practical project topic <br>&emsp; + Define the project scope and identify core features | 01/06/2026 | 01/06/2026 | Discord |
| Tuesday | - **Drafting Overall System Architecture:** <br>&emsp; + Design the architecture diagram <br>&emsp; + Identify the data flow between Frontend (S3), API Gateway, Cognito, Lambda, and DynamoDB services | 02/06/2026 | 02/06/2026 | Draw.io |
| Wednesday | - **Project Kick-off & Initial Setup:** <br>&emsp; + Create a shared Git repository for the team <br>&emsp; + Define the standard project folder structure using AWS CDK and push the initial framework to the repository for team members to clone locally | 03/06/2026 | 03/06/2026 | GitHub / AWS CDK |
| Thursday | - **Project Proposal Development:** <br>&emsp; + Create the detailed project proposal document <br>&emsp; + Describe the real-world problem, implementation plan, and task assignment for each team member | 04/06/2026 | 04/06/2026 | Google Docs |
| Friday | - **Research & DynamoDB Single-Table Design:** <br>&emsp; + Identify access patterns required by the frontend application <br>&emsp; + Apply the Single-Table Design approach by designing PK/SK structures with entity prefixes (USER#, ORDER#) | 05/06/2026 | 05/06/2026 | NoSQL Workbench |

### Challenges & Solutions:

* **Problem:** Team members faced difficulties when designing the DynamoDB database because they were familiar with the traditional relational database (SQL) approach. This resulted in the tendency to create multiple separate tables, which could increase costs and reduce optimization.

* **Solution:** The team conducted online discussions to list all required data access patterns from the frontend application. After that, the Single-Table Design approach was applied by using entity prefixes in partition keys (PK) and sort keys (SK) to store multiple related entities within a single DynamoDB table.

### Achievements in Week 7:

* Successfully finalized the project topic and clearly defined the scope of the real-world problem.
* Completed the overall system architecture diagram, providing a clear understanding of the data flow across AWS serverless services.
* Successfully created the initial project proposal document, including the implementation plan and detailed task assignment table.
* Designed the initial DynamoDB data model using the Single-Table Design approach, helping optimize costs and handle complex data queries efficiently.
* Established a synchronized project folder structure using AWS CDK and successfully distributed the initial source code framework to all team members' local environments.