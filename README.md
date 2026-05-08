# 🤖 HireSync AI — Intelligent Recruitment Analytics Dashboard
  
> A data-driven recruitment intelligence platform built to eliminate bias, track hiring performance, and optimise salary spend.

---

## 📂 Project Files

| File | Link |
|------|------|
| HireSync.xlsx | [📊 Open Dataset](./HireSync.xlsx) |
| DV_PROJECT.pbix | [📈 Open Power BI File](./DV_PROJECT.pbix) |
| DV_Power_BI_Report.pdf | [📄 Open Report PDF](./DV_Power_BI_Report.pdf) |
| DV_Mini_Project_-_Report.pdf | [📝 Open Project Report](./DV_Mini_Project_-_Report.pdf) |

---

## 📊 Dashboard Pages

| Page | Title | Key Visuals |
|------|-------|-------------|
| **Page 1** | Executive Recruitment Overview | Hire Rate KPI, Hiring Trend (Line), Hires by Dept (Donut), Recruitment Pipeline (Funnel), ATS vs Tech Scatter |
| **Page 2** | Candidate Intelligence & Score Analytics | Score Gauges, Candidate Tier Panel, Detailed Candidate Table |
| **Page 3** | Budget Forecast & Salary Gap Analysis | Budget vs Actuals (Area), Salary Gap by Dept (Bar), Decomposition Tree |

---

## 🔢 Key Metrics at a Glance

| Metric | Value |
|--------|-------|
| Total Applicants | 100 |
| Total Hires | 57 |
| Hire Rate | 57.0% |
| Avg Technical Score | 81.48 / 100 |
| Avg ATS Resume Score | 83.08 / 100 |
| Budget Forecast | $5.96M |
| Expected Budget | $10M |
| Actual Spend | $6M |
| Salary Gap (Expected vs Offered) | ~$4M |

---

## 🏢 Hires by Department

| Department | Share | Hires |
|------------|-------|-------|
| HR | 33.46% | 11 |
| Marketing | 25.05% | — |
| Engineering | 23.23% | 30 |
| Sales | 18.25% | 10 |

---

## 🧠 DAX Measures

| Measure | DAX Expression |
|---------|---------------|
| Total Applicants | `COUNTROWS(HireSync)` |
| Total Hires | `CALCULATE([Total Applicants], HireSync[Status] = "Hired")` |
| Hire Rate % | `DIVIDE([Total Hires], [Total Applicants], 0)` |
| Avg Tech Score | `AVERAGE(HireSync[Technical_Score])` |
| Salary Gap | `SUMX(HireSync, HireSync[Expected_Salary] - HireSync[Offered_Salary])` |
| Applicants YTD | `TOTALYTD([Total Applicants], Dim_Calendar[Date])` |
| YoY Growth % | `DIVIDE([Total Applicants] - [Apps Last Year], [Apps Last Year], 0)` |
| Hires MTD | `TOTALMTD([Total Hires], Dim_Calendar[Date])` |
| Rolling 90-Day Apps | `CALCULATE([Total Applicants], DATESINPERIOD(Dim_Calendar[Date], MAX(Dim_Calendar[Date]), -90, DAY))` |
| Parallel Period Hires | `CALCULATE([Total Hires], PARALLELPERIOD(Dim_Calendar[Date], -1, YEAR))` |

---

## 🏷️ Calculated Columns

| Column | Logic |
|--------|-------|
| **Candidate Tier** | `Elite` (Tech ≥ 90) · `Average` (Tech ≥ 70) · `Emerging` (< 70) |
| **Score Discrepancy** | `Technical_Score - ATS_Resume_Score` |
| **Salary Bracket** | `High` (Offered > $100K) · `Mid` (≤ $100K) |
| **Interview Intensity** | `High Intensity` (Rounds > 2) · `Standard` |
| **Application Year** | `YEAR(HireSync[Application_Date])` |

---

## 🗂️ Data Model
Star Schema
├── Fact Table:      HireSync (100 rows · 12 columns)
├── Dim_Department   (1:* → HireSync)
├── Dim_Job_Role     (1:* → HireSync)
└── Dim_Calendar     CALENDAR(DATE(2024,1,1), DATE(2026,12,31))
- **Grain:** One row per unique job application
- **Filter Direction:** Single-direction cross-filtering
- **Naming Convention:** PascalCase on all columns

---

## 💡 Key Insights

| # | Insight | Finding |
|---|---------|---------|
| 1 | **Pipeline Efficiency** | 57% hire rate signals highly targeted sourcing and effective pre-screening |
| 2 | **Score Alignment** | Avg Tech Score (81.48) ≈ Avg ATS Score (83.08) — AI screening model is well-calibrated |
| 3 | **Hiring Freeze Signal** | ~25 hires/year in 2024–25, sharp drop in 2026 (possible freeze or incomplete YTD data) |
| 4 | **Budget Optimisation** | $4M gap between expected and offered salaries — strong negotiation outcomes for the org |
| 5 | **Engineering Cost Risk** | Engineering has the most hires (30) and the widest salary gap — must inform future planning |

---
