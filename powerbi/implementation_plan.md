# Implementation Plan - E-Commerce Sales Dashboard Project

This plan outlines the steps to build a complete, professional E-Commerce Sales Dashboard project from scratch for college portfolio use. Since we are initializing this project on your system, we will programmatically generate the dataset and the Excel workbook structure to give you a solid foundation.

## User Review Required

> [!IMPORTANT]
> - We will generate the 1200-row realistic e-commerce dataset (`ecommerce_data.csv`) using a Python script.
> - We will programmatically create the Excel workbook (`Sales_Dashboard.xlsx`) with two pre-configured sheets: **Raw Data** (formatted as a table) and **Dashboard** (styled with a Premium Dark Navy theme, including working KPI formulas pointing to the raw data).
> - Since Power BI `.pbix` files are proprietary binary packages, you will follow the step-by-step instructions provided in the guide to load the CSV, write DAX, and construct the visuals.
> - We will draft the `README.md` and a comprehensive `PROJECT_REPORT.md` (which you can export to PDF for college submission).

## Open Questions

- *Color Palette Preference*: The default dashboard design proposed uses a **Premium Dark Navy theme (#1E2A3A)** for Excel and Power BI. If you prefer a **Light Minimalist theme**, please let us know. Otherwise, we will proceed with the Premium Dark Navy theme as it looks highly professional.
- *Price Ranges*: Prices will be generated in Indian Rupees (₹) with realistic distributions:
  - Electronics (Mobiles, Laptops, etc.): ₹1,500 - ₹75,000
  - Clothing: ₹499 - ₹4,999
  - Books: ₹199 - ₹999
  - Home & Kitchen: ₹299 - ₹8,999
  - Sports: ₹199 - ₹14,999

## Proposed Changes

We will create the directory structure and files in the workspace `c:\Users\bhanu\OneDrive\Desktop\SALES DASHBOARD`.

---

### 1. File Structure Setup

We will create the folders required for the project:
- [NEW] `data/`
- [NEW] `excel/`
- [NEW] `powerbi/`
- [NEW] `screenshots/`

---

### 2. Dataset Generation

#### [NEW] [generate_data.py](file:///c:/Users/bhanu/OneDrive/Desktop/SALES%20DASHBOARD/scratch/generate_data.py)
A Python utility script to generate `data/ecommerce_data.csv` with exactly 1200 rows of realistic transaction data for the year 2024. The script will:
- Generate IDs: `ORD-1001` to `ORD-2200`.
- Match dates randomly across 2024, ensuring appropriate Month and Quarter names.
- Map regions to correct states:
  - North: Delhi, Punjab, UP
  - South: Tamil Nadu, Kerala, Telangana
  - East: West Bengal, Odisha, Bihar
  - West: Maharashtra, Gujarat, Rajasthan
- Map Category -> Sub-Category -> realistic Products.
- Calculate formulas:
  - `Sales_Amount = Quantity * Unit_Price`
  - `Discount_Amount = Sales_Amount * Discount_Percent / 100`
  - `Net_Sales = Sales_Amount - Discount_Amount`
  - `Cost_Price = Net_Sales * 0.65` (with slight random variation of ±3% to make profit margins realistic and dynamic)
  - `Profit = Net_Sales - Cost_Price`
  - `Profit_Margin_Percent = (Profit / Net_Sales) * 100`
- Assign random Customer Segments, Payment Modes, and Order Status.

---

### 3. Excel Workbook Generation

#### [NEW] [generate_excel.py](file:///c:/Users/bhanu/OneDrive/Desktop/SALES%20DASHBOARD/scratch/generate_excel.py)
A Python script using the `openpyxl` library to create `excel/Sales_Dashboard.xlsx`. The workbook will contain:
- **Raw Data** sheet: Contains the 1200 rows of generated data, formatted as an Excel Table named `DataTable` with blue/grey styling, frozen top header, and appropriate column formatting (Currency for sales/profit, Percentage for discount).
- **Dashboard** sheet:
  - A beautiful Dark Navy header block styled with title: "E-COMMERCE SALES DASHBOARD (2024)" and subtitle: "TKREC B.Tech Data Science - Baikam Bhanu Prakash".
  - Four styled KPI Cards containing working Excel formulas:
    - **Total Revenue**: `=SUM(RawData_Sales)`
    - **Total Orders**: `=COUNTA(RawData_Orders)`
    - **Average Order Value (AOV)**: `=Revenue/Orders`
    - **Total Profit**: `=SUM(RawData_Profit)`
    - **Overall Profit Margin %**: `=Profit/Revenue`
  - Gridlines hidden for a clean, dashboard-like app feel.
  - Slices/charts placeholders marked visually, which you will insert following our step-by-step instructions.

---

### 4. Portfolio Documentation

#### [NEW] [README.md](file:///c:/Users/bhanu/OneDrive/Desktop/SALES%20DASHBOARD/README.md)
The primary repository README structured as a professional GitHub landing page, including project details, tools, architecture, and deployment links.

#### [NEW] [PROJECT_REPORT.md](file:///c:/Users/bhanu/OneDrive/Desktop/SALES%20DASHBOARD/PROJECT_REPORT.md)
A comprehensive academic-style project report that can be copy-pasted or exported to a PDF. It includes:
- Executive Summary
- Project Objectives & Scope
- Data Dictionary & Schema
- Excel Pivot Tables & Charts configuration
- Power BI DAX Measures & Data Modeling
- Step-by-Step GitHub & Power BI Service Publishing instructions
- Conclusion & Learnings

---

## Verification Plan

### Automated Verification
- We will execute `generate_data.py` to create `ecommerce_data.csv`.
- We will write a validation test script `validate_data.py` to ensure:
  - Exactly 1200 rows are present.
  - All columns are correctly populated.
  - Formulas (`Sales_Amount`, `Discount_Amount`, `Net_Sales`, `Profit`, `Profit_Margin_Percent`) are mathematically correct.
  - State-region mappings are correct.
- We will execute `generate_excel.py` to create the Excel workbook and inspect its structure.

### Manual Verification
- You will open `excel/Sales_Dashboard.xlsx` in Microsoft Excel to confirm that the styled Dashboard sheet, raw table, and KPI formulas load perfectly.
- You will follow the step-by-step instructions in the `PROJECT_REPORT.md` to load the data into Power BI, configure the modeling relationships, write the DAX measures, build the 3-page layout, and publish the dashboard online.
