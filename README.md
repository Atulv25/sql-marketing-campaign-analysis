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
