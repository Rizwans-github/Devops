# 📘 1. Introduction to Azure Data Factory

**Overview:**  
Azure Data Factory (ADF) is Microsoft's cloud tool that helps you move and transform data from different places so it's clean and ready for use (like reporting or analysis).

### 🔹 Key Points:

- **What is ADF?**  
  Think of it as a delivery service for your data — it picks up data from one place, repackages it, and drops it off at another.

- **ETL Pipeline Concept:**  
  - **Extract:** Get raw data from different sources.  
  - **Transform:** Clean it up or reformat it.  
  - **Load:** Save it somewhere useful like a database or storage.

- **Example Scenario:**  
  ADF can gather gaming logs from cloud storage and customer info from company servers, combine and clean them, then send the results to Power BI for visualization.

- **Why Use ADF?**  
  It’s easy to set up, works with both cloud and on-prem data, and you don’t need to manage any servers.

---

## 📗 2. Top Level Concepts in Azure Data Factory

**Overview:**  
This video explains the basic tools inside ADF that help build workflows to move and shape data.

### 🔹 Key Components:

- **Pipelines:**  
  Like a recipe – it tells ADF what tasks to do and in what order.

- **Activities:**  
  The steps inside the recipe. You might have one to copy data, and another to clean it.

- **Datasets:**  
  These tell ADF what type of data you're working with — for example, a spreadsheet or a database table.

- **Linked Services:**  
  Like saved login info. These are your connections to other tools or data sources.

- **Triggers:**  
  They decide when the workflow runs. You can schedule it daily or trigger it when something changes.

- **Integration Runtime (IR):**  
  The behind-the-scenes engine that runs your data tasks. Three types:
  - **Azure IR:** Fully managed by Microsoft, used in the cloud.  
  - **Self-hosted IR:** Installed on your machines, for accessing local data.  
  - **Azure-SSIS IR:** For using SSIS packages inside ADF.

