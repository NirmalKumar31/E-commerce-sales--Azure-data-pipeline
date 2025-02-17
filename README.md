# 🚀 End-to-End Azure Data Factory & Databricks Incremental Pipeline

📅 **Date:** January, 2025  
👤 **Author:** Nirmalkumar Thirupallikrishnan Kesavan  
🛠️ **Tech Stack:** Azure Data Factory (ADF), Azure Data Lake Storage (ADLS), Azure Databricks, SQL Server, Delta Lake, PySpark, Apache Spark, Apache Hive, Azure Synapse Analytics, Power BI, Azure Monitor, Azure Key Vault, Azure DevOps, SQL, Data Analysis, ETL pipeline, SCD Type 1, STAR Schema, Data Modelling, Data Warehousing  

---

## 📌 Overview
This project showcases an end-to-end **Azure Data Factory (ADF) and Databricks incremental pipeline**, designed for efficient and scalable data processing. The pipeline leverages **star schema modeling** and **Slowly Changing Dimensions (SCD) Type 1** for data transformation and storage.

---

## 🏗️ Concepts & Rationale
### 🔹 **Azure Resource Group**
📌 **Why?** Resource grouping enables centralized management of Azure components for cost tracking and security.  
🛠️ **What I Used?** Azure Data Factory (ADF), Azure Data Lake Storage (ADLS), Azure Databricks, SQL Server & SQL Database, and Access Connector. [📊My resources](https://github.com/NirmalKumar31/E-commerce-sales--Azure-data-pipeline/blob/9f5a7b8b6f58a8881537842e5a523c80525019b9/Visualizations%20and%20project%20resource%20details/Azure%20resource%20group.png)  
⚙️ **How I Did It?** Created a resource group in **UK South**, ensuring all components exist in the same region for optimal performance.

### 🔹 **Data Ingestion & Initial Load**
📌 **Why?** Data ingestion is necessary to extract structured data and store it in a central repository.  
🛠️ **What I Used?** GitHub as a source, ADF for ETL, and SQL Database for structured storage.  
⚙️ **How I Did It?**  
- Used **ADF Copy Data activity** to fetch `Sales_Data.csv` from GitHub.  
- Stored the data in **SQL database (`Sales_Data` table)**.  
- Created a **watermark table (`last_load`)** to track incremental loads.  

**📊Pipeline Diagram till Stored Procedures**:
![Pipeline Diagram till Stored Procedures](https://github.com/NirmalKumar31/E-commerce-sales--Azure-data-pipeline/blob/a90945d1be6bc5ee8d86cca5b767a6268a30d491/Model%20diagram%20and%20outputs/incremental%20load%20pipline(till%20updating%20watermark).png)

---

### 🔹 **Incremental Pipeline in ADF**
📌 **Why?** Incremental loading reduces processing time and ensures up-to-date data.  
🛠️ **What I Used?** Lookup activities, Copy activity, and SQL Stored Procedures.  
⚙️ **How I Did It?**  
- **Lookup Activities**:  
  - `last_load` to fetch the last successful Date_ID.  
  - `current_load` to retrieve the latest Date_ID from `Sales_Data`.  
- **Copy Data**: Extracted **new records** (between `last_load` and `current_load`) to **bronze layer (Parquet format)** in ADLS.  
- **Stored Procedure**: Updated the **watermark table** after each successful execution.  

### 🔹 **Databricks Data Processing**
📌 **Why?** Databricks enables large-scale data transformation and analytics.  
🛠️ **What I Used?** Unity Metastore, External Storage, and PySpark.  
⚙️ **How I Did It?**  
- Configured **Unity Metastore** to manage catalog, schemas, and tables.  
- Created **Bronze, Silver, and Gold layers** in Databricks for structured data transformations.  
- Used **PySpark in Databricks Notebooks** to:  
  - Load **bronze data** → apply transformations → store in **silver layer**.  
  - Further refine **silver data** → create **fact & dimension tables** → store in **gold layer**.  

![📈 Transformation Results](https://github.com/NirmalKumar31/E-commerce-sales--Azure-data-pipeline/tree/2d00bf34fa6971f086dc76d5d5b41a53caab3724/Visualizations%20and%20project%20resource%20details)

### 🔹 **Star Schema & SCD Type 1**
📌 **Why?**  
- **Star schema** enables optimized querying.  
- **SCD Type 1** ensures the latest dimension values are retained.  
🛠️ **What I Used?** Databricks SQL & Delta Lake.  
⚙️ **How I Did It?**  
- Created **dimension tables** (Branch, Model, Dealer, Date) and **Fact_Sales**.  
- Used **Delta Lake for versioning** and applied **SCD Type 1 logic** for updates.  

### 🔹 **Databricks Pipeline Execution**
📌 **Why?** A structured job execution workflow ensures smooth transformation processing.  
🛠️ **What I Used?** Databricks Job Scheduler.  
⚙️ **How I Did It?**  
- Created a **Databricks Job** to execute transformation notebooks.  
- Successfully ran transformations and validated data outputs.  

**📊Databricks ETL Pipeline to create facts and dimensions using SCD TYPE-1 and STAR Schema**:
![Databricks ETL Pipeline to create facts and dimensions using SCD TYPE-1 and STAR Schema](https://github.com/NirmalKumar31/E-commerce-sales--Azure-data-pipeline/blob/5cb723871b07968749285f8ea8f7d40a227a1090/Model%20diagram%20and%20outputs/databricks%20pipeline%20model%20and%20execution.png)

---

### 🔹 **End-to-End ADF Pipeline**
📌 **Why?** Automating the entire workflow ensures consistency and reliability.  
🛠️ **What I Used?** ADF to trigger Databricks Notebooks.  
⚙️ **How I Did It?**  
- Integrated the **incremental ADF pipeline** with **Databricks Notebooks**.  
- Triggered Databricks transformations automatically after ingestion.  
- Successfully executed **full data pipeline from ingestion to star schema modeling**.  

**📊Azure Data Factory end-to-end Incremental Pipeline connected with databricks to create facts and dimensions SCD Type-1 with STAR Schema**:
![Azure Data Factory end-to-end Incremental Pipeline connected with databricks to create facts and dimensions SCD Type-1 with STAR Schema](https://github.com/NirmalKumar31/E-commerce-sales--Azure-data-pipeline/blob/5cb723871b07968749285f8ea8f7d40a227a1090/Model%20diagram%20and%20outputs/end-to-end%20pipeline%20(ADF)%20Model.png)

## 📊 Insights & Visualizations
📌 **Why?** Data insights enable better decision-making.  
🛠️ **What I Used?** Databricks Dashboards & PySpark visualizations.  
⚙️ **How I Did It?**  
- **Silver Layer Analysis**:  
  - Extracted `model_category` from Model_ID.  
  - Aggregated **monthly revenue & units sold per year**.  
  - Performed **AD-HOC analysis - revenue per unit**.  
- **Gold Layer**:  
  - Created **final fact and dimension tables**.  
  - Built **branch-wise sales revenue analysis**.  
  - Visualized **trends using Databricks charts**.  

![📊 Visualization Results](https://github.com/NirmalKumar31/E-commerce-sales--Azure-data-pipeline/tree/5cb723871b07968749285f8ea8f7d40a227a1090/Visualizations%20and%20project%20resource%20details)

## 🎯 Conclusion
✅ **Efficient incremental data loading using ADF.**  
✅ **Scalable data processing with Databricks.**  
✅ **Optimized querying with Star Schema & SCD Type 1.**  
✅ **Comprehensive insights via Databricks visualizations.**  

The use of **parameterized pipelines**, **Delta Lake**, and **Unity Metastore** ensures **scalability and performance**, making this a robust data pipeline solution.  

---

## ⭐ Contribute & Connect
💡 If you find this useful, star ⭐ this repo!  

🔗 **LinkedIn**: [https://www.linkedin.com/in/nirmalkumartk/](https://www.linkedin.com/in/nirmalkumartk/)  
🔗 **GitHub**: [https://github.com/NirmalKumar31](https://github.com/NirmalKumar31)  

