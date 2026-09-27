# E-Commerce Analytics Platform

> **End-to-end cloud data engineering and analytics platform transforming raw e-commerce and marketing data into business-ready Snowflake data marts and Power BI dashboards.**

**Amazon S3 · Snowflake · dbt · SQL · Power BI**

[Architecture](#-architecture) ·
[Data Pipeline](#-data-pipeline) ·
[Data Model](#-data-modelling) ·
[Dashboards](#-analytics-layer--power-bi) ·
[Business Value](#-business-value) ·
[Technology Stack](#️-technology-stack)

---

## 📌 Project Overview

E-commerce businesses generate data across multiple domains — orders, customers, products, sellers, payments, logistics, and marketing.

When this data exists as separate raw files, it becomes difficult for business teams to answer important questions consistently.

This project addresses that problem by building a **cloud-based ELT pipeline** that takes raw Olist e-commerce and marketing data, stores it in Amazon S3, loads it into Snowflake, transforms it using dbt, and exposes curated analytical data through Power BI.


## 🎯 Business Problem

E-commerce businesses collect data from multiple operational areas such as orders, customers, products, sellers, logistics, payments, and marketing.

When this information remains in disconnected source files, business teams may struggle to answer questions such as:

How are sales and order volumes changing over time?
Which products and categories generate the most revenue?
Which sellers contribute most to marketplace activity?
Where are customers geographically concentrated?
How does delivery performance vary?
What patterns can be identified across e-commerce and marketing data?

The goal of this project is to transform these fragmented datasets into a centralised, structured analytical platform that supports business reporting and decision-making.

## Architecture

<img width="1692" height="603" alt="Data pipeline" src="https://github.com/user-attachments/assets/020a2fbe-5e34-4d7e-a6ce-05140e2a9cb3" />


**Flow in one sentence:** raw CSVs land in S3 → Snowflake ingests them via an external stage → dbt transforms them through three layers (staging → intermediate → marts) → Power BI connects to the marts and serves four executive-facing reports.

### Architecture at a Glance

| Layer          | Technology     | Responsibility                        |
| -------------- | -------------- | ------------------------------------- |
| Source         | Olist datasets | Raw e-commerce and marketing data     |
| Storage        | Amazon S3      | Cloud-based raw data storage          |
| Warehouse      | Snowflake      | Central analytical data warehouse     |
| Transformation | dbt            | SQL transformation and data modelling |
| Analytics      | Power BI       | Business intelligence and reporting   |

---

# 🔄 Data Pipeline

The pipeline follows a **cloud ELT architecture**, separating data storage, transformation, and consumption.

## 1. Raw Data — Amazon S3

The project begins with **11 CSV files** containing Olist e-commerce and marketing data.

The source files are stored in Amazon S3, providing a central cloud-based landing layer for the raw data.

The raw data is preserved before analytical transformations are applied.

```text
Olist CSV Files
      │
      ▼
Amazon S3
      │
      ▼
Raw Data
```

---

## 2. Data Warehouse — Snowflake

Snowflake is used as the central analytical data warehouse.

The data stored in Amazon S3 is made available to Snowflake and forms the foundation for downstream transformations.

```text
Amazon S3
    │
    ▼
Snowflake
    │
    ▼
Raw Tables
```

This creates a clear separation between the raw storage layer and the analytical warehouse.

---

## 3. Transformation — dbt

dbt is responsible for transforming raw Snowflake data into structured, business-ready analytical models.

The dbt project follows a three-layer transformation architecture:

```text
Raw
 │
 ▼
Staging
 │
 ▼
Intermediate
 │
 ▼
Marts
```

---

## 🧹 Staging Layer

The staging layer provides source-level preparation and standardisation.

Typical responsibilities include:

* Standardising column names
* Casting data types
* Cleaning source fields
* Creating consistent source-level models
* Preparing raw data for downstream transformations

```text
Raw Source Tables
       │
       ▼
Staging Models
```

---

## 🔧 Intermediate Layer

The intermediate layer contains reusable transformation and business logic.

This layer combines and enriches staging models before they are exposed to business users.

```text
Staging Models
       │
       ▼
Intermediate Models
       │
       ▼
Business Logic
```

The purpose of this layer is to avoid duplicating complex transformation logic across multiple downstream models.

---

## 📊 Marts Layer

The marts layer provides the final analytical interface for reporting.

These models are designed around business questions rather than the structure of the original CSV files.

```text
Intermediate Models
       │
       ▼
Business Marts
       │
       ▼
Power BI
```

The marts are the primary data source for the Power BI reporting layer.

---

# 🧱 Data Modelling

The project separates raw source structures from the analytical models consumed by Power BI.

```text
                    RAW DATA
                       │
                       ▼
                   STAGING
                       │
                       ▼
                 INTERMEDIATE
                       │
                       ▼
                     MARTS
                       │
                       ▼
                   POWER BI
```

![Data Model](docs/data_model.png)


# 📊 Analytics Layer — Power BI

The curated dbt marts are consumed by Power BI to provide business-facing analytics.

The project contains **four Power BI reports**, covering different analytical perspectives of the Olist marketplace.

---

## 📈 Report 01 — Executive Analytics

Provides a high-level view of marketplace performance and key business metrics.

![Executive Dashboard](docs/dashboards/executive.png)

---

## 🛒 Report 02 — Sales & Product Analytics

Provides analysis of sales activity, products, categories, and revenue performance.

![Sales Dashboard](docs/dashboards/sales.png)

---

## 👥 Report 03 — Customer Analytics

Provides insight into customer behaviour, distribution, and geographic patterns.

![Customer Dashboard](docs/dashboards/customers.png)

---

## 🚚 Report 04 — Operations & Marketing Analytics

Brings together operational and marketing perspectives to support analysis of marketplace performance.

![Operations Dashboard](docs/dashboards/operations.png)

# 🎤 Stakeholder Presentation

To close the loop from data platform to business decision-making, the project includes an executive-facing summary deck — the kind of artifact a data team would actually hand to leadership after a project like this.

📎 **[Download the Executive Presentation (PDF/PPTX)](presentation/Olist_Executive_Review.pptx)**

# 📈 Business Value

The platform transforms disconnected source files into a reusable analytical environment.

```text
Disconnected Source Files
          │
          ▼
Centralised Cloud Storage
          │
          ▼
Structured Data Warehouse
          │
          ▼
Reusable Transformation Models
          │
          ▼
Business-ready Data Marts
          │
          ▼
Interactive BI Reports
          │
          ▼
Business Insights
```

The result is a clear path from:

> **Raw Data → Transformation → Analytics → Business Insights**

---

# 🧪 Data Quality & Reliability

The transformation architecture provides a dedicated location for validating data before it reaches the reporting layer.

Potential data quality checks include:

* Primary key uniqueness
* Required fields
* Referential integrity
* Accepted values
* Relationships between fact and dimension models
* Null validation
* Source-to-model consistency

Data quality checks implemented within the project are documented in the dbt project.


# 🔮 Future Improvements

Potential extensions to the platform include:

* Automated data ingestion
* Pipeline orchestration
* Incremental dbt models
* CI/CD for dbt
* Automated data quality monitoring
* Pipeline observability and alerting
* Infrastructure as Code
* Automated Power BI dataset refreshes

These improvements would move the project further towards a production-oriented data platform.
