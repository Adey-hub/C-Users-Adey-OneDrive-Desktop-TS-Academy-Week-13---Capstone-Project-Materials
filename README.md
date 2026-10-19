# Logistics Operations Dashboard: Power BI Capstone Project

![Power BI](https://img.shields.io/badge/Tool-Power%20BI-F2C811?logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/Language-DAX-blue)
![Dashboards](https://img.shields.io/badge/Dashboards-4-green)

A four-page Power BI report that analyses three years (2022 to 2024) of trucking operations: driver performance, route and customer profitability, fleet utilisation and maintenance, fuel efficiency, safety, and seasonal patterns.

---

## Table of Contents
1. [Project Brief](#1-project-brief)
2. [Data Source](#2-data-source)
3. [Data Cleaning](#3-data-cleaning)
4. [Method](#4-method)
5. [Dashboards](#5-dashboards)
6. [DAX Measures](#6-dax-measures)
7. [Key Findings](#7-key-findings)
8. [Recommendations](#8-recommendations)
9. [Limitations and Items to Validate](#9-limitations-and-items-to-validate)
10. [Repository Structure](#10-repository-structure)
11. [How to Use](#11-how-to-use)
12. [Author](#12-author)

---

## 1. Project Brief

**Task:** Build a Power BI capstone project with a maximum of four dashboards, each showing its own KPIs and slicers.

**Business questions answered**
- Which drivers, routes and customers perform best and worst?
- How well are trucks and trailers used, and what does maintenance downtime cost?
- Is fuel efficiency improving, and where did the fuel savings come from?
- Where are the safety risks, and how many incidents were preventable?
- Does demand, pricing or on-time performance change with the season?

---

## 2. Data Source

**Logistics Database Schema:** 14 Excel sheets loaded into Power BI.

| Table | Columns | Rows |
|---|---:|---:|
| Customers | 8 | 200 |
| Drivers | 12 | 150 |
| Driver Monthly Metrics | 9 | 4,464 |
| Delivery Events | 11 | 170,820 |
| Facilities | 9 | 50 |
| Fuel Purchases | 11 | 196,442 |
| Loads | 12 | 85,410 |
| Maintenance Records | 12 | 2,920 |
| Routes | 10 | 58 |
| Safety Incidents | 15 | 170 |
| Trailers | 9 | 180 |
| Trips | 12 | 85,410 |
| Trucks | 11 | 120 |
| Truck Utilisation Metrics | 10 | 3,312 |

---

## 3. Data Cleaning

Done in Power Query:
- Replaced state abbreviations with full state names in the license state, location state, origin state, destination state and state columns
- Trimmed text columns
- Corrected data types
- Removed empty rows and columns

---

## 4. Method

| Stage | Power BI area | What was done |
|---|---|---|
| Clean and transform | Power Query Editor | Applied the cleaning steps above |
| Model and calculate | Model view / DAX | Related the tables and wrote the measures in Section 6 |
| Visualise | Report view | Built four dashboards with KPI cards, charts and slicers |

---

## 5. Dashboards

**Slicers on every page:** State, Year, Quarter, Month

### Dashboard 1: Driver Performance and Fuel Efficiency
![Dashboard 1](images/dashboard_1_driver_fuel.png)

- **KPIs:** On-Time Delivery Rate %, On-Time Pickup Rate, Trips Completed, Trips per Driver, Average MPG, Fuel Cost, Fuel Cost per Mile, Average Idle Hours, Revenue per Mile
- **Visuals:** Top 10 / Bottom 10 drivers by on-time rate, MPG by year, fuel cost trend, on-time rate by month

### Dashboard 2: Route and Customer Profitability
![Dashboard 2](images/dashboard_2_route_customer.png)

- **KPIs:** Total Revenue, Route Profit, Route Profit Margin %, Route Direct Cost, Route Cost per Mile, Active Customers, Revenue per Customer, Detention Rate %, Revenue YoY %
- **Visuals:** Top lanes by revenue and margin, top customers by revenue, on-time rate by customer, contract vs spot revenue

### Dashboard 3: Fleet Utilisation and Maintenance
![Dashboard 3](images/dashboard_3_fleet_maintenance.png)

- **KPIs:** Active Trucks, Average Fleet Utilisation %, Revenue per Truck, Revenue per Trailer, Maintenance Cost, Maintenance Cost per Mile, Downtime Hours, Estimated Revenue Lost to Downtime
- **Visuals:** Maintenance cost by type, utilisation rate by year, downtime by maintenance type, maintenance cost by month

### Dashboard 4: Safety and Seasonal Patterns
![Dashboard 4](images/dashboard_4_safety_seasonal.png)

- **KPIs:** Total Incident Cost, Accidents, Incidents per Million Miles, Preventable Rate %, Claim Amount, Vehicle Damage Cost, Cargo Damage Cost
- **Visuals:** Incidents by type and preventability, incident cost by type, incidents by month, load volume seasonal index, revenue by season

---

## 6. DAX Measures

| Category | Measures |
|---|---|
| Revenue and volume | Total Revenue, Total Loads, Total Trips, Total Miles, Average Monthly Revenue, Revenue per Mile, Revenue per Load, Revenue per Customer, Revenue per Driver, Revenue per Truck, Revenue per Trailer, Revenue YoY % |
| Delivery and driver | On-Time Delivery Rate, On-Time Pickup Rate, Trips Completed, Trips per Driver, Trips per Truck, Active Drivers, Delivery Events, Average Miles per Trip |
| Detention and idle | Detention Events, Detention Rate %, Average Detention Minutes, Idle Hours %, Average Idle Hours per Trip |
| Fuel | Fuel Cost, Fuel Cost per Mile, Average MPG |
| Route profitability | Route Direct Cost, Route Cost per Mile, Route Profit, Route Profit per Mile, Route Profit Margin % |
| Fleet and maintenance | Average Utilisation Rate, Maintenance Cost, Maintenance Cost per Mile, Maintenance Cost per Truck, Part Cost, Labour Cost, Average Downtime per Event, Estimated Revenue Lost to Downtime |
| Safety | Accidents, Accidents per Million Miles, At-Fault Incidents, At-Fault Incidents %, Preventable Accidents, Preventable Incidents, Injury Incidents, Average Cost per Incident, Total Incident Cost, Claim Amount, Vehicle Damage Cost, Cargo Damage Cost |
| Customers | Active Customers, Customer Revenue |

<!-- Tip: paste one or two of your key DAX formulas below so reviewers can see your coding style. -->

```DAX
-- Example: replace with your own formula
On-Time Delivery Rate =
DIVIDE(
    CALCULATE(COUNTROWS(Delivery_Events), Delivery_Events[On_Time] = TRUE()),
    COUNTROWS(Delivery_Events)
)
```

---

## 7. Key Findings

### Driver performance
- On-time rate is low and uniform: **55.7%** overall, only 55.0% to 56.2% by month.
- Among drivers with 50+ trips, the best are about 58% to 59% on time and the weakest about 52% to 54%. A gap of roughly 7 points points to a systemic cause (dispatch planning, appointment times, facility waits) rather than driver behaviour.
- MPG (6.42 to 6.49) and revenue per mile ($2.13 to $2.16) are almost identical across top and bottom drivers.

### Route profitability
- The eight highest-revenue lanes bring in **$75.2M (28.6% of revenue)** with direct margins of 76.6% to 82.6%.
- Strongest: Charlotte to Portland (82.6% margin, $10.0M). Weakest of the eight: Seattle to Indianapolis (76.6% margin, $7.7M).
- Direct cost per lane is stable at about 17% to 23% of revenue, dominated by fuel.

### Fleet utilisation
- Average utilisation is about **83%** (83.5% in 2022, 82.3% in 2023, 83.4% in 2024).
- Revenue per truck is about $2.85M over three years; revenue per trailer is about $1.46M.

### Maintenance and downtime
- Maintenance cost is **$5.73M (2.2% of revenue)** across 2,920 events, about $1,963 per event.
- Cost is spread evenly across types (Preventive $964K, Repair $945K, Brake $912K, Tire $919K, Engine $891K, Transmission $880K). Inspections are cheap at about $509 per event.
- Downtime is **72,231 hours (about 3.0% of available truck hours)**, roughly 25 hours per event for every type.
- Estimated revenue capacity lost to downtime is about **$7.8M** over three years (an upper-end estimate).
- Preventive maintenance is about 17% of cost but shows no lower downtime or cost per event than repairs.
- Maintenance cost peaks in June and October and is lowest in February.

### Fuel efficiency
- MPG is flat at 6.44 to 6.45 in all three years.
- Fuel cost per mile fell **12.3%** and total fuel cost fell **$4.3M** (2022 to 2024) on flat miles. Because MPG did not change, the saving came from lower fuel prices or purchasing, not driving efficiency.
- Sensitivity: at 2024 volumes, every +0.1 MPG saves roughly **$0.46M a year**.

### Customer analysis
- Revenue is well diversified: the largest customer (First Group) is $9.1M (3.5% of revenue) and the top eight customers together are about 16.7%.
- On-time delivery is 43.8% to 46.7% for every top customer, again pointing to a process issue.
- Detention affects 86% to 88% of events for every top customer.

### Safety
- **170 incidents** in three years costing about **$5.3M** (about $31K per incident).
- DOT violations: 39 (18 preventable). Equipment damage: 35 (9 preventable). Accidents: 35 (14 preventable). Customer complaints: 34 (13 preventable). Moving violations: 27 (10 preventable).
- Equipment damage is the costliest type (about $1.48M, about $42K each).
- 2024 was the worst year (60 incidents; 1.47 per million miles). Incidents cluster in January and summer.

### Seasonal patterns
- Demand is almost flat: the load-volume seasonal index runs from 0.93 (February) to 1.03 (October).
- Summer is the highest-revenue season (about $67M) and winter the lowest (about $64M), a gap of about 4.5%.
- Revenue per mile stays between $2.14 and $2.16 all year, so there is no evidence of peak-season pricing.

---

## 8. Recommendations

1. **Fix the process, not the drivers.** Review dispatch planning, appointment windows and facility wait times, since low on-time performance is the same for every driver and customer.
2. **Tackle detention.** If the 86% to 88% detention rate is accurate, negotiate detention fees or loading-time limits with customers.
3. **Confirm the fuel saving.** Check purchasing records, and compare fuel surcharge recovery against falling fuel costs.
4. **Review the full lane list.** Look beyond the top eight lanes to find the true worst performers.
5. **Test the value of preventive maintenance.** Current data shows no downtime or cost advantage over repairs.
6. **Target preventable incidents.** Focus on DOT violations and accidents, where preventable shares are 46% and 40%.
7. **Consider peak-season pricing.** Rates do not move with demand.

---

## 9. Limitations and Items to Validate

- Miles per truck works out to about 443,000 a year, far above the typical 100,000 to 150,000 for long-haul trucks. Validate the mileage data.
- The model shows 92 trucks and 180 trailers in use every year; confirm how "active" is defined against the 120 trucks in the fleet table.
- The detention rate (86% to 88%) may reflect the definition used. Confirm it.
- Estimated downtime revenue loss is an upper bound; spare trucks and rescheduling can recover some of it.
- Only the top eight lanes by revenue were reviewed.

---

## 10. Repository Structure

```
logistics-powerbi-capstone/
├── README.md
├── data/                  # Raw Excel files (or a link if too large)
├── powerbi/
│   └── Logistics_Capstone.pbix
├── images/                # Dashboard screenshots used above
└── docs/
    └── Management_Report.pdf
```

---

## 11. How to Use

1. Download or clone this repository.
2. Open `powerbi/Logistics_Capstone.pbix` in Power BI Desktop.
3. If prompted, update the data source path to the `data/` folder (Home > Transform data > Data source settings).
4. Use the State, Year, Quarter and Month slicers to explore each page.

---

## 12. Author

**[Your Name]**, Data Analyst
[LinkedIn](https://www.linkedin.com/) | [Email](mailto:you@example.com)
