---
title : "S3 Naming Conventions and Prefix Policies"
date : 2024-01-01 
weight : 2
chapter : false
pre : " <b> 5.7.2. </b> "
---

Examora utilizes a single shared S3 Upload Bucket and isolates stored resources logically using path prefixes according to specific business entities:

| File Type | Upload Type | Proposed Prefix | Upload Permissions |
| :--- | :--- | :--- | :--- |
| **User Avatar** | `avatar` | `avatars/{userId}/` | ADMIN, TEACHER, STUDENT |
| **Class Cover Image** | `classCover` | `classes/{classId}/cover/` | ADMIN, TEACHER |
| **Exam Illustration Image** | `examImage` | `exams/{examId}/images/` | ADMIN, TEACHER |
| **Raw Word Document Import** | `wordImport` | `imports/word/raw/{teacherId}/` | ADMIN, TEACHER |

#### Benefits:
*   **Structured Resource Storage:** Separates storage objects into logical directory trees on the S3 bucket.
*   **Granular Security Validation:** The Lambda backend validates the caller's Cognito JWT and validates group/role permissions prior to generating the Presigned URL, preventing unauthorized operations or overwriting of other users' assets.
