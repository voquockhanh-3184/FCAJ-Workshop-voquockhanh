---
title : "Adjusting Express Backend to Run on Lambda"
date : 2024-01-01 
weight : 5
chapter : false
pre : " <b> 5.5.5. </b> "
---

An Express backend typically runs on a traditional server model:

Express app → server.listen(PORT)

However, AWS Lambda does not run applications by opening a port like a server. Instead, it invokes a **handler function** when a request is sent from API Gateway. Therefore, the backend should be decoupled into two components:

- Express app
  -> contains middleware, routes, business logic

- Lambda handler
  -> receives events from Lambda/API Gateway and forwards requests into the Express app

**Processing Idea:**

API Gateway event  → Lambda handler  → Express app → Middleware verify Cognito JWT
→ Connect MongoDB Atlas → Xử lý API  → Trả response

