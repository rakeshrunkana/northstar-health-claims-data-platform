# Northstar Health Services — Healthcare Claims Data Platform
Enterprise healthcare claims data platform designed to ingest, transform, validate, model and visualize daily claims data using Microsoft Fabric, Azure SQL, Azure Blob Storage and Power BI.


# Northstar Health Services — Healthcare Claims Data Platform

> Enterprise healthcare claims data platform designed to ingest, transform, validate, model and visualize daily claims data using Microsoft Fabric, Azure SQL, Azure Blob Storage and Power BI.

---

## 📌 Project Overview

Northstar Health Services requires a reliable analytical data platform to process daily healthcare claims data originating from an operational claims system.

The platform is designed to:

- Ingest daily claims data
- Preserve source-aligned records
- Apply data cleansing and standardization
- Perform incremental processing
- Create curated analytical datasets
- Build a dimensional data warehouse
- Provide governed analytics through a semantic model
- Deliver business insights through Power BI

---

## 🏗️ Solution Architecture

```text
┌──────────────────────────────┐
│ Adroit Operational System    │
│ Daily Claims Data            │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│ Azure Blob Storage            │
│ Landing Zone                  │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│ Microsoft Fabric Pipeline    │
│ Orchestration                │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│ Azure SQL Staging             │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│ Bronze Layer                  │
│ Source-Aligned Data           │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│ Silver Layer                  │
│ Cleaned & Conformed Data      │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│ Gold Layer                    │
│ Fact & Dimension Model        │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│ Semantic Model                │
│ Governed Business Logic       │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│ Power BI Analytics            │
└──────────────────────────────┘
🛠️ Technology Stack
Technology	Purpose
Microsoft Fabric	Data engineering and orchestration
Azure Blob Storage	Daily file landing
Azure SQL	Relational staging
Fabric Lakehouse	Layered data engineering
Fabric Warehouse	Curated analytical serving
Fabric Pipelines	Workflow orchestration
Notebooks	Data transformation
Semantic Model	Governed analytical layer
Power BI	Reporting and visualization
Power Automate	Operational notifications
🥉🥈🥇 Medallion Architecture
Bronze Layer

The Bronze layer preserves source-aligned data with minimal transformation.

Purpose:

Preserve source data
Maintain traceability
Support reprocessing
Provide an auditable engineering layer
Silver Layer

The Silver layer contains cleaned, standardized and conformed data.

Typical processing includes:

Data type standardization
Date conversion
Null handling
Deduplication
Business rule application
Data quality validation
Gold Layer

The Gold layer contains curated, business-ready analytical data.

Typical outputs include:

Fact tables
Dimension tables
Business measures
Analytical data marts
🔄 Incremental Processing

Claims are processed at the claim-line level using the composite business key:

Claim_ID + Line_Number

Conceptually:

New Business Key
        │
        ▼
      INSERT

Existing Key + Changed Data
        │
        ▼
      UPDATE

Existing Key + No Change
        │
        ▼
   NO ACTION

This approach helps support:

Duplicate prevention
Incremental processing
Claim-line traceability
Repeatable pipeline execution
⭐ Dimensional Model

The Gold layer follows a star-schema design.

                    ┌──────────────┐
                    │   Dim_Date   │
                    └──────┬───────┘
                           │
                           │
┌──────────────┐     ┌─────▼───────┐     ┌────────────────┐
│   Dim_Payer  │────▶│ Fact_Claims │◀────│  Dim_Provider  │
└──────────────┘     └─────┬───────┘     └────────────────┘
                           │
                           │
                    ┌──────▼───────┐
                    │  Dim_Member  │
                    └──────────────┘
Fact Table

Stores measurable claim-line activity.

Dimension Tables

Provide descriptive context for analytical filtering and grouping.

🔁 End-to-End Data Flow
Operational Source
        ↓
Daily Claims Extract
        ↓
Azure Blob Storage
        ↓
Fabric Ingestion Pipeline
        ↓
Azure SQL Staging
        ↓
Bronze Layer
        ↓
Silver Layer
        ↓
Gold Warehouse
        ↓
Star Schema
        ↓
Semantic Model
        ↓
Power BI Reports
        ↓
Business Insights
📊 Analytics

The analytical layer supports reporting across areas such as:

Executive claims performance
Payer analysis
Provider performance
Financial metrics
Claim denials
Operational monitoring
🧪 Data Quality

The platform applies data-quality controls across the processing lifecycle.

Key Validation Areas
Completeness
Validity
Accuracy
Consistency
Uniqueness
Timeliness
Technical Validation
Source-to-target reconciliation
Record-count validation
Business-key validation
Duplicate detection
Date validation
Numeric validation
Referential integrity
⚙️ Pipeline Orchestration

The processing flow is coordinated through dependency-driven orchestration.

┌───────────────────────────────┐
│ Master Claims Automation      │
└───────────────┬───────────────┘
                │
                ▼
┌───────────────────────────────┐
│ Blob → SQL Staging             │
└───────────────┬───────────────┘
                │
                ▼
┌───────────────────────────────┐
│ SQL → Bronze                   │
└───────────────┬───────────────┘
                │
                ▼
┌───────────────────────────────┐
│ Bronze → Silver                │
└───────────────┬───────────────┘
                │
                ▼
┌───────────────────────────────┐
│ Silver → Gold                 │
└───────────────────────────────┘

Downstream processing is dependent on successful completion of upstream stages.

📚 Documentation
Document	Description
Solution Architecture Document	High-level solution architecture
Technical Design Document	Detailed implementation design
Theoretical Technical Reference	Conceptual enterprise data engineering design
Data Dictionary	Definitions of technical and business fields
Source-to-Target Mapping	Field-level data movement and transformations
Test Strategy	Technical testing approach
Validation Evidence	Pipeline and data validation results
Deployment Guide	Release and deployment process
Operations Runbook	Production support procedures
🗂️ Repository Structure
northstar-health-claims-data-platform/
│
├── 01-architecture/
│   ├── solution-architecture/
│   ├── technical-design/
│   ├── theoretical-reference/
│   └── diagrams/
│
├── 02-data-engineering/
│   ├── data-dictionary/
│   ├── source-to-target-mapping/
│   └── data-quality/
│
├── 03-sql/
│   ├── staging/
│   ├── bronze/
│   ├── silver/
│   ├── gold/
│   ├── stored-procedures/
│   └── dimensional-model/
│
├── 04-microsoft-fabric/
│   ├── pipelines/
│   ├── notebooks/
│   └── workspace/
│
├── 05-power-bi/
│   ├── semantic-model/
│   ├── measures/
│   └── report-documentation/
│
├── 06-testing/
│   ├── test-strategy/
│   ├── validation/
│   └── test-results/
│
├── 07-deployment/
│   ├── deployment-guide/
│   └── operations-runbook/
│
├── 08-evidence/
│   ├── architecture/
│   ├── pipelines/
│   ├── power-bi/
│   └── monitoring/
│
└── docs/
🎯 Key Technical Decisions
Layered Data Architecture

Separates raw preservation, conformed transformation and analytical serving.

Composite Business Key

Uses:

Claim_ID + Line_Number

to identify logical claim-line records.

Star Schema

Provides efficient analytical querying and reusable dimensional context.

Semantic Layer

Centralizes business measures and analytical logic.

Dependency-Driven Orchestration

Ensures downstream processing occurs only after successful upstream processing.

🚀 Future Enhancements

Potential future enhancements include:

Metadata-driven ingestion
Dynamic file discovery
Change Data Capture
Data catalog integration
Automated schema drift detection
CI/CD deployment automation
Advanced data lineage
Real-time claims processing
Machine learning for denial prediction
Advanced anomaly detection
⚠️ Security Notice

This repository is designed for demonstration and portfolio purposes.

Do not commit:

Real healthcare data
Personally identifiable information
Credentials
Secrets
Connection strings
Access tokens
Private client information

All sensitive data should be anonymized or replaced with synthetic data.

👤 Project Focus

This project demonstrates enterprise data engineering capabilities across:

Microsoft Fabric
Azure Data Engineering
SQL
Data Warehousing
Medallion Architecture
Dimensional Modeling
Power BI
Data Quality
Pipeline Orchestration
Technical Documentation
Production Operations
📌 Status

Project Status: Architecture and core data platform implementation completed.

Current Focus: Enterprise documentation, GitHub portfolio organization and deployment operationalization.
