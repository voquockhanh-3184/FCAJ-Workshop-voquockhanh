---
title: "Worklog Week 5"
date: 2026-05-22
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

## FCAJ WORKLOG - WEEK 05: EVENT-DRIVEN ARCHITECTURE & ORCHESTRATION

**Performed by:** Vo Quoc Khanh  
**Group:** KQPSV Group  

---

### Week 5 Objectives:

* Learn about Event-Driven Architecture and how to build asynchronous processing systems on AWS.
* Upgrade the system from a synchronous processing model to an asynchronous model in order to:
  * Increase system scalability.
  * Reduce Client wait time.
  * Process background tasks more efficiently.
* Learn how to use AWS services to build an event processing flow:
  * Amazon SNS.
  * Amazon SQS.
  * AWS Lambda.
  * AWS Step Functions.
* Build complex business orchestration processes using Workflow and State Machine.

---

### Tasks to be implemented during this week:

| Day | Tasks | Start Date | Completion Date | Reference (Cloud Journey) |
| :--- | :--- | :--- | :--- | :--- |
| **Day 2** | - Learn about Event-Driven Architecture:<br>&emsp;+ Event and Event Producer/Consumer concepts<br>&emsp;+ Asynchronous processing model<br>&emsp;+ Applying SNS and SQS in a Cloud system | 18/05/2026 | 18/05/2026 | [Event-Driven Architecture](https://000054.awsstudygroup.com) |
| **Day 3** | - **Hands-on with Amazon SNS and SQS:**<br>&emsp;+ Create the SNS Topic `MyTopic`<br>&emsp;+ Create the SQS Queues: `InventoryQueue`, `AnalyticsQueue`<br>&emsp;+ Configure the Fan-out Publisher/Subscriber model<br>&emsp;+ Verify message replication across the Queues | 19/05/2026 | 19/05/2026 | [Messaging Systems with SQS and SNS](https://000077.awsstudygroup.com) |
| **Day 4** | - **Hands-on event processing with Lambda:**<br>&emsp;+ Create the Lambda Function `ProcessOrderFunction` using the Python Runtime<br>&emsp;+ Configure the SQS Queue as an Event Source Trigger<br>&emsp;+ Grant the `AWSLambdaSQSQueueExecutionRole` permission<br>&emsp;+ Check the processing logs on CloudWatch | 20/05/2026 | 20/05/2026 | [Event Processing with SQS and SNS](https://000083.awsstudygroup.com/) |
| **Day 5** | - **Learn about AWS Step Functions:**<br>&emsp;+ State Machine concepts<br>&emsp;+ Workflow Orchestration<br>&emsp;+ Task State, Choice State, Pass State, Fail State<br>&emsp;+ Build an order processing workflow | 21/05/2026 | 21/05/2026 | [Workflow Orchestration with AWS Step Functions](https://000047.awsstudygroup.com) |
| **Day 6** | - **Hands-on Workflow orchestration:**<br>&emsp;+ Create the State Machine `OrderOrchestrator`<br>&emsp;+ Connect the `CheckStock` Lambda<br>&emsp;+ Configure branching conditions using JSONata<br>&emsp;+ Execute and verify the Workflow result | 22/05/2026 | 22/05/2026 | [Workflow Orchestration with AWS Step Functions](https://000047.awsstudygroup.com) |

---

### Week 5 Achievements:

* Understood Event-Driven Architecture and how components in the system communicate through Events.

* Successfully built an asynchronous processing model using Amazon SNS and Amazon SQS:
  * Created the SNS Topic:
    * `MyTopic`
  * Created the SQS Queues:
    * `InventoryQueue`
    * `AnalyticsQueue`
  * Configured the Fan-out model:
    * A message is published to the SNS Topic.
    * The message is replicated and delivered simultaneously to multiple SQS Queues.

* Successfully built an event processing system with AWS Lambda:
  * Created the Lambda Function:
    * `ProcessOrderFunction`
  * Configured SQS as the Event Source Trigger.
  * Granted the permission:
    * `AWSLambdaSQSQueueExecutionRole`
  * Lambda automatically receives messages from the Queue, parses the JSON data,