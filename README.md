

# 📊 Azure Data Factory Transformation Project

## 📌 Project Overview
This project demonstrates how to use **Azure Data Factory (ADF)** to transform raw transactional sales data into a **consolidated single-row-per-customer format**.  

- **Input**: Raw sales data (multiple rows per customer, product-wise).  
- **Process**: Data Flow transformations in ADF (Pivot + Derived Column).  
- **Output**: One row per customer with product-wise quantities, amounts, and a calculated total amount.  

---

## 🏗️ Steps I Followed

### 1. Source Dataset
- Uploaded raw sales `.txt` file into **Azure Blob Storage**.  
- Sample input file:  

```csv
CustomerID,Product,Month,Quantity,Amount
101,Notebook,Jan,5,250
101,Pen,Jan,25,250
101,Pencil,Jan,20,200
102,Notebook,Feb,12,600
102,Pen,Feb,28,280
102,Pencil,Feb,10,100
...
