---
title: "Worklog Week 12"
date: 2026-07-06
weight: 12
chapter: false
pre: " <b> 1.12. </b> "
---


### Week 12 Objectives:

* Deploy the frontend application onto AWS Amplify Hosting and prepare AWS Route 53 custom domain configurations.
* Complete integration testing, finalize the project proposal, and conclude the workshop report according to the new serverless architecture.

### Tasks to be Implemented This Week:

| Day | Task | Start Date | Completion Date | Tools / Platforms |
| --- | --- | --- | --- | --- |
| Mon | - **Frontend Build Verification:** <br>&emsp; + Verify the local production build using `npm run build` <br>&emsp; + Ensure the generated `dist/` directory contains `index.html` and all required static assets | 06/07/2026 | 06/07/2026 | Vite Documentation |
| Tue | - **Amplify Hosting Deployment:** <br>&emsp; + Connect the frontend Git repository to AWS Amplify Hosting <br>&emsp; + Configure environment variables and continuous deployment (CD) build settings | 07/07/2026 | 07/07/2026 | AWS Amplify Console |
| Wed | - **Client-Side Routing & Rewrite Configuration:** <br>&emsp; + Test React Router paths on Amplify (e.g., `/dang-nhap`, `/lop-hoc`, `/tai-khoan-cua-toi`) <br>&emsp; + Configure SPA redirection rules (rewrites) to prevent 404 errors on sub-routes | 08/07/2026 | 08/07/2026 | [AWS Amplify Redirects Guide](https://docs.aws.amazon.com/amplify/latest/userguide/redirects.html) |
| Thu | - **Route 53 & Cross-Origin (CORS) Setup:** <br>&emsp; + Map the custom domain name using AWS Route 53 hosted zones <br>&emsp; + Update backend CORS configuration to support safe request handling across `localhost`, Amplify preview domains, and the final custom domain | 09/07/2026 | 09/07/2026 | AWS Route 53 / API Gateway |
| Fri | - **Documentation Finalization & E2E Validation:** <br>&emsp; + Conduct end-to-end smoke testing across all major application flows <br>&emsp; + Complete and compile the project proposal, comprehensive testing suite logs, and the final workshop report | 10/07/2026 | 10/07/2026 | Markdown / Jira |

### Week 12 Key Results:

* Successfully launched and hosted the live frontend production application utilizing AWS Amplify Hosting.
* Resolved SPA routing issues by implementing proper single-page application (SPA) rewrite rules to support clean React Router paths.
* Configured functional CORS support covering local development, staging environments, and active cross-account production domain endpoints.
* Conducted thorough regression and integration testing on all primary features to guarantee stability under the new AWS architecture.
* Finalized and thoroughly documented all project deliverables, including structural architecture blueprints, technical proposals, and workshop reports.