

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
101,Pen,Jan,10,100
101,Notebook,Jan,5,250
101,Pencil,Feb,20,200
101,Pen,Feb,15,150
102,Pen,Jan,8,80
102,Notebook,Jan,12,600
102,Pencil,Feb,10,100
102,Pen,Mar,20,200
103,Notebook,Jan,7,350
103,Pencil,Feb,15,150
103,Pen,Feb,12,120
103,Notebook,Mar,9,450
104,Pen,Jan,25,250
104,Pencil,Jan,30,300
104,Notebook,Feb,20,1000
104,Pen,Mar,10,100
105,Notebook,Jan,18,900
105,Pen,Feb,22,220
105,Pencil,Mar,12,120
105,Notebook,Mar,10,500

...


