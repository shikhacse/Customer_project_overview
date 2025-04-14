# 📊 Data Analysis using SQL, Power BI, and Excel

This project demonstrates how to analyze employee project data using SQL Server, Power BI, and Excel. It focuses on understanding employee assignments, departmental goals, and budget utilization for upcoming and completed projects.

---

## 📁 Project Structure

| Folder | Description |
|--------|-------------|
| `datasets/` | Contains headshot CSV and sample department/project data |
| `dashboard_file/` | Final Power BI file (`.pbix`) |
| `images/` | Screenshots of the Power BI dashboard and data model |

---

## 🌟 Project Objectives

- Analyze project assignments across departments
- Track budget vs project vs salary costs
- Visualize employee-level metrics
- Combine headshots, SQL outputs, and transformed data

---

## 🧠 Tools & Skills Used

- 🗃️ SQL Server: joins, CTEs, view creation
- 📊 Power BI: Power Query, Group By, custom columns, visual design
- 📂 Excel: CSV import and column cleanup
- 🧱 Data modeling: relational structure, lookup fields, transformations

---

## 🔗 Data Sources

### 1. `Query1` – SQL View

Imported using a custom SQL query:

```sql
WITH project_status AS (
    SELECT project_id, project_name, project_budget, 'upcoming' AS status
    FROM upcoming_projects
    UNION ALL
    SELECT project_id, project_name, project_budget, 'completed' AS status
    FROM completed_projects
)
SELECT 
    e.employee_id,
    e.first_name,
    e.last_name,
    e.job_title,
    e.salary,
    d.Department_Name,
    pa.project_id,
    p.project_name,
    p.status
FROM 
    employees e
JOIN departments d ON e.department_id = d.Department_ID
JOIN project_assignments pa ON pa.employee_id = e.employee_id
JOIN project_status p ON p.project_id = pa.project_id;
```
### 2️⃣ `Head_Shots` – CSV Import

This CSV file contains:

- `Employee_ID`
- `Head_Shot` (URL)

📌 Used to map employee headshots into Power BI visuals.

---

### 3️⃣ `Cost Table` – Power Query Grouping

Created using **Power Query’s Advanced Group By**:

- **Grouped by**: `Department_Name`, `Department_Goals`
- **Aggregated columns**:
  - `Budget` = Sum of `Department_Budget`
  - `salary cost` = Sum of `salary`
  - `Project Cost` = Sum of `project_budget`


---

### 🧮 Custom Columns (in Power Query)

These were added using **Transform → Add Column → Custom Column**:

```powerquery
// Capital Revenue
= [Budget] * 0.5 - ([salary cost] * 2 + [Project Cost])

// 2 year Budget
= [Budget] * 0.5
---
## 📸 Final Dashboard Preview

The dashboard contains:

- 👤 **Employee Profile** — displays image, name, job title
- 📊 **Project Distribution** — visualized by status and budget
- 💰 **Budget Breakdown** — budget by department and project
- 📋 **Goals Matrix** — includes Capital Revenue and 2-Year Budget calculations

![Dashboard Overview](./images/project_overview_dashboard.png)
