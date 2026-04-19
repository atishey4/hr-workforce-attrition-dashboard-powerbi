# HR Workforce Insights & Employee Attrition Predictor Dashboard

## Objective
To design a Power BI dashboard that provides insights into workforce demographics, employee performance, and attrition trends while integrating a predictive component to forecast employee turnover.

---

## Tools Used
- **Power BI Desktop** – Dashboard design, data modeling, and report building
- **Power Query Editor** – Data cleaning and transformation
- **DAX (Data Analysis Expressions)** – KPI and measure creation
- **Microsoft Excel / CSV** – Source dataset

---

## Dataset Description

A realistic HR dataset containing **200+ rows** with the following columns:

| Column | Description |
|---|---|
| Employee ID | Unique identifier for each employee |
| Employee Name | Full name of the employee |
| Age | Employee age in years |
| Gender | Male / Female |
| Department | Engineering, Sales, HR, Finance, Customer Service, IT Support, Operations, Marketing |
| Job Role | Specific role within the department |
| Education Level | Undergraduate, Graduate, Postgraduate |
| Marital Status | Single / Married / Divorced |
| Location | City where the employee is based |
| Joining Date | Date the employee joined the organization |
| Years at Company | Total tenure in the organization |
| Monthly Income | Employee’s monthly salary |
| Performance Rating | Rating on a defined scale |
| Training Hours | Number of training hours completed |
| Overtime Status | Yes / No |
| Work Mode | Office / Hybrid / Remote |
| Job Satisfaction Score | Score indicating job satisfaction level |
| Work-Life Balance Score | Score indicating work-life balance perception |
| Promotion Last 2 Years | Yes / No |
| Absenteeism Rate | Rate of unplanned absences |
| Attrition Status | Yes (left) / No (active) |
| Attrition Risk Level | Low / Medium / High |

---

## Power Query Steps

1. **Remove null and blank values** – Cleaned rows with missing Employee ID, Department, or Attrition Status to ensure data reliability
2. **Change data types** – Set Monthly Income as Currency; Age, Years at Company as Whole Number; Joining Date as Date
3. **Handle duplicates** – Removed duplicate Employee IDs to maintain one record per employee
4. **Create Age Groups** – Created a calculated column to group employees into bands: Under 25, 25–35, 36–45, 45+
5. **Create Experience Bands** – Bucketed Years at Company into: 0–2 years, 3–5 years, 6–10 years, 10+ years
6. **Format date fields** – Standardized Joining Date to DD/MM/YYYY format
7. **Create Month and Year columns** – Extracted from Joining Date for cohort and trend analysis
8. **Create calculated columns** – Added Attrition Risk Level flags and Age Group columns directly in Power Query

---

## DAX Measures

```dax
Total Employees = COUNT(HRData[Employee ID])

Attrition Count = CALCULATE(COUNT(HRData[Employee ID]), HRData[Attrition Status] = "Yes")

Attrition Rate % = DIVIDE([Attrition Count], [Total Employees], 0) * 100

Active Employees = CALCULATE(COUNT(HRData[Employee ID]), HRData[Attrition Status] = "No")

Avg Monthly Income = AVERAGE(HRData[Monthly Income])

Avg Job Satisfaction Score = AVERAGE(HRData[Job Satisfaction Score])

Avg Work-Life Balance Score = AVERAGE(HRData[Work-Life Balance Score])

Avg Tenure = AVERAGE(HRData[Years at Company])

Overtime Employee Count = CALCULATE(COUNT(HRData[Employee ID]), HRData[Overtime Status] = "Yes")

High Attrition Risk Count = CALCULATE(COUNT(HRData[Employee ID]), HRData[Attrition Risk Level] = "High")

High Risk % = DIVIDE([High Attrition Risk Count], [Total Employees], 0) * 100
```

---

## Dashboard Features

- **KPI Cards** – Total Employees, Attrition Rate %, Active Employees, Avg Monthly Income, High Risk % displayed at the top
- **Clustered Bar Chart** – Attrition Count and Attrition Rate % by Department
- **Horizontal Bar Chart** – Attrition Rate % by Job Role to identify high-turnover roles
- **Grouped Column Chart** – Female Count and Male Count by Department for gender distribution view
- **Donut Chart** – Total Employees by Attrition Risk Level (Low / Medium / High)
- **Donut Chart** – Total Employees by Work Mode (Office / Hybrid / Remote)
- **Slicers & Filters** – Department, Gender, Location, Attrition Risk Level, Work Mode

---

## Key Insights

- **Engineering and Sales** departments have the highest attrition count, requiring focused retention efforts
- **QA Engineers and L&D Specialists** show the highest attrition rate by job role
- Overall **Attrition Rate stands at 41%**, indicating a significant workforce stability challenge
- **35.5% of employees** are classified as High Attrition Risk, suggesting proactive HR intervention is needed
- The **average monthly income is ₹6,057**, with income disparity likely contributing to attrition in lower-paying roles
- **Hybrid work mode** has the largest share of employees, while Office-based employees show higher attrition risk
- Gender distribution is broadly balanced across most departments, with Sales having the highest female representation
- **Medium risk employees** form the largest segment of the workforce, representing a key retention opportunity

---

## Screenshots

### Dashboard Overview
![HR Workforce Dashboard](screenshots/dashboard_overview.png)

> *Add your Power BI dashboard screenshot here. Export from Power BI → File → Export → Export to PDF or take a screenshot and save in the `screenshots/` folder.*

---

## Conclusion

This HR Workforce Insights & Employee Attrition Predictor Dashboard provides HR teams and business leadership with a data-driven view of workforce health. By combining workforce demographics, attrition trends, risk segmentation, and satisfaction metrics into one interactive Power BI report, this dashboard enables organizations to take proactive steps in employee retention and strategic workforce planning. It is directly applicable for HR Analysts, People Analytics teams, HR Managers, and Operations leaders who need actionable insights to reduce turnover costs and build a more engaged workforce.
