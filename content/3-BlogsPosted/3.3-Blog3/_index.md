---
title: "Blog 3"
date: 2026-07-05
weight: 1
chapter: false
pre: "<b> 3.3. </b> "
---
# Optimizing EC2 Costs by Analyzing Capacity Reservations with Amazon Athena

Optimizing Amazon EC2 On-Demand Capacity Reservations (ODCR) helps businesses identify and minimize underutilized reservations, thereby avoiding wasted costs when operating large-scale AWS infrastructure. The solution combines EC2 Capacity Manager, Amazon S3, and Amazon Athena to store, query, and analyze long-term historical data, helping to track capacity usage trends and support optimal resource management decisions based on real-world data rather than limited information on the AWS Console.

Key points to understand:

* The solution aims to analyze and optimize Amazon EC2 On-Demand Capacity Reservations (ODCR) costs based on long-term historical data, helping to identify inefficient reservations.
* On-Demand Capacity Reservations (ODCR) are still charged even when no EC2 instances are in use, leading to waste if reservations are left empty or underutilized.
* The AWS Management Console only stores and displays Capacity Reservation usage data for 90 days, making it difficult to analyze trends or evaluate long-term usage efficiency.
* EC2 Capacity Manager allows exporting hourly capacity usage data to Amazon S3 in Parquet format, suitable for large-scale data storage and analysis.
* Amazon Athena can directly query data on S3 using SQL, eliminating the need to build an ETL process or deploy a separate data warehouse.
* This solution uses Athena's Partition Projection to automatically identify new partitions, ensuring data is continuously updated without the need for manual metadata updates.
* This solution is suitable for businesses managing multiple AWS accounts and regions, helping to track and optimize EC2 costs based on historical data rather than just end-of-month invoices.
* The system can be expanded by integrating with Amazon EventBridge Scheduler for automatic periodic data export and refresh, or by combining with Amazon QuickSight to build intuitive dashboards for monitoring and analyzing costs.

The solution helps businesses proactively identify underutilized Capacity Reservations, allowing them to adjust or cancel unnecessary reservations to reduce costs. Long-term data storage on Amazon S3 and analysis using Amazon Athena also provides a foundation for large-scale AWS cost management reports and dashboards.

![Picture blog 3](/images/blog3.png)

[Link blog](https://www.facebook.com/groups/awsstudygroupfcj/permalink/2204187187012908/#)

![Instruction](/images/instructionblog3.png)