
# Adventure Works sales data analysis using Power Bi

I worked on a project with the Adventure Works dataset, focusing on analyzing sales and returns data for a bike manufacturing and selling company. This was a comprehensive project that covered the entire process, from importing and cleaning the data to building and optimizing visualizations in Microsoft Power BI Desktop.

## Dashboard Link(Fabric)

[Interactive Dashboard](https://app.fabric.microsoft.com/view?r=eyJrIjoiN2Q1NjU4MDItN2ZhNC00YmMwLWIyN2QtYzIxZTU1NDQzOGRmIiwidCI6ImYyYWY5N2MyLTFiODUtNDQwOC05YTc5LTBjNjI0N2M4YTQ0YiJ9&pageName=ecd649667193a78fe19e)



## Tech Stack Used 

Powerbi

![Powerbi](https://github.com/user-attachments/assets/d705e3e8-95d9-4609-9a37-cdf7edc8b5b1)

## Data Source
The dataset can be accessed on Kaggle via this [link](https://www.kaggle.com/datasets/atulmittal199174/adventure-works-dataset)

## Data Cleaning

The raw dataset, provided in .csv format, was imported directly into Power BI, comprising eight separate tables. After an initial review, I identified that the focus would be on Sales and Returns data. I cleaned the data by ensuring columns were appropriately named, data types were accurate, and confirmed there were no missing values. I then started exploring potential relationships between the tables.

## Data Modeling

Once I confirmed the accuracy and consistency of the data, I proceeded to create a data model. I designated ‘Sales Data’ and ‘Returns Data’ as the key tables, then established relationships between them. For this project, I determined that only one-to-many relationships were needed. A visual representation of the final model is also provided for better clarity.

![Data Model](https://github.com/user-attachments/assets/5128cfda-f55d-46a5-b5a0-163d47aaf456)

## Dax Functions

With the table relationships in place, I began using DAX functions to analyze the dataset. I started by creating key KPIs such as Revenue, Profit, and Total Orders, which served as the foundation for more advanced metrics. Some of the most frequently used DAX functions included:

- Iterator Functions (SUMX): These evaluate an expression for each row and aggregate the results.
- CALCULATE(): Used to apply new filter contexts, particularly useful for calculating Previous Months Orders, Revenue, Profit, Returns, and Overall Average Price.
- RELATED(): Pulls data from other tables when a many-to-one relationship exists.
- Date Functions (DateAdd): Essential for calculating metrics like Previous Month’s Orders, Profit, Revenue, and Returns.

All the measures created were organized into a dedicated Measure Table for easy access.


## Dax Functions that were used are given below:

```
Total Customer = 
DISTINCTCOUNT('Fact Sales'[CustomerKey])

Total Orders = 
DISTINCTCOUNT('Fact Sales'[OrderNumber])

Total Revenue = 
SUMX('Fact Sales',
'Fact Sales'[Order Quantity]
*
RELATED('Product Lookup'[Product Price])
)

Total Cost = 
SUMX(
    'Fact Sales',
    'Fact Sales'[Order Quantity]
    *
    RELATED(
        'Product Lookup'[Product Cost]
    ))
    
Profit = [Total Revenue]-[Total Cost]

Profit Margin = DIVIDE([Profit],[Total Revenue])

Quantity Sold = SUM('Fact Sales'[Order Quantity])

Quantity Returned = 
SUM('Fact Return'[ReturnQuantity])

Total Returns = 
COUNTROWS('Fact Return')

Return Rate = 
DIVIDE([Total Returns],[Total Orders])

Avg. Order Value = 
DIVIDE([Total Revenue],[Total Orders]
)

Avg. Revenue Per Customer = 
DIVIDE([Total Revenue],[Total Customer])

Average Retail Price = AVERAGE('Product Lookup'[Product Price])

Previous Month Revenue = 
CALCULATE([Total Revenue],
DATEADD('Calendar Lookup'[Date],-1,MONTH)
)

Previous Month Orders = 
CALCULATE([Total Orders],
DATEADD('Calendar Lookup'[Date],-1,MONTH))

Previous Month Return = 
CALCULATE([Total Returns],
DATEADD('Calendar Lookup'[Date],-1,MONTH))

Previous Month Profit = 
CALCULATE([Profit],
DATEADD('Calendar Lookup'[Date],-1,MONTH))

Order Target = [Previous Month Orders] * 1.1

Order Target Gap = [Total Orders]-[Order Target]

Profit Target = [Previous Month Profit] * 1.1

Profit Gap = [Profit]-[Profit Target]

Revenue Target = [Previous Month Revenue] * 1.1

Revenue Target Gap = [Total Revenue]-[Revenue Target]

Adjusted Price = [Average Retail Price]*(1+'Price Adjustment(%)'[Price Adjustment(%) Value])

Adjusted Revenue = SUMX('Fact Sales',
'Fact Sales'[Order Quantity]*[Adjusted Price])

Adjusted Price = [Average Retail Price]*(1+'Price Adjustment(%)'[Price Adjustment(%) Value])

Weekend Sales = 
CALCULATE([Total Orders],
'Calendar Lookup'[Weekend ] = "Weekend") 


```
## Calculated Columns and Parameters that were used are given below:

**Customer Parameters:**
- Added Customer Metrics Using New Field Parameters .
```
Customer_Metrics = {
    ("Total Custome", NAMEOF('_Measures'[Total Customer]), 0),
    ("Avg. Revenue Per Customer", NAMEOF('_Measures'[Avg. Revenue Per Customer]), 1)
}
```
**Product Parameters:**
- Added Product Metrics Using New Field Parameters .
```
Product_Metrics = {
    ("Orders", NAMEOF('_Measures'[Total Orders]), 0),
    ("Returns", NAMEOF('_Measures'[Total Returns]), 1),
    ("Revenue", NAMEOF('_Measures'[Total Revenue]), 2),
    ("Profit", NAMEOF('_Measures'[Profit]), 3),
    ("Profit Margin (%)", NAMEOF('_Measures'[Profit Margin]), 4),
    ("Return Rate (%)", NAMEOF('_Measures'[Return Rate]), 5)
}
```

**Price Adjustment Parameters:**
- Added Price adjustment(%) Using Numeric Range Parameters

```
Price Adjustment(%) = GENERATESERIES(-1, 1, 0.1)

Price Adjustment(%) Value = SELECTEDVALUE('Price Adjustment(%)'[Price Adjustment(%)], 0)
```
------------------------------------------------------

- Added Order type in Fact Sales Table.

```
Order Type = 
IF(
    'Fact Sales'[Order Quantity]>1,
    "Bulk Order",
    "Single Order"
)

```
------------------------------------------------------

**Product Lookup Table:**

- Added Price Point .
```
Price Point = 
SWITCH(
    TRUE(),
    'Product Lookup'[Product Price] > 500 ,"High",
    'Product Lookup'[Product Price] > 100, "Mid-Range",
    "Low"
)
```
------------------------------------------------------

**Customer Lookup Table:**

- Added Is Parent.
```
Is Parent = 
IF('Customer Lookup'[Total Children] > 0 , "Yes",
"No")
```
- Added Customer Priority.
```
Customer Priority = 
IF('Customer Lookup'[Annual Income] > 100000
&&
'Customer Lookup'[Is Parent] = "Yes",
"Priority","Standard"
)
```
- Added Education Category.
```
Education Category = 
SWITCH(
    'Customer Lookup'[Education Level],
    "High School","High School",
    "Partial High School","High School",
    "Bachelors","Undergrad",
    "Graduate Degree","Graduate"
    )
```
- Added Income Lavel

```
Income Level = 
IF('Customer Lookup'[Annual Income] >= 150000,"Very High",
 IF('Customer Lookup'[Annual Income] >= 100000,"High",
   IF('Customer Lookup'[Annual Income] >= 50000, "Average",
     "Low")))
```     

## Data Visualization

A total of 4 visualization pages were created for this report, these include:

**1.Executive Dashboard:** Home to company wide KPI’s, Trending Revenue, Orders as well as several lists of the top selling products.

- This dashboard is meant to be a general overview of company performance for anyone to understand.
- A slicer Panel located in the top left is also available to further filter down visuals based on the year and continent providing a more granular look at the most important KPI’s.

**2.Map:** This is an interactive visual of the company’s order distribution throughout the world broken down by continent.

- Some key insights found from this were that while the United States makes up the majority of Adventure Work’s Orders (8,700), the Pacific shares a significant share of the total orders as well (6,060).
- Additionally, no sales have taken place in Asia, Africa, or South America indicating a potential for new markets to break into.

**3.Product Details:** This page provided an in-depth and interactive look at the relationship between the products of Adventure Works and their respective revenue, orders, profit, return percentage and returns.

- By drilling through from the Exec Page for a selected product, we can view its monthly targets for Orders, Revenue, or Profit.
- In the bottom area chart, we can also view the profit and adjusted profit if a price adjustment is made. Additionally,we can displays the product's orders, returns, revenue, profit, profit margin, and return rate.

**4.Customer Details:** Multiple visuals of the relationship between customers and business metrics can be found on this page.

- On this page I was able to break our customers down by demographic including occupation and income as represented in the Donut Charts in the bottom left.
- A steep increase in total customers can be seen in July 2021 which can possibly explained by it being the summer months with biking being more popular.
- The Top 100 Customers Table has several interesting factors. In addition to providing an overview of the Top 100 customers, it also provides their total orders and it was here that some interesting insights were found.
- Take for example, the top customer displayed in the bottom right corner or first row of the table. Mr. Shan was able to secure the top position in terms of Revenue with only 6 total orders. In fact, the top 5 customers all created Revenue greater than 11,000$ and all did this with 7 or less orders.


## Report Snapshot (Power BI DESKTOP)

![Snip 1](https://github.com/user-attachments/assets/6bed4357-4a5a-4753-b8b5-4b4b25d5b133)
![Snip 2 ](https://github.com/user-attachments/assets/8d37e0fd-2593-47df-9f43-aca14b93c664)
![Snip 3](https://github.com/user-attachments/assets/8cfe36ea-f09f-4606-ad5e-26412bf70745)
![Snip 4](https://github.com/user-attachments/assets/7b355758-5ac7-4625-872a-723f39ffdc0e)

## Conclusion

I thoroughly enjoyed working on this project from start to finish. Seeing the entire process unfold offers valuable insight into both the visuals and the data. I’m excited to take on more projects like this and work with even more complex datasets in the future.

