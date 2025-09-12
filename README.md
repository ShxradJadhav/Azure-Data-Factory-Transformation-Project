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

1. Storage Account creation  
<img width="960" height="540" alt="1img" src="https://github.com/user-attachments/assets/9647c5fa-4335-49ac-9949-bfff8afbffb3" />
   
<img width="960" height="540" alt="2img" src="https://github.com/user-attachments/assets/328acd9a-923d-41f3-ba90-611906346ca6" />

<img width="960" height="540" alt="3img" src="https://github.com/user-attachments/assets/f68e9597-9495-41c3-9d2f-e1db65bc513b" />

<img width="960" height="540" alt="4img" src="https://github.com/user-attachments/assets/7945988d-0753-417b-956a-6f33d9b1986d" />


2. Container Setup  
<img width="960" height="540" alt="5img" src="https://github.com/user-attachments/assets/fe903fe1-1473-4287-b5d3-5905bba3b0f4" />

<img width="960" height="540" alt="6img" src="https://github.com/user-attachments/assets/9bd1127b-0335-44ec-a704-591b08742a41" />


3. Azure Data Fctory Creation

<img width="960" height="540" alt="7img" src="https://github.com/user-attachments/assets/d5b5d963-0ec2-45ab-be8e-ac30b0866505" />

<img width="960" height="540" alt="8img" src="https://github.com/user-attachments/assets/09769028-b62c-4772-9315-648cf3a756b0" />

<img width="960" height="540" alt="9img" src="https://github.com/user-attachments/assets/e05e3dcb-b741-46e1-a4a6-59ff4cff0bc6" />

<img width="960" height="540" alt="10img" src="https://github.com/user-attachments/assets/ef020acb-9a31-4984-843b-70f201e7e72f" />

<img width="960" height="540" alt="11img" src="https://github.com/user-attachments/assets/e03a7a23-ce41-46e1-8b37-921d42f67eb1" />

<img width="960" height="540" alt="12img" src="https://github.com/user-attachments/assets/8357cd3d-77a4-4229-a21a-6cbaf85a4edf" />


3. Dataset Configuration  
<img width="960" height="540" alt="13img" src="https://github.com/user-attachments/assets/1c22f8a8-bebd-4c7b-958a-54b7ff5fbb3e" />

<img width="960" height="540" alt="14img" src="https://github.com/user-attachments/assets/556a3f8d-7fe8-450b-96cb-1b8d8da13056" />

<img width="960" height="540" alt="15img" src="https://github.com/user-attachments/assets/23d89395-a2ce-4035-858d-d33920386815" />

<img width="960" height="540" alt="16img" src="https://github.com/user-attachments/assets/912af055-590f-4e4c-8859-a26363445c6a" />

<img width="960" height="540" alt="17img" src="https://github.com/user-attachments/assets/de2e3115-1805-411e-acff-93d71b2a52d1" />

<img width="960" height="540" alt="18img" src="https://github.com/user-attachments/assets/fd6b8264-f613-4d37-b594-2565c67aeb7f" />

<img width="960" height="540" alt="19img" src="https://github.com/user-attachments/assets/128d067f-6eaa-48b3-83c1-e04842a75a25" />

<img width="960" height="540" alt="20" src="https://github.com/user-attachments/assets/dadc91ea-6c1c-4b64-b131-349e6570c7b1" />

<img width="960" height="540" alt="21img" src="https://github.com/user-attachments/assets/db65c122-596a-4dfe-8cdc-19f657fa41a0" />

<img width="960" height="540" alt="22img" src="https://github.com/user-attachments/assets/98df576f-0f66-4241-a6ee-cc62877d8240" />

<img width="960" height="540" alt="23img" src="https://github.com/user-attachments/assets/ff05da2d-f2c5-4361-9d54-a1719cf503fa" />





4.Data Flow Creation 



<img width="960" height="540" alt="24img" src="https://github.com/user-attachments/assets/3e6a47c3-464a-4d78-9ec4-d378f2a2b497" />

<img width="960" height="540" alt="25img" src="https://github.com/user-attachments/assets/ece8e98a-ed5b-4846-94ed-cd5ac9e0370d" />

<img width="960" height="540" alt="26img" src="https://github.com/user-attachments/assets/ce5d04f2-1458-4670-9117-cbfee199f777" />

<img width="960" height="540" alt="27img" src="https://github.com/user-attachments/assets/a9009a93-13e9-4638-9334-f2151ce41888" />

<img width="960" height="540" alt="28img" src="https://github.com/user-attachments/assets/9e566cb0-7d44-4279-aca0-d06ee0cb0114" />

<img width="960" height="540" alt="29img" src="https://github.com/user-attachments/assets/e52a3d2f-fa4c-48b1-bff2-ba396a88f0f0" />

<img width="960" height="540" alt="30img" src="https://github.com/user-attachments/assets/dfa0a26e-7d1b-4e43-9b5b-758568fe3bb6" />

<img width="960" height="540" alt="31img" src="https://github.com/user-attachments/assets/e6338682-9081-4031-b6ba-932428f295dd" />

<img width="960" height="540" alt="32img" src="https://github.com/user-attachments/assets/2dde76e4-e80d-4c8d-8060-4cfcd01c5d6d" />

<img width="960" height="540" alt="33img" src="https://github.com/user-attachments/assets/ba66ea8a-fff4-4640-982f-5808f3b1050a" />

<img width="960" height="540" alt="34img" src="https://github.com/user-attachments/assets/6ee072e8-7c53-4eca-8087-46c469539ed4" />

<img width="960" height="540" alt="35img" src="https://github.com/user-attachments/assets/e8e3805f-6d91-4fe1-a802-0740a8929f2d" />



5.Pipeline Creation

<img width="960" height="540" alt="36img" src="https://github.com/user-attachments/assets/60c3d1e6-443a-4395-b019-81d650a06791" />

<img width="960" height="540" alt="37img" src="https://github.com/user-attachments/assets/c823e94c-6403-4fcf-aa80-a0bea8648817" />

6. Trigeering

<img width="960" height="540" alt="38img" src="https://github.com/user-attachments/assets/0286aff7-af2a-4ba6-afd9-f9ad0fc81f7a" />

<img width="960" height="540" alt="39img" src="https://github.com/user-attachments/assets/1ef6cc98-ba96-4f37-bdbf-044827de8c87" />

7. Monetring

<img width="960" height="540" alt="40img" src="https://github.com/user-attachments/assets/74b72d9d-e76c-4257-a35e-5cfe648467f1" />

<img width="960" height="540" alt="41img" src="https://github.com/user-attachments/assets/61e8a307-40dd-4e03-a1cf-1c56c623cec4" />

8. Destination


<img width="960" height="540" alt="42img" src="https://github.com/user-attachments/assets/4911e017-704e-4e65-b706-1d0aafd0d70f" />

<img width="960" height="540" alt="43img" src="https://github.com/user-attachments/assets/75a97fe4-0d09-4850-812c-caa45b9cc505" />




 

















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
