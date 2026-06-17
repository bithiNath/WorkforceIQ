# WorkforceIQ — HR Analytics Dashboard

An end-to-end HR analytics project that tracks employee attrition, compensation, performance, diversity, and attendance using SQL for data analysis and Power BI for visualization.

## Overview

This project simulates a real-world HR analytics workflow: raw employee data is loaded into a PostgreSQL database, analyzed using SQL, and visualized in an interactive Power BI dashboard. The goal is to answer the kind of business questions an HR or People Analytics team would actually ask — who is leaving, who is underpaid, which departments struggle with attendance, and whether performance and pay are aligned.

## Tech stack

- **PostgreSQL** — data modeling and analysis
- **Power BI** — interactive dashboard and reporting

## Project workflow

```
Raw CSV data → PostgreSQL (table creation + import) → SQL analysis queries → Power BI (dashboard)
```

1. **Extract** — Raw HR data sourced as CSV files (employees, departments, salaries, performance, attendance)
2. **Load** — Created a normalized schema in PostgreSQL with 5 tables and foreign key relationships, then imported the CSV files using `VS code Terminal`
3. **Analyze** — 12 SQL queries written in PostgreSQL to answer specific HR business questions
4. **Visualize** — Each SQL query's result loaded directly into Power BI and mapped to a corresponding chart

## Dataset

| Table | Rows | Description |
|---|---|---|
| `employees` | 1,000 | Core employee master data (demographics, hire/exit dates, job title, status) |
| `departments` | 7 | Department reference table |
| `salaries` | 1,000 | Base salary and bonus per employee |
| `performance` | 2,000 | Annual performance ratings (2022–2023, scale 1–5) |
| `attendance` | 90,000 | Daily attendance records (Jan–Mar 2024) |


## Business questions answered (SQL queries)

Each query was designed to answer a specific HR business question, and each one feeds directly into a Power BI visual.

| # | Business question | Query file | Power BI visual |
|---|---|---|---|
| Q1 | What is the total and active headcount? | `Q1_headcount.sql` | KPI card |
| Q2 | What is the overall attrition rate? | `Q2_attrition_rate.sql` | KPI card |
| Q3 | Which department has the highest attrition? | `Q3_attrition_by_dept.sql` | Bar chart |
| Q4 | Is the company's headcount growing year over year? | `Q4_headcount_by_year.sql` | Line chart |
| Q5 | Is there a pay gap by department and gender? | `Q5_salary_by_dept_gender.sql` | Clustered bar chart |
| Q6 | How is performance rating distributed across the workforce? | `Q6_performance_distribution.sql` | Donut chart |
| Q7 | Do higher performers earn more on average? | `Q7_salary_vs_performance.sql` | Bar chart |
| Q8 | How long do employees typically stay before leaving? | `Q8_tenure_analysis.sql` | Column chart (histogram) |
| Q9 | What is the gender diversity ratio per department? | `Q9_gender_diversity.sql` | Stacked bar chart |
| Q10 | Which department has the worst attendance? | `Q10_absenteeism.sql` | Line chart |
| Q11 | Who are the top 10 highest-paid active employees? | `Q11_top_earners.sql` | Table |
| Q12 | Has average performance improved year over year by department? | `Q12_yoy_performance.sql` | Line chart |

All 12 queries are available in [`/sql/02_analysis_queries.sql`](./sql/02_analysis_queries.sql).

## Power BI integration

Each query's result set was loaded into Power BI as its own table using **Get Data → PostgreSQL database → Advanced options**, pasting the corresponding SQL query directly. No DAX measures or calculated columns were created — all aggregation and business logic happens at the SQL layer, and Power BI is used purely for visualization and interactivity (slicers, filters, drill-through).

This approach keeps a clean separation of concerns: SQL owns the business logic and is independently verifiable, while Power BI owns the presentation layer.

## Dashboard pages

**Page 1 — Executive summary**
Total employees, attrition rate, average salary, and average performance rating as KPI cards, with a department-wise headcount overview.

**Page 2 — Attrition analysis**
Attrition rate by department, hiring trend by year, and tenure distribution.

**Page 3 — Compensation & performance**
Average salary by department and gender, salary vs. performance rating, and the top 10 highest-paid employees.

**Page 4 — Diversity & attendance**
Gender diversity by department and monthly absenteeism trend.

## Key insights

- *(Add 3–5 bullet points here once you've explored your final dashboard — e.g. "Engineering has the highest attrition rate at X%", "Female representation is lowest in Operations at X%", "Top performers earn on average X% more than average performers.")*

## Repository structure

```
hr-analytics-dashboard/
│
├── data/
│   ├── employees.csv
│   ├── departments.csv
│   ├── salaries.csv
│   ├── performance.csv
│   └── attendance.csv
│
├── sql/
│   ├── 01_create_tables.sql
│   └── 02_analysis_queries.sql
│
├── powerbi/
│   └── HR_Analytics_Dashboard.pbix
│
├── screenshots/
│   ├── executive_summary.png
│   ├── attrition_analysis.png
│   ├── compensation.png
│   └── diversity_attendance.png
│
└── README.md
```

## How to run this project

1. Clone the repository
   ```
   git clone https://github.com/your-username/hr-analytics-dashboard.git
   ```
2. Run `sql/01_create_tables.sql` in PostgreSQL (via `psql` or pgAdmin)
3. Import the CSV files from `/data` into their corresponding tables using the `COPY` commands above
4. Run the queries in `sql/02_analysis_queries.sql` to verify the data
5. Open `powerbi/HR_Analytics_Dashboard.pbix` in Power BI Desktop
6. Update the data source connection (File → Options and settings → Data source settings) to point to your local PostgreSQL instance
7. Refresh the data (Home → Refresh)

## Author

**Your Name**
[LinkedIn](#) · [Portfolio](#) · [Email](#)

## License

This project uses synthetically generated data for educational and portfolio purposes only.
