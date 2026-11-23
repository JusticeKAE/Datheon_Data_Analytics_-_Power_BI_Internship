# **Task 1: Superstore Retail Sales & Profitability Exploratory Data Analysis (Python)**

Documentation and executive summary for the exploratory data analysis of the Superstore retail sales dataset.

# **Overview**

This module completes Task 1 of the Datheon Data Analytics & Power BI Internship.

The core objective of this project is to clean, explore, and visualize the Superstore Sales dataset (`superstore_sales.csv`) using Python. The analysis targets key commercial drivers including overall revenue generation, monthly seasonality, product category and regional profitability, and discount sensitivity. The evaluation culminates in five actionable executive recommendations designed to optimize pricing strategies and operational margins.

# **Folder Structure & Files**

* **`01_Superstore_Python_EDA.ipynb`** — Complete Jupyter Notebook containing end-to-end data cleaning, feature engineering, exploratory aggregations, visual data charts, and detailed executive findings.  
* **`superstore_sales.csv`** — Raw Superstore retail dataset comprising 10,800 raw rows, which cleans down to 9,994 validated order line items spanning January 2015 to December 2018\.  
* **`01_monthly_sales_velocity.png`** — Time-series line chart tracking monthly sales volume and profit velocity across the 2015–2018 operational period.  
* **`02_discount_vs_profit.png`** — Scatter plot featuring a linear regression trendline analyzing line-item discount rate impact on net profit across product categories.  
* **`03_category_region_performance.png`** — Side-by-side grouped bar charts comparing total sales and net profit broken down by product category and geographic region.  
* **`README.md`** — Comprehensive documentation summarizing project methodology, key performance indicators, and strategic business takeaways.

# **Tools & Libraries Used**

* **Python 3**: Core execution environment.  
* **Pandas & NumPy**: Utilized for structural data cleaning, missing value imputation, datetime parsing, custom feature engineering, and multi-dimensional `groupby` aggregations.  
* **Matplotlib & Seaborn**: Employed for generating statistical visualizations, regression trend analyses, and publication-ready executive charts.  
* **Jupyter Notebook / VS Code**: Integrated development environment used for code execution and workflow documentation.

# **Data Cleaning & Feature Engineering Pipeline**

1. **Metadata Row Removal**: Stripped 806 appended non-order lookup rows (People and Returns lookup tables located beneath row 9,994 where `Order Date` and `Sales` were null) to isolate the 9,994 valid order line-item records.  
2. **Missing Value Imputation**: Identified and imputed 11 missing `Postal Code` entries for Burlington, Vermont using the standard 5-digit ZIP code (`05401`), bringing total dataset missing values to zero.  
3. **Type Standardization & Date Parsing**: Converted `Row ID` and `Quantity` to integer data types. Parsed `Order Date` and `Ship Date` from raw strings into native `datetime64` format for time-series processing.  
4. **Engineered Features**:  
   * **`Order_Year`**, **`Order_Month`**, **`Month_Name`**, and **`Year-Month`**: Extracted temporal components to facilitate seasonality tracking and longitudinal trend analysis.  
   * **`Shipping_Days`**: Calculated operational fulfillment lead time by evaluating the net difference between `Ship Date` and `Order Date`.  
   * **`Profit_Margin_Pct`**: Derived line-item profitability ratio (`Profit / Sales`).  
   * **`Discount_Tier`**: Segmented continuous discount rates into four distinct operational pricing brackets: **0% (No Discount)**, **1%–20%**, **21%–40%**, and **\>40%**.

# **Headline Executive KPIs (2015–2018)**

| Metric | Value |
| :---- | :---- |
| **Total Revenue** | \$2,297,200.86 |
| **Total Profit** | \$286,397.02 |
| **Overall Profit Margin** | 12.47% |
| **Total Unique Orders** | 5,009 |
| **Total Unique Customers** | 793 |
| **Total Units Sold** | 37,873 |

# **Key Business Findings & Strategic Recommendations**

## **1\. Aggressive Discounting Above 20% Erodes Unit Economics**

