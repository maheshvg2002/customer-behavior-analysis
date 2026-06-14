# Retail Customer Shopping Behavior Analysis

## 📌 Project Overview
This repository contains an end-to-end data analytics portfolio project designed to simulate real-world corporate workflows. The project transforms raw, uncleaned customer shopping data into actionable business intelligence by executing a full analytical lifecycle: data manipulation and feature engineering in Python, deep relational querying in MySQL, and executive-level KPI dashboard tracking in Power BI.

The core objective is to identify shopping trends across different demographics, evaluate the true impact of promotional discounts, and uncover customer loyalty patterns to optimize retail marketing and product strategies.

---

## 🛠️ Tech Stack & Tools Used
- **Data Cleansing & Transformation:** Python 3 (Pandas, Jupyter Notebook)
- **Database Management & Querying:** MySQL Server / MySQL Workbench
- **Database Connectivity:** SQLAlchemy & PyMySQL
- **Data Visualization & Business Intelligence:** Power BI Desktop

---

## 📁 Dataset Architecture
The dataset captures fine-grained customer profiles and transaction behavior. The features utilized include:
- **Demographics:** `customer_id` (Primary Key), `age`, `gender`, `location`
- **Purchase Details:** `item_purchased`, `category`, `purchase_amount`, `season`
- **Behavioral Metrics:** `review_rating`, `subscription_status`, `previous_purchases`, `frequency_of_purchases`, `shipping_type`, `discount_applied`

---

## 🔄 Project Pipeline & Implementation

### 1. Data Cleaning & Feature Engineering (Python)
The raw data was audited and prepared inside a Jupyter Notebook to ensure integrity before relational migration:
- **Smart Imputation:** Identified missing values in the review rating column. Instead of a blanket median, null values were dynamically imputed using the **median review rating specific to each product category** to preserve natural data distributions.
- **Naming Standardization:** Converted mixed-case and space-separated column names into clean, lower-case `snake_case` for seamless SQL referencing.
- **Feature Engineering:** - Segmented continuous ages into descriptive bins (`age_group`) using quantile-based categorization (`pd.qcut`).
  - Mapped textual shopping frequencies (e.g., Weekly, Monthly) into numerical columns representing exact intervals (`purchase_frequency_days`).
- **Redundancy Elimination:** Evaluated tracking columns and dropped overlapping attributes carrying identical information.

### 2. Relational Database Analytics (MySQL)
Using `SQLAlchemy` and `PyMySQL`, the processed data frame was loaded directly into a target MySQL database schema. Advanced SQL scripts were engineered to answer critical business inquiries:
- **Demographic Splits:** Aggregated exact total revenue segments divided strictly by customer gender.
- **Behavior Isolation:** Implemented subqueries to identify high-spending customers who utilize discount codes but still exceed the historical average order value.
- **Window Functions:** Utilized `ROW_NUMBER() OVER (PARTITION BY category ORDER BY ...)` to isolate and rank the top 3 highest-selling products nested within every individual retail category.
- **Customer Segmentation:** Wrote conditional `CASE` statements inside Common Table Expressions (CTEs) to categorize users into `New`, `Returning`, and `Loyal` segments based on aggregate transactional history.

### 3. Dynamic Executive Dashboard (Power BI)
A fully interactive semantic reporting layer was built by connecting Power BI directly to the local MySQL instance:
- **KPI Metrics:** Formatted custom DAX measures to cleanly display high-level cards tracking total unique shoppers, average ticket size, and average product satisfaction ratings.
- **Core Visuals:** Modeled clean column, bar, and donut charts highlighting revenue distribution against product categories, transaction volume, and age segments.
- **Interactive Filtering:** Deployed responsive slice filters across demographics (Gender, Age) and operations (Shipping Type, Subscription Status) to empower immediate stakeholder drill-downs.

---

## 🚀 Key Business Findings & Recommendations
- **Subscription Conversion Window:** Data reveals that non-subscribed customers buy items at an identical average spend value compared to subscribed members, though they form a larger portion of total revenue. This indicates a massive opportunity to design targeted conversion funnels.
- **Fulfillment Opportunities:** Transactions leveraging Express Shipping yield a higher average order size compared to Standard shipping paths, signaling that premium delivery offerings can successfully drive higher basket values.
- **Core Target Demographic:** The Young Adult cohort consistently generates the strongest overall revenue stream, making them the primary group for high-margin promotional campaigns.
