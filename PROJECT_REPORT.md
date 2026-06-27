# 🎓 ACADEMIC PROJECT REPORT
## E-Commerce Sales Dashboard (Excel & Power BI)

**Submitted by:** Baikam Bhanu Prakash (SAI)  
**College:** Teegala Krishna Reddy Engineering College (TKREC), Hyderabad  
**Branch:** B.Tech - Data Science (Batch 2024-2028)  
**Affiliation:** Jawaharlal Nehru Technological University Hyderabad (JNTUH)  

---

## 1. Executive Summary
This project presents a comprehensive, interactive Business Intelligence (BI) dashboard analyzing **1,200 simulated e-commerce transactions** across India for the calendar year 2024. Using a combined toolchain of **Microsoft Excel** and **Microsoft Power BI**, the project implements an end-to-end data lifecycle: from synthetic dataset generation, ETL (Extract, Transform, Load) pipelines, database schema design, and DAX modeling, to visual reporting and cloud deployment on the Power BI Service. The results provide actionable insights into product sales distribution, quarterly and monthly profit trends, regional revenue contributions, customer segment behaviors, and payment mode efficiency.

---

## 2. Project Objectives & Scope
The core objectives of this B.Tech Data Science portfolio project are:
1. **Apply ETL Principles**: Import, clean, format, and structure unstructured order data.
2. **Build Financial Logic**: Implement standard business metrics (Gross Revenue, Discounts, Net Sales, Cost of Goods Sold, Net Profit, and Profit Margin %).
3. **Data Modeling**: Design a star-schema relation using a distinct `DateTable` dimension linked to the fact dataset.
4. **Visual Storytelling**: Build user-friendly dashboard interfaces using standard design colors, clear visual hierarchies, and interactive slicers.
5. **Demonstrate Version Control**: Manage the project directories and artifacts using Git and GitHub.
6. **Cloud Deployment**: Publish the report to Power BI Service to verify live interactive visuals.

---

## 3. Data Dictionary (Dataset Schema)
The dataset contains 1,200 rows of transactional records. Below is the detailed schema:

| Column Name | Data Type | Description / Constraints |
| :--- | :--- | :--- |
| **Order_ID** | Text (String) | Unique alphanumeric order identifier (range: `ORD-1001` to `ORD-2200`). |
| **Date** | Date | Transaction date between `01-Jan-2024` and `31-Dec-2024`. |
| **Month** | Text | Three-letter abbreviation (`Jan`, `Feb`, `Mar`, etc.). |
| **Quarter** | Text | Calendar Quarter (`Q1`, `Q2`, `Q3`, `Q4`). |
| **Year** | Integer | Transaction Year (strictly `2024`). |
| **Region** | Text | Geographical region of customer (North, South, East, West). |
| **State** | Text | The Indian state associated with the region (e.g. North ➔ Delhi, Punjab, UP). |
| **Category** | Text | Product Category (Electronics, Clothing, Books, Home & Kitchen, Sports). |
| **Sub_Category** | Text | Sub-classification mapping (e.g., Electronics ➔ Mobile, Laptop, Tablet). |
| **Product_Name** | Text | Individual item brand and model name. |
| **Quantity** | Integer | Number of units ordered (range: `1` to `5`). |
| **Unit_Price** | Decimal | Retail unit cost in Indian Rupees (₹). |
| **Sales_Amount** | Decimal | Gross amount before discount (`Quantity * Unit_Price`). |
| **Discount_Percent**| Decimal | Percent discount applied (`0%`, `5%`, `10%`, `15%`, `20%`). |
| **Discount_Amount** | Decimal | Sales deduction (`Sales_Amount * (Discount_Percent / 100)`). |
| **Net_Sales** | Decimal | Realized revenue before expenses (`Sales_Amount - Discount_Amount`). |
| **Cost_Price** | Decimal | Cost of goods sold (`Net_Sales * 0.65` approximate, with random ±3% variation). |
| **Profit** | Decimal | Net profit realized (`Net_Sales - Cost_Price`). |
| **Profit_Margin_Percent** | Decimal | Percentage profit margin ratio (`(Profit / Net_Sales) * 100`). |
| **Customer_Segment**| Text | Demographics label (Regular, Premium, New). |
| **Payment_Mode** | Text | Method used (UPI, Credit Card, Debit Card, Net Banking, COD). |
| **Order_Status** | Text | Fulfillment state (Delivered, Returned, Pending). |

---

## 4. Phase A: Microsoft Excel Dashboard Implementation

