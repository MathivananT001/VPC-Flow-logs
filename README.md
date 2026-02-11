# VPC Flow Logs Monitoring with CloudWatch, S3, and Athena

## 📌 Overview
This project demonstrates how to set up **Amazon VPC Flow Logs** for monitoring and analyzing network traffic.  
It integrates with **CloudWatch** for real-time observability and **S3 + Athena** for scalable log storage and query-driven analytics.

---

## 🚀 Features
- **Flow Logs with S3 + Athena**
  - Directly query flow logs without building heavy ETL pipelines.
  - Eliminates infrastructure setup, scaling, and ongoing management.
  - Requires schema definition in Athena.
  - **Use case:** Deep analysis, reporting, and trend insights over time.

- **Flow Logs with CloudWatch**
  - Real-time log analysis for observability and troubleshooting.
  - **Use case:** Live monitoring and quick issue resolution.

---

## 🛠 Setup Instructions

### Flow Logs with S3
1. Create an **S3 bucket** in the same region as your VPC.
2. Create **Flow Logs** from the VPC with destination set to the S3 bucket.

### Using Athena with Logs Stored in S3
1. Create an **S3 bucket** to store Athena query results.
2. Map the S3 bucket in Athena’s query location.
3. Create a **structured SQL table** from logs stored in S3.
4. Partition the table by time (day/hour recommended for large datasets).
5. Run queries to analyze logs (e.g., accepted vs. rejected actions).

---

### Flow Logs with CloudWatch
1. Create an **IAM role** with:
   - Custom trust policy for `vpc-flow-logs.amazonaws.com`
   - `CloudWatchFullAccess` permissions
   ```json
   {
     "Version": "2012-10-17",
     "Statement": [
       {
         "Sid": "Statement1",
         "Effect": "Allow",
         "Principal": {
           "service": "vpc-flow-logs.amazonaws.com"
         },
         "Action": "sts:AssumeRole"
       }
     ]
   }
