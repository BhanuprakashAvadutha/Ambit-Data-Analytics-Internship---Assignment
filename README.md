# 📊 Ambit Analytics Dashboard Project

## 🧠 Objective

This project is built to deliver actionable business insights for Ambit using **Power BI** and **Excel**. It transforms and visualizes raw operational and revenue data to answer key business questions about client engagement, meeting effectiveness, time utilization, and revenue trends across dimensions like geography, client, and role.

---

## 📁 Dataset Overview

The data was extracted from the provided Excel workbook:
- `MIS Data` – Contains records of meetings, roles, and times.
- `Daily Revenue` – Contains daily revenue data per client.

A cleaned dataset was generated:  
📂 `Final_Cleaned_MIS_Revenue_Data.csv`

---

## 🧼 Data Cleaning & Transformation

Performed in **Python (Pandas)** and later used in **Power BI**:
- Parsed dates and calculated meeting durations.
- Standardized phone numbers using country codes.
- Merged daily revenue with meeting records by client and date.
- Removed malformed records (non-numeric phone/country codes, blank entries).
- Created new fields: `Meeting Duration (Hours)`, `Full Phone Number`.

---

## 📊 Power BI Dashboard Features

The dashboard is fully interactive and filters dynamically by date, client, role, and geography.

### ✅ Key Visualizations:
1. **📈 Yearly Revenue Trend by Client**
2. **⏱ Hours Spent by Sales Representatives per Client**
3. **⏱ Hours Spent by Analysts per Client**
4. **🌍 Country-wise Revenue Trends**

### 🧠 Business Questions Answered:

| Question | Method | Visual/Metric |
|---------|--------|----------------|
| 1. Analyst with highest leaves (Sep 2008–Mar 2013) | DAX table using calendar & EXCEPT | Table sorted by leave days |
| 2. Least revenue by Sales Rep (2020) | Measure filtering 2020 | Bar chart |
| 3. Country with most in-person meetings by Baki Hanma (Apr 2017–Mar 2019) | Visual filter on rep, date, and meeting type | Bar chart |
| 4. Client who preferred Zoom meetings the most | Count of Zoom meetings by client | Bar chart |
| 5. City with highest revenue (Jun 2022–Mar 2025) | Time-windowed revenue measure | Bar chart |

---

##🧮 Key DAX Measures Used

```dax
-- Meeting Duration Aggregation
TotalMeetingHours = SUM('Data'[Meeting Duration (Hours)])

-- Sales Rep Filtered Measure
SalesRepHours = CALCULATE(
    SUM('Data'[Meeting Duration (Hours)]),
    NOT(ISBLANK('Data'[Sales Representative]))
)

-- Analyst Filtered Measure
AnalystHours = CALCULATE(
    SUM('Data'[Meeting Duration (Hours)]),
    NOT(ISBLANK('Data'[Analyst]))
)

-- Time-windowed Revenue
Revenue_Jun22_Mar25 = CALCULATE(
    SUM('Data'[Revenue (Rs.)]),
    'Data'[Date] >= DATE(2022,6,1) &&
    'Data'[Date] <= DATE(2025,3,31)
)
```
