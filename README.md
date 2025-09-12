# Azure Data Factory Transformation Project 🚀

## 📌 Business Use Case
- Raw data is stored in **Azure Storage Account** from external sources.
- Requirement: Transform **multiple rows → single row per customer** using **ADF Pivot Transformation**.
- Store the transformed data into a **separate target storage** for reporting & analytics.

---

## ⚙️ Architecture

1. **Source** → Raw data (CSV/TXT) stored in **Azure Blob / Data Lake**.
2. **Data Flow in ADF**
   - **Pivot Transformation** → Reshape rows into columns per `CustomerID`.
   - **Derived Column** (optional) → Calculate totals or new metrics.
3. **Sink** → Final transformed dataset stored in **output container**.

---

## 📂 Input File

`sales_raw_data.txt`

| CustomerID | Product   | Month | Quantity | Amount |
|------------|-----------|-------|----------|--------|
| 101        | Pen       | Jan   | 10       | 100    |
| 101        | Notebook  | Jan   | 5        | 250    |
| 101        | Pencil    | Feb   | 20       | 200    |
| 101        | Pen       | Feb   | 15       | 150    |
| 102        | Pen       | Jan   | 8        | 80     |
| 102        | Notebook  | Jan   | 12       | 600    |
| 102        | Pencil    | Feb   | 10       | 100    |
| 102        | Pen       | Mar   | 20       | 200    |
| 103        | Notebook  | Jan   | 7        | 350    |
| 103        | Pencil    | Feb   | 15       | 150    |
| 103        | Pen       | Feb   | 12       | 120    |
| 103        | Notebook  | Mar   | 9        | 450    |
| 104        | Pen       | Jan   | 25       | 250    |
| 104        | Pencil    | Jan   | 30       | 300    |
| 104        | Notebook  | Feb   | 20       | 1000   |
| 104        | Pen       | Mar   | 10       | 100    |
| 105        | Notebook  | Jan   | 18       | 900    |
| 105        | Pen       | Feb   | 22       | 220    |
| 105        | Pencil    | Mar   | 12       | 120    |
| 105        | Notebook  | Mar   | 10       | 500    |

---

## ✅ Expected Output File

| CustomerID | Qty_Notebook | Qty_Pen | Qty_Pencil | Amt_Notebook | Amt_Pen | Amt_Pencil |
|------------|--------------|---------|------------|--------------|---------|------------|
| 101        | 5            | 25      | 20         | 250          | 250     | 200        |
| 104        | 20           | 35      | 30         | 1000         | 350     | 300        |
| 102        | 12           | 28      | 10         | 600          | 280     | 100        |
| 103        | 16           | 12      | 15         | 800          | 120     | 150        |
| 105        | 28           | 22      | 12         | 1400         | 220     | 120        |

---

## 🛠 Step-by-Step Implementation

### 🔹 1. Create Storage Account
- **Name**: `sharadstorageaccount`
- **Region**: Asia Pacific (South India)
- **Performance**: Standard
- **Redundancy**: Locally Redundant Storage (LRS)
- **Access Tier**: Hot
- **Networking**: Public network access → Enabled

### 🔹 2. Create Containers
- `input` → For raw data (`sales_raw_data.txt`)
- `output` → For transformed data

### 🔹 3. Setup Azure Data Factory
- **Name**: `SharadDataFactory1`
- **Region**: Central India
- **Version**: V2
- Launch ADF Studio.

### 🔹 4. Create Dataset (Source)
- **Type**: Azure Blob Storage → DelimitedText
- **Linked Service**: Connected to `sharadstorageaccount`
- File Path: `input/sales_raw_data.txt`
- Verified with **Test Connection** ✅

### 🔹 5. Build Data Flow
- Source → Dataset from step 4.
- Data Preview → Verified data ingestion.

**Pivot Transformation**
- **Group By** → `CustomerID`
- **Pivot Key** → `Product`
- **Aggregations**:
  - `SUM(toInteger(Quantity))` → prefix `Qty_`
  - `SUM(toInteger(Amount))` → prefix `Amt_`

**Sink**
- Dataset: Azure Blob Storage → DelimitedText
- Linked Service: Same as source
- File Path: `output/`
- Optimized with **Single Partition** → single output file.

### 🔹 6. Pipeline Setup
- Created new pipeline.
- Drag & Drop Data Flow into pipeline.
- Publish → Trigger Now.
- **Monitor Tab** → Verified successful pipeline execution.

### 🔹 7. Validate Output
- Final transformed file stored in `output` container.
- Verified correct pivoted structure.

---

## 📸 Screenshots
(Add your **40 screenshots** here step-by-step. Example:)

1. Storage Account creation  
   ![Storage Account](screenshots/storage_account.png)

2. Container Setup  
   ![Containers](screenshots/containers.png)

3. Dataset Configuration  
   ![Dataset](screenshots/dataset.png)

... (continue for all steps)  

---

## 🎯 Key Learnings
- Azure Storage Account setup (Blob & Data Lake Gen2).
- Dataset creation and Linked Service in ADF.
- **Pivot Transformation** for reshaping data.
- End-to-end pipeline execution & monitoring.
- Data validation in Sink.

---

## 🏁 Conclusion
This project demonstrates how to use **Azure Data Factory** to transform **raw transactional data** into a **customer-centric summary** using pivot transformations.  
It can be extended for **real-world analytics pipelines** such as sales aggregation, reporting dashboards, and data warehouse ETL.

---
