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

## 🏗️ Architecture & Data Pipeline

<img width="1692" height="603" alt="Data pipeline" src="https://github.com/user-attachments/assets/020a2fbe-5e34-4d7e-a6ce-05140e2a9cb3" />


The platform follows a cloud ELT architecture — data is loaded first, then transformed inside the warehouse, keeping storage, transformation, and consumption cleanly separated.


| Layer | Technology | Responsibility |
|---|---|---|
| Source | Olist datasets | Raw e-commerce and marketing data |
| Storage | Amazon S3 | Cloud-based raw data storage |
| Warehouse | Snowflake | Central analytical data warehouse |
| Transformation | dbt | SQL transformation and data modelling |
| Analytics | Power BI | Business intelligence and reporting |

### dbt Transformation Layers

- **Staging** — 1:1 with source tables. Standardises column names, casts data types, cleans source fields. No business logic.
- **Intermediate** — reusable business logic and joins (e.g. RFM scoring, delivery-delay flags), built once so it isn't duplicated across marts.
- **Marts** — the final analytical interface, modelled around business questions rather than the original CSV structure. This is the only layer Power BI queries.

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

## 📊 Analytics Layer — Power BI

The curated dbt marts are consumed by Power BI to provide business-facing analytics.

The project contains **four Power BI reports**, covering different analytical perspectives of the Olist marketplace.

📎 **[View Full Power BI Report (PDF)](powerbi/Olist_PowerBI_Reports.pdf)**

| Report | Focus |
|---|---|
| 📈 **01 — Sales & Commercial Performance** | Revenue drivers, top categories, sellers and regions |
| 👥 **02 — Customer Intelligence** | Customer behaviour, value and RFM segmentation |
| 🛒 **03 — Marketing & Acquisition** | Channel performance and customer acquisition value |
| 🚚 **04 — Customer Experience** | Delivery performance, reviews, and revenue impact |

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


## 🛠️ Technology Stack

| Technology | Role |
|---|---|
| **Amazon S3** | Raw cloud data storage |
| **Snowflake** | Cloud data warehouse |
| **dbt** | Data transformation and modelling |
| **SQL** | Transformation and analytical logic |
| **Power BI** | Business intelligence and reporting |

---

## 🔮 Future Improvements

- Automated data ingestion and pipeline orchestration
- Incremental dbt models
- CI/CD for dbt
- Automated data quality monitoring and alerting
- Infrastructure as Code
- Automated Power BI dataset refreshes

---

## 👤 About

Built to demonstrate practical experience with modern cloud data engineering and analytics workflows: cloud storage, data warehousing, ELT architecture, dbt modelling, business intelligence, and stakeholder-ready reporting.

**Core architecture:** Amazon S3 → Snowflake → dbt → Power BI
