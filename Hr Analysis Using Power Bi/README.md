
# Human Resources (Hr) analysis using Power Bi

In this project I worked with a HR dataset, focusing on analyzing employee data. This comprehensive project covered the entire process, from importing and cleaning the data to building and optimizing visualizations in Microsoft Power BI Desktop.

## Dashboard Link(Fabric)

[Interactive Dashboard](https://app.fabric.microsoft.com/view?r=eyJrIjoiZjNjZGYyMDMtMmI2OC00ZmEyLWI4NTAtYzQ2YTIwNjlmN2NmIiwidCI6ImYyYWY5N2MyLTFiODUtNDQwOC05YTc5LTBjNjI0N2M4YTQ0YiJ9&pageName=32bde92840b55248de7e)



## Tech Stack Used 

Powerbi

![Powerbi](https://github.com/user-attachments/assets/d705e3e8-95d9-4609-9a37-cdf7edc8b5b1)

## Data Cleaning

The raw dataset, provided in .csv format, was imported directly into Power BI, comprising One  table.
- As there was to date table so I created a date table by creating a blank query ,then I opened the advenced editor and pasted the script code created by Brian Grant.
- Then created another table for survey scores by duplicating the hr_attrition table and removed other columns keeping "Employee Number", "Switch Attrition/Retention 2", "Environment Satisfaction", "Heat Map - Attrition Emp", "Heat Map - Current Emp", "Job Involvement", "Job Satisfaction", "Relationship Satisfaction", "Work Life Balance" columns. M code is given below.

```
Table.SelectColumns(#"Reordered Age Column to 1st column",{"Employee Number", "Switch Attrition/Retention 2", "Environment Satisfaction", "Heat Map - Attrition Emp", "Heat Map - Current Emp", "Job Involvement", "Job Satisfaction", "Relationship Satisfaction", "Work Life Balance"})
```

- Then I Unpivoted other columns and renamed Attribute to Survey type and Values to Scores.THis table will be useful for creating the Heatmap table.

```
Table.UnpivotOtherColumns(#"Removed Other Columns", {"Heat Map - Current Emp", "Heat Map - Attrition Emp", "Switch Attrition/Retention 2", "Employee Number"}, "Attribute", "Value")
```
- I cleaned the data by ensuring columns were appropriately named, data types were accurate, and confirmed there were no missing values. I then started exploring potential relationships between the tables.

## Data Modeling

Once I confirmed the accuracy and consistency of the data, I proceeded to create a data model. I designated 'Hr_Attrition" as the key tables, then established relationships between them. For this project, I determined that only one-to-many relationships were needed. A visual representation of the final model is also provided for better clarity.

![Data Model](https://github.com/user-attachments/assets/338bd622-073b-4a6f-be8b-44f1aa785103)

## Dax Functions

With the table relationships in place, I began using DAX functions to analyze the dataset. I started by creating key KPIs such as Attrition Rate , Total Attrition , Current Employees. Some of the most frequently used DAX functions included:

- CALCULATE(): Used to apply new filter contexts, particularly useful for calculating Total Attrition, Current Employees.
- DISTINCTCOUNT():The DAX DISTINCTCOUNT function returns the count of unique (distinct) values in a column. It is commonly used to eliminate duplicates in the counting process.It is useful for calculating Total Employees.
- DIVIDE(): The DAX DIVIDE function performs division in a safer way by handling cases where the denominator might be zero or missing, avoiding errors.It is useful for calculating Attrition Rate.
- The DAX VAR function is used to define variables within a DAX expression, making the code easier to read and more efficient by avoiding redundant calculations. It is useful for calculating Min/Max Dates,Matrix Conditional Formatting,Dynamic Variance %.
- SWITCH():The DAX SWITCH function evaluates an expression against multiple possible values and returns a corresponding result. It acts like a more flexible IF function with multiple conditions.It is useful for calculating Matrix Conditional Formatting,Dynamic Variance %.

All the measures created were organized into a dedicated Measure Table for easy access.

## Dax Functions that were used are given below:

```
Total Employees = DISTINCTCOUNT(Hr_Attrition[Employee No.])

Total Attrition = CALCULATE([Total Employees],Hr_Attrition[Attrition]="Yes")

Current Employees = CALCULATE([Total Employees],Hr_Attrition[Attrition]="NO")

Attrition Rate = DIVIDE([Total Attrition],[Current Employees])

Blank Measure = " "
---
Min/Max Dates, formatted = 
var minDate = FORMAT(MIN('Hr_Attrition'[Attrition Date]), "DD MMM, YYYY")
var maxDate = FORMAT(MAX('Hr_Attrition'[Attrition Date]), "DD MMM, YYYY")

return "(" & minDate & " to " & maxDate & ")"
---

---
Matrix Conditional Formatting = 
var empCount = CALCULATE(COUNT('Survey Scores'[Employee Number]))
var attRetVal = MIN('Survey Scores'[Switch Attrition/Retention 2])

//This switch checks the attrition/retention value and uses a different color set for each
return SWITCH(
        TRUE(), 
            attRetVal = "Attrition" && empCount > 64, "#457b9d",
            attRetVal = "Attrition" && empCount >= 57, "#cdeae5",
            attRetVal = "Attrition" && empCount >= 52, "#f1faee",
            attRetVal = "Attrition", "#F1F1F1",
            attRetVal = "Retention" && empCount > 386, "#1d3557",
            attRetVal = "Retention" && empCount > 360, "#8b97a9",
            attRetVal = "Retention" && empCount > 244, "#b5bdc8",
            attRetVal = "Retention", "#F1F1F1",

        BLANK()
)

This measure is used in Survey Scores Table.
---

---
Employee Multirow Info = 
MIN('Hr_Attrition'[Employee No.]) & UNICHAR(10) &
MIN('Hr_Attrition'[Job Role]) & UNICHAR(10) &
MIN('Hr_Attrition'[Department]) & UNICHAR(10) 

Employee Multirow Details = 

"Attrition date: " & FORMAT(MIN(Hr_Attrition[Attrition Date]), "DD MMM, YYYY") & UNICHAR(10) &
"Avg. Satisfaction Score: " & MIN(Hr_Attrition[Avg. Satisfaction Score]) & UNICHAR(10) & 
"Performance Rating: " & MIN(Hr_Attrition[Performance Rating]) & UNICHAR(10) &
"Monthly Income: " & MIN(Hr_Attrition[Monthly Income]) & UNICHAR(10) &
"Salary Hike: " & MIN(HR_Attrition[Percent Salary Hike]) & UNICHAR(10) 

This measure is used in Recent Retention Table.
---

---
Dynamic Variance % = 
//this data is static, so we get the latest values by getting the max in the data table. Date tables are really useful for their "relative" columns to keep things dynamic - this calculation would auto-update as time passed if fresh data was coming in.
//WEEK
var latestWeek = CALCULATE(MAX('Date'[Week Relative]), 'Date'[Date] = MAX('Hr_Attrition'[Attrition Date]))
var priorWeekAttr = CALCULATE([Total Attrition], 'Date'[Week Relative] = latestWeek - 1)
var latestWeekAttr = CALCULATE([Total Attrition], 'Date'[Week Relative] = latestWeek)
var weekAttrChange = DIVIDE(latestWeekAttr - priorWeekAttr, priorWeekAttr)
var formattedWeekAttr = IF(weekAttrChange < 1, "▼ " & FORMAT(weekAttrChange * -1, "0.0%"), "▲" & FORMAT(weekAttrChange, "0.0%")) & " vs previous week"

//MONTH
var latestMonth = CALCULATE(MAX('Date'[Month Relative Num]), 'Date'[Date] = MAX('Hr_Attrition'[Attrition Date]))
var priorMonthAttr = CALCULATE([Total Attrition], 'Date'[Month Relative Num] = latestMonth - 1)
var latestMonthAttr = CALCULATE([Total Attrition], 'Date'[Month Relative Num] = latestMonth)
var monthAttrChange = DIVIDE(latestMonthAttr - priorMonthAttr, priorMonthAttr)
var formattedMonthAttr = IF(monthAttrChange < 1, "▼ " & FORMAT(monthAttrChange * -1, "0.0%"), "▲" & FORMAT(monthAttrChange, "0.0%")) & " vs previous month"

//QUARTER
var latestQuarter = CALCULATE(MAX('Date'[Qtr Num]), 'Date'[Date] = MAX('Hr_Attrition'[Attrition Date]))
var priorQuarterAttr = CALCULATE([Total Attrition], 'Date'[Qtr Num] = latestQuarter - 1)
var latestQuarterAttr = CALCULATE([Total Attrition], 'Date'[Qtr Num] = latestQuarter)
var quarterAttrChange = DIVIDE(latestQuarterAttr - priorQuarterAttr, priorQuarterAttr)
var formattedQuarterAttr = IF(quarterAttrChange < 1, "▼ " & FORMAT(quarterAttrChange * -1, "0.0%"), "▲" & FORMAT(quarterAttrChange, "0.0%")) & " vs previous quarter"

//YEAR
var latestYear = CALCULATE(MAX('Date'[Year Relative Num]), 'Date'[Date] = MAX('Hr_Attrition'[Attrition Date]))
var priorYearAttr = CALCULATE([Total Attrition], 'Date'[Year Relative Num] = latestYear - 1)
var latestYearAttr = CALCULATE([Total Attrition], 'Date'[Year Relative Num] = latestYear)
var yearAttrChange = DIVIDE(latestYearAttr - priorYearAttr, priorYearAttr)
var formattedYearAttr = IF(yearAttrChange < 1, "▼ " & FORMAT(yearAttrChange * -1, "0.0%"), "▲" & FORMAT(yearAttrChange, "0.0%")) & " vs previous year"


return SWITCH(
        TRUE(),
            SELECTEDVALUE('Date Hierarchy'[Date Hierarchy Order]) = 0, formattedWeekAttr,  //0 is the first field parameter row, for some reason it will give an error when trying to use the text W/M/Q/Y column instead
            SELECTEDVALUE('Date Hierarchy'[Date Hierarchy Order]) = 1, formattedMonthAttr,
            SELECTEDVALUE('Date Hierarchy'[Date Hierarchy Order]) = 2, formattedQuarterAttr,
            SELECTEDVALUE('Date Hierarchy'[Date Hierarchy Order]) = 3, formattedYearAttr,
            BLANK()
)
This is used Attrition Trend.
---


```
## Parameter
- Used Field Parameter to create Date Hierarchy 

```
Date Hierarchy = {
    ("W", NAMEOF('Date'[Year and Week]), 0),
    ("M", NAMEOF('Date'[Month Start Date]), 1),
    ("Q", NAMEOF('Date'[Qtr qq-yy]), 2),
    ("Y", NAMEOF('Date'[Year]), 3)
}

```

## Data Visualization

This Dashboard contains only one Page.In this one page I tried to visualize every key metrics.

**OVERVIEW:**
- Attrition Rate: 19.22%, indicating the percentage of employees who have left the company within the selected timeframe (27 May 2021 to 08 May 2022).

- Total Attrition: 237 employees have left the company during this period.

- Current Employees: The total number of employees currently in the organization is 1,233.

**Department:** Attrition figures are broken down by department.
- R&D: 133 attritions and Retention is 828 employees.
- Sales: 92 attritions and Retention is 354 employees.
- HR: 12 attritions and Retention is 51 employees.

**Attrition Trend:** Shows the trend of employee attrition over time .And it also shows attrition rate compared to previous week,month,quater and year.

**Demographics Section:**
- Male: 150 attrition, 732 retention.
- Female: 87 attrition, 501 retention.

**Age Group:** Shows the attrition and retention breakdown by age groups, with the 35-44 age range having the highest attrition.

**Education:** Displays attrition across different educational qualifications, with Bachelor’s Degree holders having the highest attrition.

**Survey Scores:** The section evaluates employees' satisfaction in different areas (on a scale of 1-4) for both attrition and retention. This includes:
- Environment Satisfaction: Scores of 3 and 4 are more common for attrition, while retention has higher satisfaction scores (3 and 4).
- Job Involvement, Job Satisfaction, Relationship Satisfaction, and Work-Life Balance: These are also analyzed, with lower scores more associated with attrition, and higher scores with retention.

**Recent Attrition:** Provides details on individual employees who recently left the organization, showing:
- Employee ID, Job Role, and Department.
- Attrition date, satisfaction score, performance rating, monthly income, and salary hike.Note:Attrition date will show only if you select emp id and attr. date from the slicer.

*This dashboard helps identify trends and potential causes of attrition, such as dissatisfaction in work-life balance or lower job satisfaction, and provides decision-makers with insights to address these issues.*

## Report Snapshot (Power BI DESKTOP)

![Attrition](https://github.com/user-attachments/assets/eeaaf764-3799-48e9-898e-d8900f035875)

## Conclusion

I thoroughly enjoyed working on this project from start to finish. Seeing the entire process unfold offers valuable insight into both the visuals and the data. I’m excited to take on more projects like this and work with even more complex datasets in the future.

