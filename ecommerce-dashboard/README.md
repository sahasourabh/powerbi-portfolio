# 🛒 E-Commerce Sales Performance Dashboard

![Dashboard Preview](screenshots/overview.png)

---

## 📋 Project Overview

**Industry:** E-Commerce / Retail  
**Dashboard Type:** Sales Analytics  
**Pages:** 4 (Overview, Trends, Regional Analysis, Product Performance)  
**Data Source:** Kaggle Brazilian E-Commerce Dataset (anonymized)  
**Tools Used:** Power BI Desktop, DAX, Power Query

---

## 🎯 Business Problem

E-commerce businesses typically track sales across multiple channels (Amazon, Flipkart, Shopify, etc.) using disconnected Excel spreadsheets. Key challenges:

❌ No unified view of total revenue across channels  
❌ Manual effort to calculate YoY/MoM growth  
❌ Difficult to identify top-performing products or regions  
❌ Time-consuming monthly reporting process  

---

## ✅ Solution

Built a comprehensive, interactive Power BI dashboard that provides:

✔️ **Unified Revenue View:** Total sales across all channels in one place  
✔️ **Automated Time Intelligence:** YoY, MoM, QoQ growth calculated via DAX  
✔️ **Regional Insights:** Geographic breakdown with drill-through to city level  
✔️ **Product Performance:** Top/bottom N products with dynamic filtering  
✔️ **Self-Service:** Business users can slice/filter by date, region, category without IT help  

---

## 📊 Dashboard Pages

### Page 1: Executive Overview
![Overview](screenshots/overview.png)

**KPIs Displayed:**
- Total Revenue (current period)
- YoY Revenue Growth %
- Total Orders
- Average Order Value (AOV)
- Top 5 Products by Revenue

**Visuals:**
- KPI cards with trend indicators
- Revenue trend line chart (monthly)
- Revenue by region (map visual)

---

### Page 2: Sales Trends
![Sales Trends](screenshots/sales-trends.png)

**Analysis:**
- Monthly revenue trend with YoY comparison
- Revenue by category (bar chart)
- Orders vs Revenue dual-axis chart

---

### Page 3: Regional Analysis
![Regional Analysis](screenshots/regional-analysis.png)

**Features:**
- Revenue by state/region (filled map)
- Drill-through to city-level details
- Regional performance table with variance %

---

### Page 4: Product Performance
![Product Performance](screenshots/product-performance.png)

**Analysis:**
- Top 10 products by revenue (dynamic — can change N via slicer)
- Product category breakdown
- Product performance matrix (revenue vs order volume)

---

## 🧮 Key DAX Measures

### 1. YoY Revenue Growth
```dax
YoY Revenue Growth % = 
VAR CurrentRevenue = [Total Revenue]
VAR PreviousRevenue = CALCULATE([Total Revenue], SAMEPERIODLASTYEAR('Date'[Date]))
RETURN
DIVIDE(CurrentRevenue - PreviousRevenue, PreviousRevenue, 0)
```

### 2. Running Total Revenue
```dax
Running Total Revenue = 
CALCULATE(
    [Total Revenue],
    FILTER(
        ALL('Date'),
        'Date'[Date] <= MAX('Date'[Date])
    )
)
```

### 3. Average Order Value (AOV)
```dax
AOV = DIVIDE([Total Revenue], [Total Orders], 0)
```

### 4. Top N Products (Dynamic)
```dax
Top N Products = 
VAR SelectedN = SELECTEDVALUE('Top N Slicer'[N], 10)
RETURN
CALCULATE(
    [Total Revenue],
    TOPN(SelectedN, ALL(Products[ProductName]), [Total Revenue], DESC)
)
```

---

## 🗄️ Data Model

**Fact Table:**
- `Sales` (OrderID, ProductID, CustomerID, Date, Revenue, Quantity)

**Dimension Tables:**
- `Products` (ProductID, ProductName, Category, SubCategory)
- `Customers` (CustomerID, City, State, Region)
- `Date` (Date, Year, Quarter, Month, Week) — Calendar table

**Relationships:**
- Sales[ProductID] → Products[ProductID] (Many-to-One)
- Sales[CustomerID] → Customers[CustomerID] (Many-to-One)
- Sales[Date] → Date[Date] (Many-to-One)

**Schema:** Star Schema

---

## 📥 Data Source

**Dataset:** [Kaggle Brazilian E-Commerce Public Dataset](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)

**Data Preparation (Power Query):**
1. Loaded 5 CSV files (orders, order items, products, customers, geolocation)
2. Merged tables using inner joins on OrderID and ProductID
3. Removed null values and duplicates
4. Created calculated columns:
   - `Revenue = Quantity * Price`
   - `Order Year-Month` for time series
5. Created a Date dimension table using M code

---

## 🚀 How to Use This Dashboard

### Option 1: View Screenshots
Browse the `screenshots/` folder to see each dashboard page.

### Option 2: Download and Open in Power BI
1. Download `ecommerce-sales-dashboard.pbix`
2. Open with Power BI Desktop (free version works)
3. Explore the data model, DAX measures, and visualizations
4. Modify as needed for your own data

### Option 3: Connect Your Own Data
1. Open the .pbix file
2. Go to **Transform Data** (Power Query Editor)
3. Replace the data source with your own CSV/Excel/SQL data
4. Map the column names to match the existing schema
5. Refresh the data model

---

## 💡 Business Impact

**Before (Excel-based reporting):**
- 4–5 hours/month to manually create sales reports
- No interactivity — each new question requires a new report
- No historical trend analysis

**After (Power BI dashboard):**
- One-click refresh (takes 30 seconds)
- Self-service — business users explore data themselves
- Historical trends and YoY comparisons built-in
- **Time saved:** ~5 hours/month per user

---

## 🔧 Technical Details

**File Size:** ~8 MB  
**Data Rows:** ~100,000 sales transactions  
**Performance:** Optimized with:
- Proper star schema
- Integer keys for relationships
- DAX variables to reduce recalculation
- Aggregations where appropriate

**Compatibility:** Power BI Desktop (2023 or later recommended)

---

## 📸 Additional Screenshots

<details>
<summary>Click to expand all screenshots</summary>

![Overview](screenshots/overview.png)
![Sales Trends](screenshots/sales-trends.png)
![Regional Analysis](screenshots/regional-analysis.png)
![Product Performance](screenshots/product-performance.png)

</details>

---

## 📬 Questions or Feedback?

If you have questions about this dashboard or want a similar solution for your business:

📧 Email: [YOUR_EMAIL]  
💼 LinkedIn: [YOUR_LINKEDIN_URL]  
🟢 Fiverr: [YOUR_FIVERR_URL]

---

## ⭐ If you found this useful, please star the main repository!

[← Back to Portfolio](../)
