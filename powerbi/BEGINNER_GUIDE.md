# 🚀 Beginner's Click-by-Click Guide
## E-Commerce Sales Dashboard (Excel & Power BI)

Welcome, Sai! This guide is written specifically for you to build and complete your B.Tech Data Science project at TKREC step-by-step. Don't worry if you've never used Excel or Power BI before—just follow these exact clicks!

---

## 📂 PART 1: Find Your Files on Your PC
1. Go to your computer's Desktop.
2. Open the folder named **`SALES DASHBOARD`**.
3. You will see these folders already created for you:
   *   `data/` ➔ contains `ecommerce_data.csv` (your raw database of 1,200 orders).
   *   `excel/` ➔ contains `Sales_Dashboard.xlsx` (your Excel dashboard template).
   *   `powerbi/` ➔ empty folder (this is where you will save your Power BI file later).
   *   `screenshots/` ➔ empty folder (where you will save screenshots of your dashboard).

---

## 🟢 PART 2: Completing Your Excel Dashboard

We have already set up the raw data and designed a premium Dark Navy dashboard sheet with working formulas. Now, let's build the **Pivot Tables** and **Charts** that will sit on your dashboard.

### Step 2.1: Open the Excel File
1. Go to the `excel/` folder.
2. Double-click to open **`Sales_Dashboard.xlsx`**.
3. You will see two tabs at the bottom:
   *   **`Dashboard`**: A Dark Navy layout with your KPI Cards showing values like `₹15,920,405.00` (Total Revenue).
   *   **`Raw Data`**: The spreadsheet filled with 1,200 rows of blue table data.

### Step 2.2: Create a Pivot Table Sheet
1. Click on the **`Raw Data`** tab at the bottom.
2. Click any cell inside the blue data table.
3. On the top menu (Ribbon), click **Insert** ➔ click **PivotTable**.
4. In the box that pops up:
   *   Choose **New Worksheet**.
   *   Click **OK**.
5. Double-click the name of this new sheet at the bottom (usually named *Sheet1*) and rename it to **`Pivot Tables`**.

### Step 2.3: Build Pivot Table 1 (Revenue by Region)
1. Click inside the empty Pivot Table box on your new `Pivot Tables` sheet.
2. On the right side, you will see a pane called **PivotTable Fields**.
3. **Click and Drag** these fields:
   *   Drag **`Region`** into the **Rows** box.
   *   Drag **`Net_Sales`** into the **Values** box.
4. Right-click any number in the Pivot Table ➔ click **Number Format** ➔ select **Currency** ➔ click **OK** (this formats the values into Rupees ₹).

### Step 2.4: Turn Pivot Table 1 into a Chart
1. Click inside your new Pivot Table.
2. On the top menu, click **PivotTable Analyze** (or **Insert**) ➔ click **PivotChart**.
3. Select **Bar** (Clustered Bar Chart) ➔ click **OK**.
4. Click on the chart that appears. Press `Ctrl + X` (Cut).
5. Click on your **`Dashboard`** tab at the bottom.
6. Click near cell `B13` (where the dashed guide says *"Revenue by Region"*).
7. Press `Ctrl + V` (Paste) to place the chart here!
8. **Format it to match the Navy theme**:
   *   Double-click the chart background. Set **Fill** to *No fill* (so it is transparent) and **Border** to *No line*.
   *   Click the chart text/labels and change their color to **White** so they are visible.

### Step 2.5: Repeat for the Other Charts
Go back to the `Pivot Tables` sheet, click on a blank cell, click **Insert** ➔ **PivotTable** again using `DataTable` as the source, and repeat the process to build:
*   **Sales by Category**: Drag `Category` to Rows, `Net_Sales` to Values. Insert a **Donut Chart** and paste it at cell `K13`.
*   **Monthly Trend**: Drag `Month` to Rows, `Net_Sales` to Values. Insert a **Line Chart** and paste it at cell `B24`.
*   **Top 10 Products**: Drag `Product_Name` to Rows, `Net_Sales` to Values. Sort descending, filter top 10. Insert a **Bar Chart** and paste it at cell `K24`.

---

## 🔵 PART 3: Building the Power BI Dashboard

