# 🚲 BIKE SHOP – Revenue & Rider Analysis Dashboard

An interactive Power BI dashboard that delivers powerful insights into sales performance, rider behavior, seasonal trends, and profitability of a bike rental business.

---

## 📊 Dashboard Overview

This dashboard is designed to answer essential business questions such as:

- 🕒 **When are we making the most money?**
- 🌦️ **Which seasons are the most profitable?**
- 📉 **What are the trends in riders and profits over time?**
- 👥 **What types of riders are contributing most to revenue?**

---

## 📌 Key Metrics

- **🧍‍♂️ Total Riders:** `3M`
- **💰 Total Revenue:** `$15M`
- **📈 Total Profit:** `$15.14M`

---

## 🔍 Key Insights

### 🕒 When Are We Making Money?

- The most profitable hours are between **10 AM and 3 PM**, with noticeable spikes in **midday and early evening hours**.
- **Wednesdays and Fridays** show significantly higher revenue, suggesting peak customer engagement on these days.

> Tip: Focus marketing and staffing during these peak hours and days.

---

### 📆 KPI Over Time

A visual breakdown of monthly performance across two years:
- **Bar Chart:** Sum of Riders
- **Line Chart:** Average Profit

> Profits and rider count grow steadily from early 2021, peaking around **July–September 2022**.

---

### 🌦️ Revenue by Season

| Season | Revenue |
|--------|---------|
| Season 3 | $4.9M ✅ *(Highest)* |
| Season 2 | $4.2M |
| Season 4 | $3.9M |
| Season 1 | $2.2M ❌ *(Lowest)* |

> Season 3 (likely summer) drives the most business. Consider planning offers or expansion during this time.

---

### 👥 Riders Demographics

- **Registered Riders:** `81.17%`
- **Casual Riders:** `18.83%`

> The majority of revenue is driven by registered users. Loyalty programs and personalized offers may increase retention.

---

## 🗃️ Data Model & Query Logic

The underlying SQL query merges two years of data and calculates revenue and profit:

```sql
WITH cte AS (
    SELECT * FROM bike_share_yr_0
    UNION ALL
    SELECT * FROM bike_share_yr_1
)
SELECT 
    dteday, 
    season, 
    a.yr, 
    weekday, 
    hr, 
    rider_type, 
    riders, 
    price, 
    COGS,
    (riders * price) AS revenue,
    (riders * price - COGS) AS profit
FROM cte AS a
LEFT JOIN cost_table AS b 
ON a.yr = b.yr;
