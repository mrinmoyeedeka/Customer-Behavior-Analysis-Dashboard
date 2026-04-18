# Customer Behavior Analysis Dashboard

## Project Overview

Understanding customer behavior is critical for improving marketing strategies, increasing revenue, and enhancing customer retention.

This project analyzes customer shopping behavior using **Python, SQL, and PostgreSQL** to uncover insights about purchasing patterns, product performance, and customer segments.

The workflow demonstrates a typical **end-to-end data analytics process**, including data cleaning, feature engineering, database integration, and answering business-driven analytical questions.

---

## Business Objectives

This project answers several key business questions:

* What is the revenue contribution from **male vs female customers**?
* Do **discounts increase customer spending**?
* Which products have the **highest customer satisfaction ratings**?
* Do **subscribed customers spend more** than non-subscribers?
* Which products are **most frequently purchased within each category**?
* What percentage of purchases occur **with discounts applied**?
* How can customers be segmented into **New, Returning, and Loyal groups**?

These insights help businesses optimize marketing strategies, promotions, and product offerings.

---

## Dataset

The dataset contains customer shopping activity including:

* Customer demographics (Age, Gender)
* Product category and item purchased
* Purchase amount
* Discount usage
* Shipping type
* Subscription status
* Review ratings
* Purchase frequency

---

## Tech Stack

| Tool                 | Purpose                               |
| -------------------- | ------------------------------------- |
| **Python (Pandas)**  | Data cleaning and feature engineering |
| **PostgreSQL**       | Data storage and querying             |
| **SQL**              | Business analysis queries             |
| **Jupyter Notebook** | Data exploration                      |
| **VS Code**          | Development environment               |

---

## Data Cleaning & Feature Engineering

Several preprocessing steps were performed to improve data quality and enable deeper analysis.

### Handling Missing Values

Missing review ratings were filled using the **median rating within each product category**, ensuring unbiased imputation.

### Standardizing Column Names

Column names were standardized to **lowercase with underscores** to improve consistency for SQL querying.

### Feature Engineering

**Age Groups**

Customers were segmented into quartile-based age groups:

* Young Adult
* Adult
* Middle-aged
* Senior

**Purchase Frequency (Days)**

Purchase frequency categories were converted into numerical values for better analytical flexibility.

Example mapping:

| Frequency   | Days |
| ----------- | ---- |
| Weekly      | 7    |
| Fortnightly | 14   |
| Monthly     | 30   |
| Quarterly   | 90   |
| Annually    | 365  |

### Data Consistency Checks

A validation step confirmed that:

```
discount_applied == promo_code_used
```

Since both fields contained identical information, the redundant column was removed.

---

## Data Pipeline

The cleaned dataset was loaded into **PostgreSQL** for scalable analysis.

Pipeline steps:

1. Load dataset with **Pandas**
2. Perform data cleaning and transformations
3. Connect to **PostgreSQL using SQLAlchemy**
4. Upload dataset as a database table
5. Run **analytical SQL queries**

---

## Key SQL Analyses

### Revenue by Gender

Evaluates how revenue is distributed between male and female customers.

### High-Value Discount Purchases

Identifies customers who used discounts but still spent **above average purchase amounts**, highlighting valuable promotional segments.

### Top Rated Products

Ranks products based on **average customer review ratings**.

### Shipping Impact on Spending

Compares average spending between **Standard and Express shipping** options.

### Subscription Revenue Impact

Measures whether **subscribed customers generate more revenue** than non-subscribers.

### Discount Usage Analysis

Calculates the **percentage of purchases with discounts applied** per product.

### Customer Segmentation

Customers are segmented into:

| Segment   | Definition              |
| --------- | ----------------------- |
| New       | 1 previous purchase     |
| Returning | 2–10 previous purchases |
| Loyal     | More than 10 purchases  |

This segmentation supports **targeted marketing strategies**.

### Top Products by Category

Uses **window functions** to identify the **top 3 most purchased products within each category**.

---

## Example SQL Query

```sql
SELECT item_purchased,
ROUND(100 * SUM(CASE WHEN discount_applied='Yes' THEN 1 ELSE 0 END)/COUNT(*),2) AS discount_rate
FROM customer
GROUP BY item_purchased
ORDER BY discount_rate DESC
LIMIT 5;
```

This query identifies products that rely most heavily on discounts to drive sales.

---

## Key Insights

* Certain products show **high discount dependency**, indicating price-sensitive demand.
* **Subscribed customers tend to generate higher revenue**, suggesting strong retention potential.
* Customer purchase patterns vary significantly across **product categories**.
* A small group of **loyal customers contributes disproportionately to revenue**.

---

## Project Structure

```
customer_behavior_analysis_dashboard
│
├── Customer analytics.ipynb
├── customer_behavior_basic business questions.sql
├── dataset
│
└── README.md
```

---

## Skills Demonstrated

* Data Cleaning
* Exploratory Data Analysis
* Feature Engineering
* SQL Analytics
* Window Functions
* Customer Segmentation
* Business Question Framing
* Data Pipeline Design

---

## Future Improvements

* Build an **interactive dashboard (Power BI / Tableau)**
* Implement **customer lifetime value (CLV) analysis**
* Apply **predictive models for purchase behavior**
* Add **cohort analysis for retention tracking**

---

### Dashboard Snapshot

![Dashboard](https://github.com/mrinmoyeedeka/customer_behavior_analysis_dashboard/blob/main/dashboard_snapshot.png)


---

## Author

**Mrinmoyee Deka**

Data Analyst focused on transforming raw data into actionable insights.

If you're interested in collaboration or discussing analytics opportunities, feel free to connect.
