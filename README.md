# 💳 Real-Time Banking Data Pipeline
End-to-End Streaming • Warehouse • Orchestration • Analytics

This project is a real-time banking data engineering pipeline built using a modern data stack. It mirrors how enterprise financial systems process high-volume transactional data reliably and securely.

Unlike typical tutorial projects using clean Kaggle datasets, this pipeline handles:
✔ Real-time CDC streaming
✔ Raw JSON ingestion
✔ Data quality issues
✔ Multi-layer modeling (Bronze, Silver, Gold)
✔ SCD Type 2 dimensions
✔ Automated orchestration
✔ CI/CD deployment
✔ Live dashboards

This is designed to reflect real-world banking systems.

# 📌 Architecture Overview

<img width="2816" height="1536" alt="Gemini_Generated_Image_9mhhxf9mhhxf9mhh" src="https://github.com/user-attachments/assets/bf33e469-ca24-49cc-a86a-691aee635269" />


## 🏦 1. Data Source & OLTP Layer (PostgreSQL)

The pipeline starts with a PostgreSQL OLTP database, simulating core banking tables:

👥 customers

💼 accounts

💸 transactions

Because banking systems cannot expose APIs publicly, generator code simulates secure transactional activity.

Why SQL here?

ACID transactions

Strong consistency

Structured schema suitable for financial logic

## ⚡ 2. Real-Time Streaming with Kafka + Debezium (CDC)

To capture changes in real time, the project uses:

🟦 Kafka for distributed streaming

🟩 Debezium for Change Data Capture

Debezium listens to PostgreSQL logs and streams:

inserts

updates

deletes

Raw data is streamed out as JSON strings for downstream processing.

## 🪣 3. Object Storage (S3 / MinIO)

Kafka consumer writes the streaming data into an S3-compatible store:

Parquet files for efficient storage

Separate folders for each table

Acts as a durable landing zone

## 🔁 4. Orchestration with Apache Airflow

Airflow automates the ETL and transformation workloads:

DAG pulls raw data from S3

Loads into Snowflake Bronze layer

Triggers DBT transformations

Runs SCD2 snapshots

Fully scheduled daily/real-time runs

## ❄️ 5. Data Warehouse (Snowflake)

The warehouse follows the Medallion Architecture:

🥉 Bronze

Raw JSON in a single VARIANT column

Simplifies ingestion

🥈 Silver

Cleaned and typed tables

Deduped CDC events

🥇 Gold

Business-ready star schema

SCD2 applied to dimension tables

Fact tables prepared for analytics

## 🛠 6. DBT for Transformations & SCD Type 2

DBT handles all SQL transformations:

Staging models

Snapshot-based SCD2

Surrogate keys

Tests for quality

Environment-based deployments

📘 SCD Type 2 Logic

Tracks historical changes such as updated emails or account types:

Old record → is_current = false

New record → inserted with is_current = true

Full history preserved

## 🚀 7. CI/CD & DevOps Integration

This project includes enterprise deployment workflows:

🐳 Docker

Containers for PostgreSQL, Kafka, Debezium, Airflow, MinIO

🔐 Secrets

Managed using .env + GitHub Secrets

No credentials inside repository

🤖 GitHub Actions

CI: DBT compile, syntax checks

CD: Deploy DBT models/snapshots automatically

## 📊 8. Power BI Analytics Dashboard

Power BI connects to Snowflake using DirectQuery, enabling:

Real-time metrics

No manual refresh

Direct visibility into Gold models

Dashboard Includes:

Total customers

Account balances

Transaction trends

Top customers by activity

Fraud-like behavior patterns


# 🧠 Skills Covered
Data Engineering

Kafka streaming

Debezium CDC

Snowflake warehousing

DBT modeling

Airflow orchestration

Real-time ETL/ELT pipelines

Data Modeling

Star schema design

SCD Type 2

Fact/dimension modeling

DevOps

Docker

CI/CD with GitHub Actions

Secrets management

Programming

Python

SQL

Jinja/DBT

Business Intelligence

Power BI dashboards

DirectQuery for real-time insights

# 📞 Contact

If you want to collaborate or discuss data engineering projects, feel free to reach out:

👤 Lakshmi Prasad Bathina
🔗 LinkedIn: https://www.linkedin.com/in/lakshmi-prasad-b-91a67b198/

📧 Email: blaxmiprasad6@gmail.com
