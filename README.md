# ✈️ HighCloud Airlines – Performance Analysis

> A multi-tool data analytics project analyzing airline operations, load factors, passenger trends, and route performance using **MySQL**, **Power BI**, **Tableau**, **Excel**, and **PowerPoint**.

---

## 📁 Repository Structure

```
HighCloud-Airlines-Project/
│
├── Airlines_Performance_Analysis.xlsx              # Data model, pivot analysis & Excel dashboard
├── HighCloudAirline_MySQL.sql                      # SQL queries for data transformation & KPIs
├── High_Cloud_Airline_Analysis.pbix                # Power BI dashboard
├── High_Cloud_Airlines_Analysis_dashboard.twbx     # Tableau dashboard
└── High_cloud_Airlines_With-Dashboards.pptx        # Final presentation with dashboards
```

---

## 🎯 Project Objective

To analyze the operational performance of **HighCloud Airlines** by examining key metrics such as load factor, passenger volumes, route efficiency, and fleet utilization — across time, geography, and carrier dimensions — and present insights through interactive dashboards.

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|---|---|
| **MySQL** | Data transformation, KPI queries, derived columns |
| **Microsoft Excel** | Data model, pivot tables, Excel dashboard |
| **Power BI (.pbix)** | Interactive visual dashboard |
| **Tableau (.twbx)** | Visual analytics dashboard |
| **PowerPoint (.pptx)** | Final presentation with embedded dashboards |

---

## 🔍 Key Business Questions Answered

1. **Date Intelligence** — Derived Year, Month, Quarter, Weekday, Financial Month & Financial Quarter from raw date fields
2. **Load Factor Analysis** — Calculated `Transported Passengers / Available Seats` on:
   - Yearly, Quarterly, and Monthly basis
   - Per Carrier Name
   - Weekend vs Weekday breakdown
3. **Top 10 Carriers** — Ranked by passenger volume and load factor efficiency
4. **Top Routes** — Identified busiest city-pair routes by flight count
5. **Distance Group Analysis** — Classified flights into Short Haul / Medium Haul / Long Haul categories

---

## 📊 Key Metrics

| Metric | Description |
|---|---|
| **Load Factor %** | `(Transported Passengers / Available Seats) × 100` |
| **Departures Performed** | Actual flights operated vs scheduled |
| **Transported Passengers** | Total revenue passengers carried |
| **Available Seats** | Seat capacity offered |
| **Ramp-to-Ramp Time** | Total elapsed gate-to-gate time |
| **Air Time** | Actual in-air duration |
| **Payload & Freight** | Cargo and mail volumes |

---

## 🧩 Data Dimensions

- **Time** — Date, Year, Month, Quarter, Weekday, Weekend/Weekday, Financial Month/Quarter
- **Carrier** — Airline ID, Carrier Code, Carrier Name, Carrier Group
- **Geography** — Origin & Destination City, State, Country, Market ID, World Area Code
- **Aircraft** — Aircraft Group (Jet/Turbo-Prop/Piston/Helicopter), Aircraft Type, Configuration
- **Route** — Distance Group, Haul Type (Short/Medium/Long), Service Class, Flight Type

---

## 💡 Sample SQL Insights

```sql
-- Yearly Load Factor %
SELECT Year,
    CONCAT(ROUND(SUM(Transported_Passengers) / 1000000, 2), 'M') AS Total_Passengers,
    CONCAT(ROUND(SUM(Available_Seats) / 1000000, 2), 'M') AS Total_Seats,
    CONCAT(ROUND((SUM(Transported_Passengers) / SUM(Available_Seats)) * 100, 2), '%') AS Load_Factor_Percentage
FROM maindata
GROUP BY Year ORDER BY Year;

-- Top 10 Carriers by Passengers
SELECT Carrier_Name,
    CONCAT(ROUND(SUM(Transported_Passengers) / 1000000, 2), 'M') AS Total_Passengers
FROM maindata
GROUP BY Carrier_Name
ORDER BY SUM(Transported_Passengers) DESC LIMIT 10;

-- Haul Type Classification
SELECT d.Distance_Interval,
    CASE WHEN d.Distance_Interval < 1000 THEN 'Short_Haul'
         WHEN d.Distance_Interval < 3000 THEN 'Medium_Haul'
         ELSE 'Long_Haul' END AS Haul_Type,
    COUNT(m.Airline_ID) AS Total_Flights
FROM maindata m
JOIN distance_groups d ON m.Distance_Group_ID = d.Distance_Group_ID
GROUP BY d.Distance_Interval ORDER BY Distance_Group_ID;
```

---

## 📌 Data Source

Based on the **U.S. Bureau of Transportation Statistics (BTS) T-100 Domestic Segment** dataset, covering scheduled and non-scheduled domestic airline operations.

---

## 🚀 How to Use

1. **SQL Analysis** — Import `HighCloudAirline_MySQL.sql` into MySQL Workbench and run against your `maindata` table
2. **Excel** — Open `Airlines_Performance_Analysis.xlsx` to explore pivot tables and the dashboard
3. **Power BI** — Open `High_Cloud_Airline_Analysis.pbix` in Power BI Desktop
4. **Tableau** — Open `High_Cloud_Airlines_Analysis_dashboard.twbx` in Tableau Desktop or Tableau Public
5. **Presentation** — View `High_cloud_Airlines_With-Dashboards.pptx` for the full project walkthrough

---

*📅 Project completed as part of a Data Analytics Portfolio | HighCloud Airlines Case Study*