### Step 1: Data Importation & Formatting
1. Open a blank workbook in **Microsoft Excel**.
2. Go to the **Data** tab on the ribbon ➔ **From Text/CSV** in the *Get & Transform Data* group.
3. Select `data/ecommerce_data.csv` and click **Import**.
4. Set File Origin to **65001: Unicode (UTF-8)**, Delimiter to **Comma**, and click **Load**.
5. Rename the imported spreadsheet tab to `Raw Data`.
6. Select any cell inside the data, press `Ctrl + T` (or **Home** ➔ **Format as Table**), select a blue table style, and name the table `DataTable` in the Table Design tab.
7. Change formatting of columns:
   - Select Column `L` (Unit Price), `M` (Sales Amount), `O` (Discount Amount), `P` (Net Sales), `Q` (Cost Price), and `R` (Profit) ➔ Format as **Currency (₹ Indian standard or standard decimal currency)**.
   - Select Column `N` (Discount Percent) and `S` (Profit Margin) ➔ Format as **Percentage** with 2 decimal places.
8. Freeze the headers: Select cell `A2`, go to the **View** tab ➔ **Freeze Panes** ➔ **Freeze Panes** (or **Freeze Top Row**).

### Step 2: Creating Pivot Tables
Create a new sheet called `Pivot Tables` and construct these summaries:

*   **Pivot Table 1: Regional Sales**
    - Drag `Region` to **Rows**
    - Drag `Net_Sales` to **Values** (summarized as Sum, display as Currency)
    - Drag `Order_ID` to **Values** (summarized as Count)
    - Drag `Profit` to **Values** (summarized as Sum, display as Currency)
*   **Pivot Table 2: Category Contribution**
    - Drag `Category` to **Rows**
    - Drag `Net_Sales` to **Values** (summarized as Sum)
    - Drag `Order_ID` to **Values** (summarized as Count)
*   **Pivot Table 3: Monthly Trends**
    - Drag `Month` to **Rows** (ensure sorted chronologically: Jan, Feb, Mar, etc.)
    - Drag `Net_Sales` to **Values** (Sum)
    - Drag `Profit` to **Values** (Sum)
*   **Pivot Table 4: Product Leaderboard (Top 10)**
    - Drag `Product_Name` to **Rows**
    - Drag `Net_Sales` to **Values** (Sum, sorted descending)
    - Apply value filter: Click Row Labels filter drop-down ➔ **Value Filters** ➔ **Top 10** (Filter by Sum of Net_Sales).
*   **Pivot Table 5: Payment Method Share**
    - Drag `Payment_Mode` to **Rows**
    - Drag `Order_ID` to **Values** (Count)
    - Drag `Net_Sales` to **Values** (Sum)
*   **Pivot Table 6: Customer Segment Metrics**
    - Drag `Customer_Segment` to **Rows**
    - Drag `Net_Sales` to **Values** (Sum)
    - Drag `Profit` to **Values** (Sum)

### Step 3: Excel Dashboard Formatting & Visuals
1. Create a new sheet tab named `Dashboard`.
2. Go to **View** and uncheck **Gridlines** to clean the page.
3. Design a dark header from cell `B2` to `Q4` filled with Dark Navy (`#1E2A3A`). Write the dashboard title in white bold Segoe UI.
4. Enter the formulas for the styled **KPI Cards** in the merged cells:
   - **Total Revenue**: `=SUM('Raw Data'!P:P)`
   - **Total Orders**: `=COUNTA('Raw Data'!A:A)-1`
   - **Average Order Value (AOV)**: `=B7/E7` (where B7 is Revenue and E7 is Orders)
   - **Total Profit**: `=SUM('Raw Data'!R:R)`
   - **Profit Margin %**: `=K7/B7` (where K7 is Total Profit and B7 is Revenue)
5. Generate the charts from the Pivot Tables sheet:
   - **Chart 1**: Clustered Bar Chart ➔ Move to Dashboard cell `B13` (Revenue by Region).
   - **Chart 2**: Donut Chart ➔ Move to Dashboard cell `K13` (Sales by Category).
   - **Chart 3**: Line Chart ➔ Move to Dashboard cell `B24` (Monthly Trend).
   - **Chart 4**: Horizontal Bar Chart ➔ Move to Dashboard cell `K24` (Top 10 Products).
6. Insert Slicers: Select any chart ➔ **PivotTable Analyze** or **Chart Analyze** ➔ **Insert Slicer** ➔ Choose `Region`, `Category`, `Month`, `Quarter`.
7. **Crucial Connection**: Right-click each slicer ➔ **Report Connections** ➔ Check all pivot tables so that clicking a slicer filters every visual simultaneously.

---

## 5. Phase B: Power BI Dashboard & DAX modeling

