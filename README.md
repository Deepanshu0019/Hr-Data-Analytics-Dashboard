# Hr-Data-Analytics-Dashboard

📌 Project Overview

This project explores workforce attrition data to help HR teams make **data-driven decisions**. The dashboard answers critical business questions like — *Why are employees leaving? Which departments are most affected? What age groups have the highest attrition?*

---

## 🎯 Key KPIs

| Metric | Value |
|--------|-------|
| 👨‍💼 Overall Employees | 1,470 |
| 📉 Total Attrition | 237 |
| 📊 Attrition Rate | **16.1%** |
| ✅ Active Employees | 1,233 |
| 🎂 Average Age | 37 |

---

## 📊 Dashboard Highlights

- **Department-wise Attrition** — R&D (56.12%), Sales (38.82%), HR (5.06%)
- **Education Field-wise Attrition** — Life Sciences (89), Medical (63), Marketing (35)
- **Attrition by Age Group & Gender** — Highest in 25–34 age band (112 employees)
- **Job Satisfaction Matrix** — Ratings across all job roles (1–4 scale)
- **Employee Count by Age Group** — Male vs Female stacked bar chart

---

## 🗄️ SQL Queries Used

### 1. Attrition Rate by Gender for Different Age Groups
```sql
SELECT
  age_band,
  gender,
  COUNT(attrition) AS attrition,
  ROUND(
    (CAST(COUNT(attrition) AS NUMERIC) /
    (SELECT COUNT(attrition) FROM hrdata WHERE attrition = 'Yes')) * 100, 2
  ) AS pct
FROM hrdata
WHERE attrition = 'Yes'
GROUP BY age_band, gender
ORDER BY age_band, gender DESC;
```

### 2. Active Employee Count
```sql
-- Method 1
SELECT SUM(employee_count) -
  (SELECT COUNT(attrition) FROM hrdata WHERE attrition = 'Yes')
FROM hrdata;

-- Method 2
SELECT (SELECT SUM(employee_count) FROM hrdata) - COUNT(attrition) AS active_employee
FROM hrdata
WHERE attrition = 'Yes';
```

### 3. Education Field & Job Role wise Attrition
```sql
SELECT
  education_field,
  job_role,
  COUNT(attrition) AS attrition_count
FROM hrdata
WHERE attrition = 'Yes'
GROUP BY education_field, job_role
ORDER BY education_field, job_role;
```

### 4. Attrition Rate by Job Role
```sql
SELECT
  job_role,
  COUNT(attrition) AS attrition_count,
  ROUND(
    (CAST(COUNT(attrition) AS NUMERIC) /
    (SELECT COUNT(attrition) FROM hrdata WHERE attrition = 'Yes')) * 100, 2
  ) AS pct
FROM hrdata
WHERE attrition = 'Yes'
GROUP BY job_role
ORDER BY job_role;
```

---

## 🔍 Key Insights

- 🔴 **R&D Department** has the highest attrition at **56.12%**
- 📚 **Life Sciences** graduates leave the most (89 employees)
- 👶 **Age group 25–34** is the most vulnerable with 112 attritions
- 👨 **Male employees** have higher attrition than females across most age groups
- 💼 **Sales Executives** & **Laboratory Technicians** show the highest job role attrition

---

## 🛠️ Tools & Technologies

| Tool | Usage |
|------|-------|
| **Power BI** | Dashboard creation, DAX measures, visualizations |
| **SQL (PostgreSQL)** | Data extraction, attrition calculations |
| **Microsoft Excel** | Data cleaning, preprocessing |

---

## 📁 Project Structure

```
HR-Analytics-Dashboard/
│
├── 📊 HR_Analytics_Dashboard.pbix   # Power BI file
├── 🗄️ hr_queries.sql                # All SQL queries
├── 📋 hrdata.xlsx                   # Raw dataset
├── 🖼️ dashboard_preview.png         # Dashboard screenshot
└── 📄 README.md
```

---

## 🚀 How to Use

1. Clone this repository
   ```bash
   git clone https://github.com/Deepanshu0019/HR-Analytics-Dashboard.git
   ```
2. Open `hrdata.xlsx` to explore the raw data
3. Run `hr_queries.sql` in PostgreSQL to explore queries
4. Open `HR_Analytics_Dashboard.pbix` in **Power BI Desktop**
5. Refresh data source if needed and explore the dashboard

<img width="1294" height="683" alt="Screenshot 2026-04-09 152303" src="https://github.com/user-attachments/assets/db3247a9-5347-4f34-92c3-4282c265f38f" />

---

## 👨‍💻 Author

**Deepanshu Mehta**
📧 deepanshu9469@gmail.com
🔗 [LinkedIn](https://www.linkedin.com/in/deepanshu-mehta-19dm)
🐙 [GitHub](https://github.com/Deepanshu0019)

---

⭐ **If you found this project helpful, please give it a star!**
