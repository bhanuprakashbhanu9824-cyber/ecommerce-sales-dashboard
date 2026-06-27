# 📊 Power BI Data Analysis Project (Excel & Power BI)

An end-to-end business intelligence and data analytics project built from scratch to analyze 1,200+ realistic e-commerce orders for the year 2024. This repository contains the complete dataset, the Excel workbook model, and the step-by-step documentation for building and deploying the interactive Power BI dashboard.

---

## 🚀 Live Dashboard
🔗 **[View Live Dashboard on Power BI Service](https://app.powerbi.com/)** *(Paste your published shareable link here)*

---

## 📂 Project Structure
```text
ECommerce-Sales-Dashboard/
├── data/
│   └── ecommerce_data.csv          # Generated raw dataset (1,200 rows, 22 columns)
├── excel/
│   └── Sales_Dashboard.xlsx        # Excel workbook (Raw Data & Dashboard tabs)
├── powerbi/
│   └── Sales_Dashboard.pbix        # Power BI desktop model (Pages 1, 2 & 3)
├── screenshots/
│   └── dashboard_preview.png       # Interactive dashboard screenshot preview
├── README.md                       # Repository landing page
└── PROJECT_REPORT.md               # Detailed academic project report
```

---

## 🛠️ Tools & Technologies Used
* **Data Prep & Storage**: Microsoft Excel / CSV
* **Data Processing & Modeling**: Microsoft Power BI Desktop (Power Query & Data Model)
* **Calculations & Analytics**: DAX (Data Analysis Expressions) & Excel Formulas
* **Dashboard Design**: Custom Theme layout, KPI Cards, and Visual Charts
* **Version Control**: Git & GitHub Desktop
* **Deployment**: Power BI Service Cloud Workspace

---

## 📈 KPIs Tracked
* 💰 **Total Revenue**: Sum of Net Sales (`₹1.59 Crore+` total transaction value)
* 📦 **Total Orders**: Count of successful transactions (`1,200` total orders)
* 🧾 **Average Order Value (AOV)**: Average amount spent per transaction (`₹13,200+` average basket value)
* 📈 **Total Profit**: Sum of profit after subtracting Cost Price (`₹55.7 Lakh+`)
* 📊 **Profit Margin %**: Ratio of total profit to net revenue (maintained at an average of `~35%`)

---

## ⚡ Key Dashboard Features
1. **Multi-level Slicers**: Interactive filtering by *Region, Category, Month, Quarter*, and *Customer Segment*.
2. **Regional Performance**: Geo-spatial visualization mapping revenue across 12 Indian states (North, South, East, West).
3. **Category Breakdown**: Analysis of Sales and Profit trends across 5 categories (*Electronics, Clothing, Books, Home & Kitchen, Sports*).
4. **Time Series Analysis**: Interactive Line chart depicting monthly trends of Revenue and Profit throughout 2024.
5. **Top Product Leaderboard**: Dynamic ranking of top 10 products by Net Revenue.
6. **Payment Mode Share**: Visual breakdown of orders placed via UPI, Credit Card, Debit Card, Net Banking, and COD.

---

## 📝 Dataset Dictionary
The dataset `data/ecommerce_data.csv` contains exactly **1,200 rows** of order data with the following attributes:
* **Order_ID**: Unique identifier (ORD-1001 to ORD-2200)
* **Date**: Transaction date in 2024
* **Region / State**: Sales location mapping (Delhi, Tamil Nadu, West Bengal, Maharashtra, etc.)
* **Category / Sub_Category / Product_Name**: Structured item classifications
* **Quantity / Unit_Price / Sales_Amount**: Quantity ordered, price in ₹, and gross sales
* **Discount_Percent / Discount_Amount / Net_Sales**: Promotional deductions and final revenue
* **Cost_Price / Profit / Profit_Margin_Percent**: Financial profitability attributes
* **Customer_Segment / Payment_Mode / Order_Status**: Order demographics and delivery details

---

## 💻 How to Use and Run the Project

### 🟢 1. Microsoft Excel Dashboard
1. Go to the `excel/` folder in this repo and download [Sales_Dashboard.xlsx](excel/Sales_Dashboard.xlsx).
2. Open the file in Microsoft Excel 2016 or above.
3. The **Raw Data** sheet contains the formatted table. The **Dashboard** sheet has the visual grid structure, titles, and live formulas configured in the top KPI Cards.
4. *To build the Pivot Tables*: Go to **Insert** ➔ **PivotTable** using `DataTable` as source, place it in a new sheet "Pivot Tables", and create the regional, categorical, and trend summaries.
5. *To build Charts*: Insert the suggested charts (Bar, Line, Donut, Pie) from the Pivot Tables, format them to match the Dark Navy style, and paste them in the designated dashed placeholders on the Dashboard sheet.

### 🔵 2. Power BI Desktop Implementation
1. Download and open [Power BI Desktop](https://powerbi.microsoft.com/desktop) (free).
2. Click **Get Data** ➔ **Excel Workbook** or **Text/CSV** and import `data/ecommerce_data.csv`.
3. In **Power Query (Transform Data)**, verify data types (e.g. set `Date` as Date, currencies as decimal, quantities as whole numbers).
4. Go to **Modeling** ➔ **New Table** and paste the calendar script to create the `DateTable` relationship:
   ```dax
   DateTable = CALENDAR(DATE(2024,1,1), DATE(2024,12,31))
   ```
5. Add calculated columns to the DateTable (Month, Month Number, Quarter, Year) and link `DateTable[Date]` to `Raw Data[Date]`.
6. Create the 10 DAX measures documented in the project report (Revenue, Orders, AOV, Growth %, etc.).
7. Build the 3-page layout (*Main Dashboard, Regional Analysis, Product Analysis*) using the custom templates, slicers, and formatting.
8. Save as `Sales_Dashboard.pbix` in the `powerbi/` folder.

---

## 👤 Author Profile
* **Name**: Baikam Bhanu Prakash (SAI)
* **College**: Teegala Krishna Reddy Engineering College (TKREC), Hyderabad
* **Branch**: B.Tech - Data Science (Affiliated to JNTUH)
* **Batch**: 2024 - 2028
* **Contact**: [Your LinkedIn Profile] | [Your Email]

---

## 🎓 Academic Acknowledgments
This project has been built as a database-driven business intelligence solution for B.Tech Data Science academic portfolios, demonstrating hands-on expertise in ETL workflows, data modeling, DAX scripting, financial metric calculation, and dashboard deployment.
