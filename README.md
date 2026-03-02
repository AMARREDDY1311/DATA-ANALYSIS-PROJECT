# 📊 SQL Data Analysis — Adventure Works Data Warehouse

> End-to-end exploratory and business analysis of a retail cycling company's sales, customer, and product data — built on a production SQL Server data warehouse using the Medallion Architecture (Bronze → Silver → Gold).

---

## 📌 Project Overview

This project answers the most critical business questions a company needs to understand its growth, customer base, and product performance. All analysis is written in **T-SQL** against a clean Gold layer Star Schema, covering **$29.3M in sales**, **18,484 customers**, and **27,659 orders** across a **37-month trading window (Dec 2010 – Jan 2014)**.

---

## 🗂️ Table of Contents

1. [Business Questions Answered](#1-business-questions-answered)
2. [Data Scope](#2-data-scope)
3. [Key Metrics Snapshot](#3-key-metrics-snapshot)
4. [Analysis & Results](#4-analysis--results)
   - [Magnitude Analysis — Who, What, Where](#magnitude-analysis)
   - [Product Rankings — Best & Worst Performers](#product-rankings)
   - [Sales Trends — Growth Over Time](#sales-trends)
   - [Cumulative Performance](#cumulative-performance)
   - [Year-over-Year Product Performance](#year-over-year-product-performance)
   - [Customer Segmentation](#customer-segmentation)
   - [Revenue by Category (Part-to-Whole)](#revenue-by-category)
5. [Recommendations](#5-recommendations)
6. [SQL Techniques Used](#6-sql-techniques-used)

---

## 1. Business Questions Answered

| # | Business Question |
|---|-------------------|
| 1 | What is the overall scale and health of the business? |
| 2 | Which countries and demographics drive the most customers? |
| 3 | Which product categories and individual products generate the most revenue? |
| 4 | Which products are underperforming and need attention? |
| 5 | How has revenue trended month-over-month and year-over-year? |
| 6 | How is revenue accumulating — is the business growing? |
| 7 | How do products perform relative to their own average and the prior year? |
| 8 | Which customers are VIP, Regular, or New — and how many of each? |
| 9 | What share of total revenue does each category represent? |

---

## 2. Data Scope

| Attribute | Value |
|-----------|-------|
| **Date Range** | December 29, 2010 → January 28, 2014 |
| **Trading Window** | 37 months |
| **Source Systems** | CRM (customers, products, sales) + ERP (demographics, locations) |
| **Gold Layer Tables** | `gold.fact_sales`, `gold.dim_customers`, `gold.dim_products` |
| **Customer Age Range** | 40 years old (youngest) → 110 years old (oldest) |

---

## 3. Key Metrics Snapshot

| Metric | Value |
|--------|-------|
| 💰 Total Revenue | **$29,356,250** |
| 📦 Total Orders | **27,659** |
| 🛒 Total Units Sold | **60,423** |
| 💵 Average Unit Price | **$486** |
| 👥 Total Customers | **18,484** |
| 🛍️ Customers Who Ordered | **18,484** |
| 🏷️ Total Products | **295** |

---

## 4. Analysis & Results

---

### Magnitude Analysis

**Purpose:** Understand the distribution of customers, products, and sales across key dimensions — countries, gender, and product categories.

#### 🌍 Customers by Country

| Country | Customers | Share |
|---------|-----------|-------|
| 🇺🇸 United States | 7,482 | 40.5% |
| 🇦🇺 Australia | 3,591 | 19.4% |
| 🇬🇧 United Kingdom | 1,913 | 10.4% |
| 🇫🇷 France | 1,810 | 9.8% |
| 🇩🇪 Germany | 1,780 | 9.6% |
| 🇨🇦 Canada | 1,571 | 8.5% |
| Unknown | 337 | 1.8% |

> 🔍 **Insight:** The US alone accounts for 40% of the customer base, making it the dominant market. Australia punches above its weight at nearly 20%.

---

#### 👤 Customers by Gender

| Gender | Customers |
|--------|-----------|
| Male | 9,341 |
| Female | 9,128 |
| Unknown | 15 |

> 🔍 **Insight:** The gender split is near-perfect (50.5% male / 49.4% female) — no significant gender skew in the customer base.

---

#### 🏷️ Products by Category & Average Cost

| Category | Products | Avg Cost |
|----------|----------|----------|
| Components | 127 | $264 |
| Bikes | 97 | $949 |
| Clothing | 35 | $24 |
| Accessories | 29 | $13 |

> 🔍 **Insight:** Bikes have the highest unit cost at $949 — making them the key revenue driver despite fewer SKUs than Components.

---

#### 🗺️ Units Sold by Country

| Country | Units Sold |
|---------|------------|
| United States | 20,481 |
| Australia | 13,346 |
| Canada | 7,630 |
| United Kingdom | 6,910 |
| Germany | 5,626 |
| France | 5,559 |

> 🔍 **Insight:** Canada ranks 3rd in units sold despite ranking 6th in customer count — suggesting Canadian customers buy more per person than other markets.

---

### Product Rankings

**Purpose:** Identify top-performing and bottom-performing products to inform stock, marketing, and discontinuation decisions.

#### 🏆 Top 5 Products by Revenue

| Rank | Product | Revenue |
|------|---------|---------|
| 1 | Mountain-200 Black, Size 46 | $1,373,454 |
| 2 | Mountain-200 Black, Size 42 | $1,363,128 |
| 3 | Mountain-200 Silver, Size 38 | $1,339,394 |
| 4 | Mountain-200 Silver, Size 46 | $1,301,029 |
| 5 | Mountain-200 Black, Size 38 | $1,294,854 |

> 🔍 **Insight:** The entire top 5 is dominated by the **Mountain-200** model — this single product line is a revenue pillar for the business.

---

#### ⚠️ Bottom 5 Products by Revenue

| Rank | Product | Revenue |
|------|---------|---------|
| 1 | Racing Socks, Size L | $2,430 |
| 2 | Racing Socks, Size M | $2,682 |
| 3 | Patch Kit / 8 Patches | $6,382 |
| 4 | Bike Wash - Dissolver | $7,272 |
| 5 | Touring Tire Tube | $7,440 |

> 🔍 **Insight:** The lowest 5 products combined generated less than $26,000 — less than 0.1% of total revenue. These are candidates for discontinuation or promotional bundling.

---

#### 👑 Top 10 Customers by Revenue

| Customer | Revenue |
|----------|---------|
| Kaitlyn Henderson | $13,294 |
| Nichole Nara | $13,294 |
| Margaret He | $13,268 |
| Randall Dominguez | $13,265 |
| Adriana Gonzalez | $13,242 |
| Rosa Hu | $13,215 |
| Brandi Gill | $13,195 |
| Brad She | $13,172 |
| Francisco Sara | $13,164 |
| Maurice Shan | $12,914 |

> 🔍 **Insight:** The top customers are remarkably close in revenue ($13,164–$13,294) — indicating no single customer dominates, which is a healthy sign. The business is **not over-reliant on any one client**.

---

### Sales Trends

**Purpose:** Track revenue and volume changes over time to identify growth trends, seasonality, and anomalies.

#### 📅 Annual Revenue Summary

| Year | Revenue | Customers | Notes |
|------|---------|-----------|-------|
| 2010 | $43,419 | 14 | Partial year (Dec only) |
| 2011 | $7,075,088 | ~222/month | Stable growth |
| 2012 | $5,842,231 | ~300/month | Slight dip vs 2011 |
| 2013 | $16,344,878 | ~1,800/month | **Explosive growth** |
| 2014 | $45,642 | 834 | Partial year (Jan only) |

> 🔍 **Insight:** 2013 was a breakout year — revenue **increased by 180% vs 2012**. Monthly customer volume jumped from ~300 in 2012 to ~1,800+ in 2013, suggesting a major expansion event (new market, product launch, or channel growth).

#### 📈 Monthly Revenue Highlights

| Month | Revenue | Active Customers |
|-------|---------|------------------|
| Dec 2013 | $1,874,128 | 2,133 | ← Peak month |
| Nov 2013 | $1,780,688 | 2,036 | |
| Oct 2013 | $1,673,261 | 2,073 | |
| Jun 2013 | $1,642,948 | 1,948 | |
| Jun 2011 | $737,793 | 230 | ← 2011 peak |

> 🔍 **Insight:** Revenue peaks consistently appear in **June and Q4 (Oct–Dec)** — pointing to clear seasonality aligned with summer cycling season and holiday gifting.

---

### Cumulative Performance

**Purpose:** Show the running total of revenue to demonstrate long-term growth trajectory.

| Year | Annual Revenue | Cumulative Revenue | Avg Price |
|------|---------------|-------------------|-----------|
| 2010 | $43,419 | $43,419 | $3,101 |
| 2011 | $7,075,088 | $7,118,507 | $3,146 |
| 2012 | $5,842,231 | $12,960,738 | $2,670 |
| 2013 | $16,344,878 | $29,305,616 | $2,080 |
| 2014 | $45,642 | $29,351,258 | $1,668 |

> 🔍 **Insight:** **56% of all revenue was generated in 2013 alone**. The declining average price trend (from $3,146 to $1,668) suggests a strategic shift toward volume — more customers buying lower-cost products alongside the premium bikes.

---

### Year-over-Year Product Performance

**Purpose:** Compare each product's annual sales against its own historical average and prior year to identify which are growing, declining, or consistent.

**Method:** `LAG()` window function for prior year comparison + `AVG() OVER (PARTITION BY product_name)` for historical benchmark.

#### Key Findings

| Pattern | Example | Signal |
|---------|---------|--------|
| Consistent growth every year | Mountain-200 Black-46, Road-250 Black-44 | Core product — protect and invest |
| Strong 2013, sharp 2014 drop | Most accessories & clothing | Likely partial-year 2014 data effect |
| Only appeared in 2011 | Road-150 Red (all sizes), Mountain-100 | Discontinued or phased out |
| New in 2013 only | Mountain-500, Touring-3000, Road-750 | New launches — monitor closely |

> 🔍 **Insight:** The **Mountain-200** series showed unbroken year-over-year growth across all sizes — confirming it as the business's most reliable product line. Products that only appeared in 2011 (Road-150, Mountain-100) appear to have been phased out by 2012.

---

### Customer Segmentation

**Purpose:** Group customers by spend behaviour and purchase history to identify where to focus retention and acquisition efforts.

**Segmentation Rules:**
- **VIP** — 12+ months purchase history AND total spend > $5,000
- **Regular** — 12+ months purchase history AND spend ≤ $5,000
- **New** — Purchase history < 12 months

| Segment | Customers | Share |
|---------|-----------|-------|
| 🆕 New | 14,631 | **79.1%** |
| 🔄 Regular | 2,198 | 11.9% |
| 👑 VIP | 1,655 | 9.0% |

> 🔍 **Insight:** Nearly **4 in 5 customers are classified as New** — meaning either the business is in heavy acquisition mode, or retention is a serious problem. The 2013 growth spike likely brought in a large wave of new, short-tenure customers who haven't yet built purchase history.

---

### Revenue by Category

**Purpose:** Understand which product categories drive the business — and which are peripheral.

| Category | Revenue | Share of Total |
|----------|---------|----------------|
| 🚲 Bikes | $28,316,272 | **96.46%** |
| 🎒 Accessories | $700,262 | 2.39% |
| 👕 Clothing | $339,716 | 1.16% |

> 🔍 **Insight:** Bikes generate **96.5% of all revenue**. Accessories and Clothing together represent just 3.5%. This extreme concentration creates both a strength (clear focus) and a risk (vulnerability to any disruption in the bike market).

---

## 5. Recommendations

### 🎯 Double Down on the Mountain-200

The Mountain-200 series is the single most important product in the portfolio. It dominates the top 5 revenue rankings across multiple sizes. Prioritise stock availability, marketing spend, and product development around this line.

---

### 🔄 Urgently Address the New Customer Retention Problem

79% of customers are classified as New — and with only 9% reaching VIP status, the conversion funnel is leaking badly. Implementing post-purchase email flows, loyalty incentives, and re-engagement campaigns targeting the 14,631 New customers should be the highest-priority CRM action.

---

### 🌏 Invest in the Australian Market

Australia is the 2nd largest market by customer count and units sold, yet is likely underserved relative to the US. With 3,591 customers and 13,346 units sold, it represents a high-growth opportunity with localised marketing and potential regional stock positioning.

---

### 📦 Review or Bundle Underperforming Products

Racing Socks, Patch Kits, and Bike Wash products collectively generated under $26,000 across 37 months. These should be reviewed for discontinuation, bundled as add-ons at checkout alongside high-value bike purchases, or repriced to drive volume.

---

### 🗓️ Plan for Seasonality

June and Q4 (October–December) consistently represent revenue peaks. Marketing budgets, inventory procurement, and staffing should align to these periods. A targeted Q4 push with the Mountain-200 range could maximise revenue concentration at the highest-demand window.

---

### 📉 Investigate the 2012 Revenue Dip

2012 revenue ($5.84M) was lower than 2011 ($7.07M). Before attributing 2013's growth to strategy, it's worth understanding what caused the 2012 decline — whether that was product discontinuation (Road-150, Mountain-100 phased out), a market contraction, or a data issue.

---

### 🎯 Replicate Whatever Caused 2013

2013 drove 56% of total revenue and saw customer volume grow 6x from 2012 levels. Understanding the root cause — whether a new product launch, a new sales channel, geographic expansion, or pricing change — is critical. Replicating that trigger is the clearest path to sustained growth.

---

## 6. SQL Techniques Used

| Technique | Applied In |
|-----------|------------|
| `MIN()`, `MAX()`, `DATEDIFF()` | Date range and customer age exploration |
| `COUNT()`, `SUM()`, `AVG()` | Key business metrics snapshot |
| `GROUP BY`, `ORDER BY` | Magnitude analysis across all dimensions |
| `TOP N` | Simple product and customer ranking |
| `RANK()`, `DENSE_RANK()`, `ROW_NUMBER()` | Window-based flexible ranking |
| `LAG()` | Year-over-year product performance comparison |
| `AVG() OVER (PARTITION BY ...)` | Per-product historical benchmark |
| `SUM() OVER (ORDER BY ...)` | Running/cumulative revenue totals |
| `DATEPART()`, `DATETRUNC()`, `FORMAT()` | Time-series grouping by year and month |
| `CASE WHEN` | Customer and product segmentation logic |
| `CTE (WITH ...)` | Multi-step segmentation and ranking queries |
| `CAST()` | Safe numeric division for percentage calculations |

---

## 🧰 Tech Stack

![SQL Server](https://img.shields.io/badge/SQL%20Server-CC2927?style=flat&logo=microsoftsqlserver&logoColor=white)
![T-SQL](https://img.shields.io/badge/T--SQL-0078D4?style=flat&logo=microsoft&logoColor=white)
![Git](https://img.shields.io/badge/Git-F05032?style=flat&logo=git&logoColor=white)

- **Database:** Microsoft SQL Server
- **Language:** SQL
- **Layer Queried:** Gold (Star Schema — `fact_sales`, `dim_customers`, `dim_products`)
- **Methodology:** Exploratory Data Analysis → Business Insight → Recommendations

---

## 📁 Repository Structure

```
sql-analysis/
├── 01_date_and_measures_exploration.sql   # Temporal boundaries + key metric snapshot
├── 02_magnitude_analysis.sql              # Volume by country, gender, category
├── 03_ranking_analysis.sql                # Top/bottom products and customers
├── 04_change_over_time.sql                # Monthly and yearly revenue trends
├── 05_cumulative_analysis.sql             # Running totals and moving averages
├── 06_performance_analysis.sql            # YoY and vs-average product comparison
├── 07_segmentation_analysis.sql           # Product cost tiers + customer VIP/Regular/New
├── 08_part_to_whole.sql                   # Category revenue share
└── README.md
```

---

*Analysis based on 37 months of transactional data from a retail cycling company — Dec 2010 to Jan 2014.*
