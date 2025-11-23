# 📊 CarePlus Ticket Analytics Pipeline  
End-to-End Data Engineering Project using AWS (S3, Lambda, Glue, Athena, Redshift) + Power BI

---

## 📘 Project Overview

The **CarePlus Ticket Analytics Pipeline** is a complete end-to-end data engineering and analytics solution built using AWS cloud services.

It ingests **support tickets (CSV)** and **application logs (LOG)** into an S3 Data Lake, processes them using **AWS Lambda & AWS Glue**, loads the clean data into **Amazon Redshift**, and visualizes insights using **Power BI**.

This project demonstrates:

- Amazon **S3 (Data Lake)**
- **AWS Lambda** — event-driven transformations
- **AWS Glue** — ETL and schema management  
- **Amazon Athena** — ad-hoc querying  
- **Amazon Redshift** — data warehouse  
- **Power BI** — dashboard and analytics  

---

## 🏗️ Tech Architecture

![Architecture](sandbox:/mnt/data/730ffab8-a720-4e27-aad0-8e6d8fb7b2de.png)

### **Architecture Flow**
1. Extract data from **MySQL (tickets DB)**
2. Store raw data in **S3 Data Lake**
3. Lambda triggers on new files → processes data  
4. Glue crawlers & ETL jobs normalize data  
5. Load into **Redshift Warehouse**
6. Power BI connects to Redshift for reporting  

---

## 📁 S3 Data Lake Folder Structure
s3://careplus-data-lake/
├── support_tickets/
│ ├── raw/
│ └── processed/
└── support_logs/
├── raw/
└── processed/

---

## ⚙️ ETL Pipeline

### **1️⃣ Ingestion (S3)**
- CSV files → `support_tickets/raw/`
- LOG files → `support_logs/raw/`
- S3 event triggers Lambda function

### **2️⃣ Transformation (Lambda)**
- Cleans CSV & LOG data  
- Removes duplicates  
- Parses log files  
- Writes clean output to `/processed/`

### **3️⃣ AWS Glue**
- Glue Crawler detects schema  
- Glue ETL job further transforms and prepares data  
- Converts into analytical format for Redshift  

### **4️⃣ Load to Redshift**

Example Redshift COPY command:

```sql
COPY tickets
FROM 's3://careplus-data-lake/support_tickets/processed/'
IAM_ROLE '<REDSHIFT_ROLE>'
FORMAT AS PARQUET
REGION 'us-east-1';

🗄️ Redshift Data Warehouse

Final analytical tables include:

tickets

ticket_logs

interactions

agent_performance

These tables enable:

Resolution time analytics

Agent ticket load

Escalation tracking

Issue category analysis

📊 Power BI Dashboard

Dashboard Highlights

Total Tickets: 48

Resolved: 39

Open: 8

Escalated: 1

Avg Interactions: 4.38

Avg Resolution Time: 1098 minutes

Tickets by Agent

Tickets by Channel

Resolution Time by Category & Priority

Detailed ticket table

🎯 What I Learned
AWS

S3 Data Lake design

Lambda event automation

Glue ETL development

Athena for data validation

Redshift warehousing

Data Engineering

Raw vs processed zones

Handling structured & unstructured data

ETL pattern implementation

Data modelling for BI

Visualization

Connecting Power BI with Redshift

Building KPIs, charts, and insights

🚀 How to Run the Pipeline

Upload raw CSV/LOG files to S3

Lambda auto-processes them

Glue crawler updates schema

Glue ETL job prepares final tables

COPY command loads into Redshift

Power BI refreshes dashboard

✔️ Conclusion

This project showcases a fully functional cloud-native data analytics pipeline using AWS services and Power BI.

It covers data ingestion → processing → warehousing → visualization, demonstrating strong data engineering and analytics capabilities.