### Step 1: Transform Data in Power Query
1. Open **Power BI Desktop**.
2. Click **Get Data** ➔ **Text/CSV** and select `data/ecommerce_data.csv`.
3. In the preview modal, click **Transform Data** to open the Power Query Editor.
4. Check columns and assign appropriate data types:
   - `Order_ID`, `Region`, `State`, `Category`, `Sub_Category`, `Product_Name`, `Customer_Segment`, `Payment_Mode`, `Order_Status` ➔ **Text**
   - `Date` ➔ **Date**
   - `Year` ➔ **Whole Number**
   - `Quantity` ➔ **Whole Number**
   - `Unit_Price`, `Sales_Amount`, `Discount_Amount`, `Net_Sales`, `Cost_Price`, `Profit` ➔ **Fixed Decimal Number** (Currency)
   - `Discount_Percent`, `Profit_Margin_Percent` ➔ **Decimal Number**
5. Click **Close & Apply** in the Home tab.

### Step 2: Establish the Date Dimension (Date Table)
To ensure reliable time-intelligence reporting, a standalone date table must be established:
1. In the Report view, go to **Modeling** on the ribbon ➔ Click **New Table**.
2. Enter the DAX query:
   ```dax
   DateTable = CALENDAR(DATE(2024, 1, 1), DATE(2024, 12, 31))
   ```
3. With the new table selected, add these calculated columns one by one by clicking **New Column**:
   ```dax
   Month = FORMAT(DateTable[Date], "MMM")
   ```
   ```dax
   Month Number = MONTH(DateTable[Date])
   ```
   ```dax
   Quarter = "Q" & QUARTER(DateTable[Date])
   ```
   ```dax
   Year = YEAR(DateTable[Date])
   ```
4. **Sort Order Alignment**: Select the `Month` column in the data view ➔ Go to **Column Tools** ➔ **Sort by Column** ➔ Select `Month Number` (this prevents alphabetical listing like Apr, Aug, Dec, and enforces Jan, Feb, Mar, etc.).
5. **Relationship Configuration**: Switch to the **Model View** (left pane) ➔ Drag `DateTable[Date]` to `Raw Data[Date]` (joins as a 1-to-many relationship where the DateTable filters the transaction table).

### Step 3: DAX Modeling Measures
For academic consistency, create a blank table called `_Measures` (Home ➔ **Enter Data** ➔ Name it `_Measures`) and right-click it to add these 10 calculated DAX measures:

1. **Total Revenue** (Calculates sum of Net Sales):
   ```dax
   Total Revenue = SUM('Raw Data'[Net_Sales])
   ```
2. **Total Orders** (Counts total rows):
   ```dax
   Total Orders = COUNTROWS('Raw Data')
   ```
3. **Average Order Value (AOV)**:
   ```dax
   AOV = DIVIDE([Total Revenue], [Total Orders], 0)
   ```
4. **Total Profit**:
   ```dax
   Total Profit = SUM('Raw Data'[Profit])
   ```
5. **Profit Margin %**:
   ```dax
   Profit Margin % = DIVIDE([Total Profit], [Total Revenue], 0) * 100
   ```
6. **Total Discount Amount**:
   ```dax
   Total Discount = SUM('Raw Data'[Discount_Amount])
   ```
7. **Revenue Last Month** (Time intelligence measure):
   ```dax
   Revenue Last Month = 
   CALCULATE(
       [Total Revenue],
       DATEADD(DateTable[Date], -1, MONTH)
   )
   ```
8. **Revenue Growth %** (Month-over-month comparisons):
   ```dax
   Revenue Growth % = 
   DIVIDE(
       [Total Revenue] - [Revenue Last Month],
       [Revenue Last Month],
       0
   ) * 100
   ```
9. **Top Selling Category**:
   ```dax
   Top Category = 
   CALCULATE(
       FIRSTNONBLANK('Raw Data'[Category], 1),
       TOPN(
           1,
           SUMMARIZE('Raw Data', 'Raw Data'[Category], "Rev", [Total Revenue]),
           [Rev], DESC
       )
   )
   ```
10. **Average Quantity per Order**:
    ```dax
    Avg Order Size = AVERAGE('Raw Data'[Quantity])
    ```

---

## 6. Page Layout and Visualization Configuration

### Page 1: Main Sales Dashboard
*   **Visual 1-5 (KPI Cards)**: Place individual card visuals at the top for:
    - `Total Revenue` (formatted as Currency ₹, auto-units)
    - `Total Orders` (whole number)
    - `AOV` (Currency ₹)
    - `Total Profit` (Currency ₹)
    - `Profit Margin %` (Formatted with `%` suffix, e.g. `34.9%`)
