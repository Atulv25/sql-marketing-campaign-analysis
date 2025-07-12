# 📊 Campaign Performance Tracker - SQL Project

## 🧠 Project Overview

**Project Title:** Campaign Performance Tracker  
**Level:** Intermediate  
**Tech Stack:** SQL (MySQL), CSV  
**Dataset:** `big_campaigns.csv`, `big_ad_performance_800.csv`

This SQL project evaluates the performance of digital marketing campaigns using structured queries. It calculates key metrics such as Click-Through Rate (CTR), Cost Per Acquisition (CPA), and Budget Utilization across multiple channels and campaigns. Ideal for aspiring data analysts looking to showcase real-world SQL skills.

---

## 🎯 Objectives

- 🗄 Create campaign & performance tables from CSV data
- 🧹 Perform data exploration & handle potential issues
- 📊 Analyze performance via SQL (CTR, CPA, Spend, etc.)
- 🔍 Derive insights from campaign data

---

## 📁 Dataset Description

### `big_campaigns.csv`
| Column Name    | Description                    |
|----------------|--------------------------------|
| campaign_id    | Unique ID of the campaign      |
| campaign_name  | Name of the campaign           |
| channel        | Platform (e.g., Instagram)     |
| start_date     | Campaign start date            |
| end_date       | Campaign end date              |
| budget         | Total campaign budget          |

### `big_ad_performance_800.csv`
| Column Name    | Description                          |
|----------------|--------------------------------------|
| ad_id          | Unique ad ID                         |
| campaign_id    | Foreign key to campaign              |
| impressions    | Number of ad views                   |
| clicks         | Number of ad clicks                  |
| conversions    | Number of successful conversions     |
| cost           | Total cost for that ad               |
| date           | Date of ad performance               |

---

## 🛠 SQL Table Structure

```sql
-- Campaign Table
CREATE TABLE big_campaigns (
  campaign_id INT PRIMARY KEY,
  campaign_name VARCHAR(255),
  channel VARCHAR(50),
  start_date DATE,
  end_date DATE,
  budget FLOAT
);

-- Ad Performance Table
CREATE TABLE big_ad_performance_800 (
  ad_id INT PRIMARY KEY,
  campaign_id INT,
  impressions INT,
  clicks INT,
  conversions INT,
  cost FLOAT,
  date DATE
);


## Data Analysis & Findings
The following SQL queries were developed to answer specific business questions related to digital marketing performance:

1. What is the Click-Through Rate (CTR) for each campaign?

SELECT 
  c.campaign_name,
  ROUND(SUM(a.clicks) * 100.0 / NULLIF(SUM(a.impressions), 0), 2) AS ctr_percent
FROM big_campaigns AS c
JOIN big_ad_performance_800 AS a ON c.campaign_id = a.campaign_id
GROUP BY c.campaign_name;

2. What is the Cost Per Acquisition (CPA) for each campaign?

SELECT 
  c.campaign_name,
  ROUND(SUM(a.cost) / NULLIF(SUM(a.conversions), 0), 2) AS cpa
FROM big_campaigns AS c
JOIN big_ad_performance_800 AS a ON c.campaign_id = a.campaign_id
GROUP BY c.campaign_name;

3. How much budget has each campaign used, and what’s the utilization percentage?

SELECT 
  c.campaign_name,
  c.budget,
  ROUND(SUM(a.cost), 2) AS total_spent,
  ROUND(SUM(a.cost) * 100.0 / NULLIF(c.budget, 0), 2) AS budget_utilization_percent
FROM big_campaigns AS c
JOIN big_ad_performance_800 AS a ON c.campaign_id = a.campaign_id
GROUP BY c.campaign_name, c.budget;

4. What is the daily ad spend trend across all campaigns?

SELECT 
  a.date,
  ROUND(SUM(a.cost), 2) AS daily_spend
FROM big_ad_performance_800 AS a
GROUP BY a.date
ORDER BY a.date;

5. Which channel has the highest conversion rate (conversions per click)?

SELECT 
  c.channel,
  ROUND(SUM(a.conversions) * 100.0 / NULLIF(SUM(a.clicks), 0), 2) AS conversion_rate
FROM big_campaigns AS c
JOIN big_ad_performance_800 AS a ON c.campaign_id = a.campaign_id
GROUP BY c.channel
ORDER BY conversion_rate DESC;

6. Which campaigns are underperforming (CPA greater than ₹500)?

SELECT 
  c.campaign_name,
  ROUND(SUM(a.cost) / NULLIF(SUM(a.conversions), 0), 2) AS cpa
FROM big_campaigns AS c
JOIN big_ad_performance_800 AS a ON c.campaign_id = a.campaign_id
GROUP BY c.campaign_name
HAVING cpa > 500;

7. Which campaigns achieved the highest number of conversions and what were their CTRs?

SELECT 
  c.campaign_name,
  SUM(a.conversions) AS total_conversions,
  ROUND(SUM(a.clicks) * 100.0 / NULLIF(SUM(a.impressions), 0), 2) AS ctr
FROM big_campaigns AS c
JOIN big_ad_performance_800 AS a ON c.campaign_id = a.campaign_id
GROUP BY c.campaign_name
ORDER BY total_conversions DESC, ctr DESC;

8. How does each marketing channel perform in terms of CTR and CPA?
SELECT 
  c.channel,
  ROUND(SUM(a.clicks)*100.0 / NULLIF(SUM(a.impressions), 0), 2) AS ctr,
  ROUND(SUM(a.cost) / NULLIF(SUM(a.conversions), 0), 2) AS cpa
FROM big_campaigns AS c
JOIN big_ad_performance_800 AS a ON c.campaign_id = a.campaign_id
GROUP BY c.channel
ORDER BY ctr DESC;



📊 Insights
🔝 Instagram was the best-performing channel (highest CTR & lowest CPA)

💰 Year End Sale was the most successful campaign

📉 No budget overspend across campaigns

🔍 Channel selection impacts efficiency significantly

🚀 Future Enhancements
Include revenue column to compute ROI

Add Power BI or Excel dashboards

Use time series analysis to predict campaign trends
