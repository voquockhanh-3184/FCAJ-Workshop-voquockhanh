---
title : "Create Cognito Groups"
date : 2024-01-01 
weight : 3
chapter : false
pre : " <b> 5.4.5. </b> "
---

#### Objective:
Initialize **Cognito User Groups** to categorize user roles for role-based access control (RBAC) within the Examora platform.

The Examora examination management system has three primary user categories:

| Cognito Group | Role | Permissions Description |
|---|---|---|
| **ADMIN** | System Administrator | Manages the entire infrastructure, configures platform-wide settings. |
| **TEACHER** | Teacher / Instructor | Manages classrooms, drafts exams, manages the question bank. |
| **STUDENT** | Student / Candidate | Takes online multiple-choice exams, reviews individual results. |

**Mechanism of Action:**
*   **Cognito Groups** are used to cluster users based on business roles. Upon successful authentication, Cognito injects the group memberships into the JWT ID Token via the `cognito:groups` claim.
*   The Backend services (Lambda API) decode the incoming JWT and read the `cognito:groups` claim to grant or deny access to resources (authorization).

#### Configuration Steps:

1. In the detailed configuration view of the created User Pool, switch to the **Groups** tab -> Click **Create group**.
2. Create three groups sequentially, using the exact names: `ADMIN`, `TEACHER`, and `STUDENT` -> Click **Create group** to complete each one.

![Create Group](/images/5-Workshop/5.4-Cognito-SES/COGNITO4.6.png)