*   **Visual 6 (Revenue by Region)**: Clustered Bar Chart.
    - Y-Axis: `Region`, X-Axis: `Total Revenue`, Legend: `Category`.
*   **Visual 7 (Category Contribution)**: Donut Chart.
    - Legend: `Category`, Values: `Total Revenue` (Display percentage and category labels).
*   **Visual 8 (Revenue & Profit Trend)**: Line Chart.
    - X-Axis: `Month` (from `DateTable`, sorted), Y-Axis: `Total Revenue` and `Total Profit`.
*   **Visual 9 (Top 10 Products)**: Horizontal Bar Chart.
    - Y-Axis: `Product_Name`, X-Axis: `Total Revenue`. Set visual filter to `Top N` ➔ `N = 10` by `Total Revenue`.
*   **Visual 10 (Quarterly Performance)**: Stacked Bar Chart.
    - X-Axis: `Quarter`, Y-Axis: `Total Revenue`, Legend: `Region`.
*   **Visual 11 (Payment Mode Distribution)**: Pie Chart.
    - Legend: `Payment_Mode`, Values: `Total Orders` (Shows popularity of UPI, cards, and COD).
*   **Slicers Pane (Filters)**:
    - Dropdowns: `Region`, `Category`.
    - Horizontal lists: `Quarter`, `Customer_Segment`.

### Page 2: Regional Analysis
*   **Map Visual**: Add the standard Map visual. Set location to `State` (ensure country is recognized as India) and Bubble Size to `Total Revenue`.
*   **Revenue by State**: Column chart showing state-by-state net sales sorted from largest to smallest.
*   **Regional Filter**: Vertical slicer for `Region`.

### Page 3: Product Analysis
*   **Top 10 Products Table**: Table visual containing columns `Product_Name`, `Category`, `Total Revenue`, `Total Orders`, and `Total Profit`.
*   **Sub-Category Heatmap**: Treemap visual displaying `Sub_Category` size relative to `Total Revenue`.
*   **Product Filter**: Dropdown slicer for `Category` and `Sub_Category`.

---

## 7. Phase C: GitHub Upload & Source Control

### Step-by-Step GitHub Setup
1. Log in to [GitHub](https://github.com).
2. Click the **New** repository button.
3. Repository name: `ecommerce-sales-dashboard`.
4. Description: `Interactive Sales Dashboard using Excel and Power BI for college portfolio | B.Tech Data Science Project at TKREC.`
5. Visibility: **Public**.
6. Check **Add a README file** and select **Add .gitignore** (choose *None* or *Windows*). Click **Create repository**.
7. Open **GitHub Desktop** ➔ File ➔ **Clone Repository** ➔ Select `ecommerce-sales-dashboard` and clone to your local PC.
8. Copy the folders (`data/`, `excel/`, `powerbi/`, `screenshots/`, `README.md`, `PROJECT_REPORT.md`) into your cloned repository folder.
9. In GitHub Desktop, you will see all changes lists. Write commit message: `"Initial upload of e-commerce dashboard dataset, Excel template, and academic report"`.
10. Click **Commit to main** ➔ **Push origin** to upload.

---

## 8. Phase D: Cloud Deployment (Power BI Service)

### Step-by-Step Publishing
1. Register/Sign in to the [Power BI Portal](https://app.powerbi.com/) using your college email credentials.
2. In the left panel, select **Workspaces** ➔ **Create a workspace** ➔ Name it `"SAI - Sales Dashboard"`.
3. In **Power BI Desktop**, open `Sales_Dashboard.pbix` and click **Publish** on the Home tab ribbon.
4. Select the `"SAI - Sales Dashboard"` workspace and click **Select**.
5. Once published successfully, click the link on the screen or open the cloud workspace in your browser.
6. Open your published report in the workspace.
7. Go to **File** ➔ **Embed report** ➔ **Website or portal**.
8. Copy the generated URL and paste it under the **Live Dashboard** section in your `README.md` file.

---

## 9. Academic Conclusions & Learnings
Building this project developed core industry competencies:
*   **ETL Pipeline Efficiency**: Learned to import unstructured CSVs, clean date entries, enforce consistent naming, and standardize float values.
*   **DAX Scripting**: Mastered using `DIVIDE` to avoid division-by-zero errors and using time intelligence (`DATEADD`) to calculate periodic trends.
*   **Business Intelligence Best Practices**: Applied visual hierarchy rules by using size and color contrast to highlight key metrics over secondary graphs.
*   **Deployment Cycle**: Understand how local desktop dashboards sync with cloud workspaces and how code updates are managed through version control (Git).