The line-item discount rate exhibits a clear negative correlation with profitability (**r \= \-0.22**). Line items sold at a **0% discount** generate **\$320,988 in profit** (**29.51% profit margin**) with zero loss-making transactions. Conversely, discounts falling within the **21%–40% tier** cause average margins to collapse to **\-15.30%** (**90.22% of items sold at a net loss**). Deep markdowns exceeding **40%** result in severe margin degradation to \-77.40%, representing a aggregate net loss of \-\$99,559 across 933 line items.

* **Recommendation**: Implement an automated **20% maximum discount ceiling** within the point-of-sale system. Any exceptional promotional markdown exceeding 20% must require formal Regional Director authorization.

## **2\. Furniture Generates High Revenue with Near-Zero Net Margin**

Top-line revenue is relatively balanced across all three product categories: Technology (\$836.2K), Furniture (\$742.0K), and Office Supplies (**\$719.0K**). However, profitability diverges sharply. Technology accounts for **50.79% of total net profit** (**\$145.5K**, **17.40% margin**), whereas Furniture contributes only **6.44% of net profit** (**\$18.5K**, **2.49% margin**). Significant losses within Furniture are concentrated in **Tables** (**\-\$17,725** profit; **\-8.56% margin**) and Bookcases (-\$3,473 profit; \-3.02% margin), driven by steep average discounting (26.1% and 21.1% respectively) alongside high freight overhead.

* **Recommendation**: Re-price the Tables and Bookcases sub-categories, eliminate default discounting on bulky items, and introduce minimum order value thresholds to absorb freight overhead.

## **3\. Late-Year Seasonality Concentrates Revenue in September–December**

Order volume and sales velocity experience a sharp surge during the final four months of the calendar year. **November** (**\$352.5K**, **15.34%** of annual sales), **December** (**\$325.3K**, **14.16%**), and **September** (**\$307.6K**, **13.39%**) collectively generate **42.89% of total annual revenue**. By contrast, Q1 performance remains sluggish, with **February** (**\$59.8K**, **2.60%**) and **January** (**\$94.9K**, **4.13%**) recording the lowest sales volumes.

* Recommendation: Front-load inventory procurement and supply chain staging into August to prevent Q4 fulfillment bottlenecks, and launch targeted B2B commercial restocking campaigns in Q1 to smooth out annual cash flow.

## **4\. Central Region Margin Compression Mirrors Discount Overuse**

The **West region** leads overall corporate performance in both sales (**\$725.5K**) and profit margin (14.94%, \$108.4K profit), while maintaining the lowest average discount rate (**10.93%**). In contrast, the **Central region** records the lowest profit margin across the organization (**7.92%**, **\$39.7K profit** on **\$501.2K sales**)—yielding less absolute profit than the smaller South region (\$46.7K profit). This regional margin compression is directly attributable to an un-capped 24.04% average discount rate across Central territory transactions.

* **Recommendation**: Align Central region promotional authorization policies with the disciplined pricing structures established in the West and East territories.

## **5\. Consumer Leads Volume, While Corporate & Home Office Yield Higher Margins**

The Consumer segment drives the majority of transaction volume, contributing 50.56% of total revenue (\$1.16M across 2,586 orders) at an 11.55% profit margin. However, commercial segments deliver superior profitability per dollar sold: Home Office generates **\$429.7K** at a **14.03% profit margin**, while **Corporate** yields **\$706.1K** at a **13.03% profit margin**.

* **Recommendation**: Expand direct B2B sales acquisition efforts targeting Corporate and Home Office accounts, while tightening margin controls and discount thresholds on B2C Consumer promotions.

# **How to Run Locally**

1. **Environment Setup**: Ensure Python 3 and the required dependencies (`pandas`, `numpy`, `matplotlib`, `seaborn`, `jupyter`) are installed in your environment.  
2. **Directory Placement**: Download and place `superstore_sales.csv` and `01_Superstore_Python_EDA.ipynb` into the same root working directory.  
3. **Execution**: Open `01_Superstore_Python_EDA.ipynb` in Jupyter Notebook or VS Code, select your active Python kernel, and execute **Restart & Run All** to re-generate all dynamic data tables and high-resolution chart output files (`.png`).

