
# SuperStore Sales analysis using Power Bi

In this project, I worked on the Superstore Sales dataset to gain insights into sales performance. By analyzing trends across regions, states, and product categories, I identified key drivers and opportunities for growth. This analysis provides a clear understanding of top-performing areas and highlights potential strategies for optimizing overall sales.
## Dashboard Link(Fabric)

[Interactive Dashboard](https://app.fabric.microsoft.com/view?r=eyJrIjoiZTI3YjA3MGMtYTY0Zi00ZWRkLWFhMWMtZjVhMjQ5MzY1YzRkIiwidCI6ImYyYWY5N2MyLTFiODUtNDQwOC05YTc5LTBjNjI0N2M4YTQ0YiJ9&pageName=ce2c7f5f81d829faa9a5)


## Tech Stack Used 

Powerbi

![Powerbi](https://github.com/user-attachments/assets/d705e3e8-95d9-4609-9a37-cdf7edc8b5b1)

## Data Source
The dataset can be accessed on Kaggle via this [link](https://data.world/vizwiz/superstore-2023)

## Data Cleaning

- The raw dataset, provided in .xls format, was imported directly into Power BI, it has three sheets but for analysis I imported orders sheet.
 
- I cleaned the data by ensuring columns were appropriately named, data types were accurate, and confirmed there were no missing values. 

- As there is no date table I used a external tool called **Bravo** to create the order_calender table. 

## Data Modeling

Once I confirmed the accuracy and consistency of the data, I proceeded to create a data model. I designated "order" table as the  key table, then established relationships between fact tables and dimention tables. For this project, I determined that only one-to-many relationships were needed. A visual representation of the final model is also provided for better clarity.

![Data model](https://github.com/user-attachments/assets/abcc7b15-b12d-4a57-b8dc-11dbd67b5c2b)


## Dax Functions

With the table relationships in place, I began using DAX functions to analyze the dataset.Some of the most frequently used DAX functions included:

- SUM(): The SUM() function in DAX  is used to calculate the total of all values in a column that contains numerical data.It is used to calculate total sales.
- CONCATENATE(): The CONCATENATE() function in DAX is used to join (or concatenate) two text strings into a single text string. This is useful when you want to combine text from multiple columns or create custom labels in Power BI reports.
- SELECTEDVALUES(): The SELECTEDVALUE is a DAX function that returns the value from a column when exactly one value is selected (or filtered) in the current context.If there is more than one value or no value selected, it returns a default value (which can be set optionally) or BLANK().It is used to calculate Selected year.
- INT(): This function converts the selected value to an integer. It ensures that the year is treated as an integer data type rather than a string or decimal.
- The DAX VAR function is used to define variables within a DAX expression, making the code easier to read and more efficient by avoiding redundant calculations. It is useful for calculating Sales YoY% change.

All the measures created were organized into a dedicated Measure Table for easy access.

## Dax Functions that were used are given below:

```
Total Sales = SUM('Order'[Sales])

Showing Sales Text = CONCATENATE("Showing Sales For : ",[Selected Year])

Selected Year = INT(SELECTEDVALUE(Order_calender[Year]))

Sales YoY% = 
IF(
   ISFILTERED(Order_calender[Date]), 
   ERROR("Time intelligence quick measures can only be grouped or filtered by the Power BI_provided datee hierarchy or primary date column."),
VAR __PREV_YEAR = CALCULATE(SUM('Order'[Sales]), DATEADD('Order_calender'[Date], -1, YEAR))
RETURN
	DIVIDE(SUM('Order'[Sales]) - __PREV_YEAR, __PREV_YEAR)
    )

Blank = ""

```


## Data Visualization

This dashboard is a single-page report where I've highlighted key business insights through various visualizations. It provides a clear and concise overview of the data, allowing for easy analysis of important metrics at a glance.

**Sales By Region:** This section provides a comparison of total sales across four regions: Central, East, South, and West.The small line charts under each region show the sales trend for that region.

**Sales By State:** A map visualization showing sales distribution by state. Larger circles indicate higher sales.Below the map, there’s a table listing key states (California, New York, Texas, Washington) with their sales numbers, but their Year-over-Year (YoY) growth rate.

**Sales By Category:** This horizontal bar chart shows sales figures by product category (Technology, Furniture, Office Supplies).Technology has the highest sales, while Office Supplies has the lowest.

**Sales Trend By Category:** A line chart that displays the sales trends for each product category (Technology, Furniture, Office Supplies) across the year. It shows how sales have fluctuated by Time.

**Sales Heatmap By Subcategory:** A heatmap showing sales performance by subcategory (e.g., Phones, Chairs, Storage) across different months.Darker shades indicate higher sales for that subcategory in a specific month.

**Sales By Subcategory:** A horizontal bar chart listing various subcategories (e.g., Phones, Chairs, Storage) and their respective sales figures.Phones and Chairs are the top-selling subcategories. 

**Sales By Segment:** This section displays sales figures broken down by customer segments (Home Office, Corporate, Consumer).The Consumer segment leads in sales, followed by Corporate and Home Office.It also shows YoY% sales of the segments.

**Top 10 Customers by Sales:** A bar chart listing the top 10 customers by sales amounts. It shows the names of customers and how much they contributed to total sales.Sean Miller appears to be the top customer in terms of sales.

Each section of the dashboard provides insights into different aspects of sales performance, including sales distribution by geography, category, segment, and individual customers.



## Report Snapshot (Power BI DESKTOP)
![Main ](https://github.com/user-attachments/assets/38985abc-2ebb-4549-90e5-c817fe5aec36)


## Conclusion

I thoroughly enjoyed working on this project from start to finish. Seeing the entire process unfold offers valuable insight into both the visuals and the data. I’m excited to take on more projects like this and work with even more complex datasets in the future.

