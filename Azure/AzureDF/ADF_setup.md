# Azure Data Factory – Detailed Setup & Demo
##  1. Provisioning the Data Factory
- Open **Azure Portal** → Search “Data Factory”.
- Click **Create**, input:
  - Name
  - Resource Group
  - Region
- Use **V2 version**
- Wait for deployment → Launch **Author & Monitor**

##  2. Authoring Pipelines in ADF Studio
- Navigate to **Author** tab → Right-click & add **New Pipeline**
- Drag in activities (e.g., `Copy Data`, `Wait`, etc.)
- Create **linked services** for source/destination:
  - _Example_: Azure Blob → Azure SQL DB

##  3. Dataset Configuration
- Define **datasets** tied to each linked service:
  - **For Blob**: specify folder path, file format
  - **For SQL DB**: define query/table

## 4. Pipeline Execution & Triggering
- Use **Debug** to test the pipeline without publishing
- **Publish** the pipeline when ready
- Configure **Trigger**:
  - Schedule-based
  - Tumbling Window
  - Event-based

##  5. Monitoring Pipeline Runs
- Switch to **Monitor** tab:
  - Check activity runs
  - View success/failure logs
  - Resubmit failed runs or modify properties