### Step 3.1: Import Your Data
1. Open the **Power BI Desktop** application. (If you don't have it, download it free from the Microsoft Store).
2. Click **Get data from another source** (or click **Home** ➔ **Get Data**).
3. Select **Text/CSV** ➔ click **Connect**.
4. Navigate to your desktop: `SALES DASHBOARD/data/` ➔ select **`ecommerce_data.csv`** ➔ click **Open**.
5. In the window that pops up, click **Load**.

### Step 3.2: Create the Calendar Table (Date Table)
1. On the top ribbon menu, click the **Modeling** tab.
2. Click **New Table**.
3. A formula bar will appear at the top. Copy and paste this exact line:
   ```dax
   DateTable = CALENDAR(DATE(2024, 1, 1), DATE(2024, 12, 31))
   ```
   Press Enter.
4. In the same **Modeling** tab, click **New Column** (do this 4 times to add these columns):
   *   **Month**: `Month = FORMAT(DateTable[Date], "MMM")`
   *   **Month Number**: `Month Number = MONTH(DateTable[Date])`
   *   **Quarter**: `Quarter = "Q" & QUARTER(DateTable[Date])`
   *   **Year**: `Year = YEAR(DateTable[Date])`
5. Go to the **Model View** (the icon with three small boxes connected on the far-left sidebar).
6. Click and drag the **`Date`** column from `DateTable` and drop it directly onto the **`Date`** column inside the **`Raw Data`** box. This creates a link (relationship) between them.

### Step 3.3: Write Your DAX Measures
1. Go back to the **Report View** (the canvas icon on the far-left sidebar).
2. Click **Home** ➔ click **Enter Data**.
3. In the box that opens, change the Name to **`_Measures`** and click **Create**. This creates a clean folder to store your math formulas.
4. Right-click the new `_Measures` table on the right side panel ➔ click **New Measure**.
5. Copy and paste this first formula:
   ```dax
   Total Revenue = SUM('Raw Data'[Net_Sales])
   ```
   Press Enter.
6. Repeat this step (right-click `_Measures` ➔ click **New Measure**) and copy-paste these formulas:
   *   **Total Orders**: `Total Orders = COUNTROWS('Raw Data')`
   *   **Average Order Value**: `AOV = DIVIDE([Total Revenue], [Total Orders], 0)`
   *   **Total Profit**: `Total Profit = SUM('Raw Data'[Profit])`
   *   **Profit Margin %**: `Profit Margin % = DIVIDE([Total Profit], [Total Revenue], 0) * 100`

### Step 3.4: Build the Visuals
1. **Add a Card (KPI)**: On the right side, click the **Card** visual icon (looks like a small box with "123").
   *   Drag **`Total Revenue`** from the `_Measures` list and drop it into the visual.
   *   Double-click to resize and place it at the top of your page.
2. **Add a Bar Chart (Revenue by Region)**: Click the **Clustered Bar Chart** icon in the visuals pane.
   *   Drag **`Region`** into the *Y-axis* box.
   *   Drag **`Total Revenue`** into the *X-axis* box.
3. **Add Slicers (Filters)**: Click the **Slicer** icon (looks like a funnel on a card).
   *   Drag **`Region`** into it. Now you can click "North", "South", etc. to filter the entire page!
4. Go to **File** ➔ **Save As** ➔ Save it inside your `powerbi/` folder as **`Sales_Dashboard.pbix`**.

---

## 🐱 PART 4: Uploading to GitHub (Your Online Portfolio)

To show your college professors, you must upload these files to GitHub.

### Step 4.1: Download GitHub Desktop
1. Download and install [GitHub Desktop](https://desktop.github.com) on your PC.
2. Open it and sign in with your GitHub account (create one free on github.com if you haven't).

### Step 4.2: Create Repository online
1. Open your browser and go to [github.com](https://github.com).
2. Click the green **New** button on the left.
3. Type Repository Name: **`ecommerce-sales-dashboard`**.
4. Set visibility to **Public** ➔ Check **Add a README file** ➔ Click **Create repository** at the bottom.

### Step 4.3: Upload Your Files
1. Open **GitHub Desktop** on your computer.
2. Click **File** (top left) ➔ click **Clone Repository**.
3. Select your repository `ecommerce-sales-dashboard` from the list and click **Clone**.
4. It will create a folder on your PC. Click **Show in Explorer** to open it.
5. **Copy all files** from your desktop folder (`SALES DASHBOARD`) and paste them inside this cloned folder.
6. Open **GitHub Desktop** again. It will automatically show a list of your files on the left side!
7. At the bottom-left corner, type a title like `"Upload project files"` in the Summary box.
8. Click the blue **Commit to main** button.
9. Click the **Push origin** button at the top.
10. Go to your GitHub website page, refresh it, and you will see all your files online! 🚀

---

This is your complete roadmap, Sai! Take it one click at a time. Let me know if you run into any issues on any specific step!
