# 🛠️ Operation Team Tools Tracking & Life Management

[![PowerBI](https://img.shields.io/badge/Analytics-PowerBI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)](https://powerbi.microsoft.com/)
[![SAP](https://img.shields.io/badge/Data_Source-SAP_ERP-008FD3?style=for-the-badge&logo=sap&logoColor=white)](https://www.sap.com/)
[![Industry](https://img.shields.io/badge/Industry-4.0-green?style=for-the-badge)](https://en.wikipedia.org/wiki/Fourth_Industrial_Revolution)

## 📌 Project Overview
This project focuses on the digital tracking and life-cycle management of critical assembly line tools. By integrating **SAP ERP data** (orders/procurement) with **real-time shop floor production data** provided by operators, this system visualizes tool wear, consumption trends, and replacement schedules via PowerBI.

The primary goal is to transition from reactive maintenance to a data-driven **Predictive Tool Management** strategy.

## ⚙️ Monitored Equipment & Specifications

The system tracks several key categories of tools, each with unique lifecycle dynamics:

| Tool Category | Varieties | Target Life (Cycles) | Operational Logic |
| :--- | :---: | :---: | :--- |
| **Electrodes** | 18 Types | ~10,000 | Replaced approx. every 10 days. Lifespan fluctuates based on quality issues and weld parameters. |
| **Honing Heads** | 5 Units | ~150,000 | **International Loop:** Heads are sent to Germany for stone replacement/refurbishment and returned to the plant. |
| **Filters** | Standard | Variable | Tracked based on pressure differential and production volume. |
| **Suction Cups** | Standard | Variable | Tracked via manual wear-and-tear logs from the assembly line. |

## 📊 Technical Architecture & Deep Dive

### 1. Data Integration (The "Hybrid" Approach)
The model consolidates two distinct data streams:
* **System Data (SAP):** Pulls order history, material movements, and official production targets.
* **Human-in-the-loop (Field Logs):** Daily logs submitted by production operators regarding tool swaps, manual cycle counts, and observed quality defects.

### 2. Predictive Analytics & Calculations
The system applies the following logic to forecast replacements:
* **Remaining Useful Life (RUL):** Calculated as $RUL = TargetCycles - CurrentCycles$.
* **Anomaly Detection:** Tracking instances where Electrodes fail before the 10,000-cycle mark to identify machine calibration issues or raw material defects.
* **Lead Time Buffer:** For Honing Heads, the system tracks "Days in Transit" to Germany to ensure the 5-unit rotation never hits a bottleneck.

### 3. PowerBI Visualization Layers
* **Executive Dashboard:** High-level monthly/yearly consumption costs.
* **Operator View:** Real-time "Health Bars" for each active tool on the line.
* **Maintenance Alert:** Automated triggers when a tool reaches 90% of its expected life.

## 🛠️ Tech Stack
* **Data Orchestration:** Power Query (M Language) for cleaning SAP exports.
* **Analytics Engine:** DAX (Data Analysis Expressions) for complex cycle-life calculations.
* **Visualization:** Microsoft PowerBI.
* **Data Source:** Excel/CSV Exports from SAP & Manual Input Forms.

## 🧮 Production Logic & Math
The tracking model operates on the following production distribution:

### Electrode Tracking (3-Line Split)
- **Total Plant Output:** 10,000 units/day
- **Throughput per Line:** ~3,333 units/day
- **Lifespan Calculation:** $$10,000 \text{ (Total Life)} / 3,333 \text{ (Daily Cycles)} \approx 3 \text{ Days per Electrode}$$

### Honing Head Tracking (2-Line Split)
- **Total Plant Output:** 10,000 units/day
- **Throughput per Line:** 5,000 units/day
- **Lifespan Calculation:** $$150,000 \text{ (Total Life)} / 5,000 \text{ (Daily Cycles)} = 30 \text{ Days per Head}$$

## 📁 Project Structure

```bash
├── data/           # Raw and processed CSV/Excel files
├── docs/           # Documentation and Dashboard screenshots
├── notebooks/      # Python scripts for data simulation and cleaning
├── powerbi/        # PowerBI Template (.pbit) files
└── README.md       # Project overview and technical details
