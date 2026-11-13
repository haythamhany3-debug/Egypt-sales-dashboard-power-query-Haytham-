# 📊 Egypt Retail Sales Dashboard (Power Query + Excel)

An end-to-end **data cleaning and sales analysis project** built in **Microsoft Excel** using **Power Query** for ETL and **PivotTables / PivotCharts** for reporting.

Raw monthly order files, a product list, and a customer list are cleaned, standardized, and modeled, then summarized in a dashboard showing sales performance by product, category, and city.

---

## 🎯 Project Goals

- Combine many monthly order files into one clean orders table
- Fix messy dates, prices, names, and regions
- Remove duplicates and incomplete records
- Build a data model linking **Orders → Products → Customers**
- Answer business questions with PivotTables and charts

---

## 🗂️ Data Sources

| Table | Source | Key Columns |
|-------|--------|-------------|
| **Orders** | Folder of monthly files (`Orders\`) | OrderID, CustomerID, ProductID, OrderDate, Quantity |
| **Products** | `Products.csv` | ProductID, ProductName, Category, Price |
| **Customers** | `Customers.csv` | CustomerID, CustomerName, Region |

---

## 🧹 Power Query Cleaning Steps

### 1. Orders (folder import)
- Load all files with `Folder.Files`, filter hidden files, and apply a **Transform File** function to each
- Expand and combine into a single table, keeping `Source.Name` (file name)
- Set correct data types
- Trim text and remove duplicate `OrderID`s
- Remove rows with missing `ProductID` or `Quantity`
- **Fix inconsistent date formats:**
  - Replace `/` with `-` and split the date into 3 parts
  - Detect the **Year** (value ≥ 35 in either the first or last part)
  - Extract the **Month** from the file name (text between `_` and `.`)
  - Derive the **Day** from the remaining part (≤ 31 and different from month)
  - Rebuild a proper date column (`New Year`, type Date)
- Generate a fresh sequential **OrderID** with an index column
- Reorder columns and remove helper columns (Year, Month, Day)

### 2. Products
- Import CSV and promote headers
- Remove duplicate `ProductID`s
- Trim whitespace and apply **Proper Case** to `ProductName` and `Category`
- Replace text price `"Two Hundred"` with `200`
- Strip the `$` symbol and convert `Price` to **Currency** type

### 3. Customers
- Import CSV and promote headers
- Remove duplicate `CustomerID`s
- Trim and **Proper Case** the customer name
- Split `CustomerName` into **First Name** and **Last Name**
- Clean `Region`: trim, remove extra spaces, apply Proper Case

---

<img width="517" height="270" alt="image" src="https://github.com/user-attachments/assets/afe8925a-39d1-458e-93f6-397c89ee2b8a" />

The workbook (`hh.xlsx`) contains PivotTables and charts that cover:

| Visual | Description |
|--------|-------------|
| **3D Column Chart** | Total sales, total quantity, and average sales per order by product |
| **Pie Chart** | Order count by product category |
| **Column Chart** | Total customers by city |
| **3D Column Chart** | Total sales by city |

### Key Numbers

| Metric | Value |
|--------|-------|
| 💰 Total Sales | **$101,208,243** |
| 📦 Total Quantity Sold | **108,203 units** |
| 🧾 Total Orders | **19,606** |
| 💵 Average Sales per Order | **≈ $5,162** |
| 👥 Total Customers | **300** |

### Sales by City

| City | Total Sales | Customers |
|------|------------:|----------:|
| Alexandria | $18,671,331 | 56 |
| Aswan | $20,595,672 | 60 |
| Cairo | $20,462,357 | 61 |
| Giza | $20,412,093 | 61 |
| Mansoura | $21,066,790 | 62 |

### Orders by Category

| Category | Orders |
|----------|-------:|
| Clothing | 4,010 |
| Electronics | 3,962 |
| Furniture | 3,932 |
| Books | 3,867 |
| Toys | 3,835 |

### Highlights
- 🏆 **Mansoura** has the highest sales and the most customers; **Alexandria** has the lowest on both
- 👕 **Clothing** is the category with the most orders
- 🧸 **Doll**, **Shirt**, and **Pants** are among the top products by sales; **Sofa** and **Headphones** are among the lowest

---

## 🛠️ Tools & Skills

- Microsoft Excel
- Power Query (M language)
- PivotTables & PivotCharts
- Data cleaning, transformation, and modeling
- Data visualization

---

## 📁 Repository Structure

```
├── README.md
├── hh.xlsx                         # Final workbook with dashboard
├── Orders/                         # Monthly order files (raw data)
├── Products.csv
├── Customers.csv
└── Orders_and_Products_and_Customers.txt   # Power Query (M) applied steps
```

---

## 🚀 How to Use

1. Clone or download this repository
2. Open `hh.xlsx` in Excel
3. Go to **Data → Queries & Connections** and update the file paths to match your local folders
4. Click **Data → Refresh All**
5. Explore the PivotTables and charts on the dashboard sheet

> **Note:** The Power Query scripts use local paths such as `E:\SIS part\Material\Session 7\PowerQuery\`. Change them to your own location.

---

## 💡 Possible Improvements

- Add a **Date table** and time-based analysis (monthly / yearly trends)
- Add slicers for City, Category, and Product
- Replace "Sum of CustomerID" / "Sum of OrderID" with **Distinct Count** measures (summing IDs has no business meaning)
- Build a Power BI version of the dashboard

---

## 👤 Author

**Your Name**  
📧 your.email@example.com  
🔗 [LinkedIn](https://linkedin.com/in/your-profile)
