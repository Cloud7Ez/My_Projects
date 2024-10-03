
# Hotel Management analysis using Power Bi

In this project, I worked on a hotel management dataset to gain insights into the hospitality domain. The dashboard highlights key performance indicators, guest satisfaction metrics, revenue trends, and operational insights. By leveraging data visualization techniques, I aimed to provide actionable insights for enhancing guest experiences and optimizing operational efficiency, ultimately contributing to better decision-making in the hospitality industry.

## Dashboard Link(Fabric)

[Interactive Dashboard](https://app.fabric.microsoft.com/view?r=eyJrIjoiMTA4YzU2ODMtNTJiZC00MDAyLWI1YTAtZGQyYzQ3ZTA1ZWMzIiwidCI6ImYyYWY5N2MyLTFiODUtNDQwOC05YTc5LTBjNjI0N2M4YTQ0YiJ9&pageName=9df8f20a45b580365ba7)



## Tech Stack Used 

Powerbi

![Powerbi](https://github.com/user-attachments/assets/d705e3e8-95d9-4609-9a37-cdf7edc8b5b1)

## Data Cleaning

- The raw dataset, provided in .csv format, was imported directly into Power BI, comprising Five tables.
 
- I cleaned the data by ensuring columns were appropriately named, data types were accurate, and confirmed there were no missing values. I then started exploring potential relationships between the tables.

## Data Modeling

Once I confirmed the accuracy and consistency of the data, I proceeded to create a data model. I designated "fact_aggregated_booking" and "fact_booking" as the key tables, then established relationships between fact tables and dimention tables. For this project, I determined that only one-to-many relationships were needed. A visual representation of the final model is also provided for better clarity.

![data model](https://github.com/user-attachments/assets/7c38c8f5-e05f-4d42-a8bd-ae79222cc7e1)


## Dax Functions

With the table relationships in place, I began using DAX functions to analyze the dataset. I started by creating key KPIs such as Total Revenue , Revenue Loss,Average daily rate,Revenue Per Room,Total Capacity,Total Bookings. Some of the most frequently used DAX functions included:

- CALCULATE(): Used to apply new filter contexts, particularly useful for calculating Total Checked out/No Show Bookings and many other measures.
- DISTINCTCOUNT():The DAX DISTINCTCOUNT function returns the count of unique (distinct) values in a column. It is commonly used to eliminate duplicates in the counting process.It is useful for calculating Total Bookings.
- DIVIDE(): The DAX DIVIDE function performs division in a safer way by handling cases where the denominator might be zero or missing, avoiding errors.It is useful for calculating Rates.
- The DAX VAR function is used to define variables within a DAX expression, making the code easier to read and more efficient by avoiding redundant calculations. It is useful for calculating WoW Change rates.

All the measures created were organized into a dedicated Measure Table for easy access.

## Dax Functions that were used are given below:

```
Revenue = SUM(fact_bookings[revenue_realized])

Revenue loss = -SUM(fact_bookings[Revenue_Loss])

Total Guest = SUM(fact_bookings[Total_Guest])

Total Bookings = COUNT(fact_bookings[booking_id])

Total Capacity = SUM(fact_aggregated_bookings[capacity])

Total Succesful Bookings = SUM(fact_aggregated_bookings[successful_bookings])

Occupancy % = DIVIDE([Total Succesful Bookings],[Total Capacity],0)

Average Rating = AVERAGE(fact_bookings[ratings_given])

No of days = DATEDIFF(MIN(dim_date[date]),MAX(dim_date[date]),DAY) +1

Total cancelled bookings = CALCULATE([Total Bookings],fact_bookings[booking_status]="Cancelled")

Cancellation % = DIVIDE([Total cancelled bookings],[Total Bookings])

Total Checked Out = CALCULATE([Total Bookings],fact_bookings[booking_status]="Checked Out")

Total no show bookings = CALCULATE([Total Bookings],fact_bookings[booking_status]="No Show")

No Show rate % = DIVIDE([Total no show bookings],[Total Bookings])

Booking % by Platform = DIVIDE([Total Bookings],
CALCULATE([Total Bookings], 
ALL(fact_bookings[booking_platform])
))

Booking % by Room class = DIVIDE([Total Bookings],
CALCULATE([Total Bookings], 
ALL(dim_rooms[room_class])
))

Average Daily Rate = DIVIDE( [Revenue], [Total Bookings],0)

Realisation % = 1- ([Cancellation %]+[No Show rate %])

Revenue Per Room = DIVIDE([Revenue],[Total Capacity])

Daily Booked Room Nights = DIVIDE([Total Bookings], [No of days])

Daily Sellable Room Nights = DIVIDE([Total Capacity], [No of days])

Daily Utilized Room Nights = DIVIDE([Total Checked Out],[No of days])

---
Revenue WoW change % = 
Var selv = IF(HASONEFILTER(dim_date[wn]),SELECTEDVALUE(dim_date[wn]),MAX(dim_date[wn]))
var revcw = CALCULATE([Revenue],dim_date[wn]= selv)
var revpw =  CALCULATE([Revenue],FILTER(ALL(dim_date),dim_date[wn]= selv-1))

return


DIVIDE(revcw,revpw,0)-1
---

---
Occupancy WoW change % = 
Var selv = IF(HASONEFILTER(dim_date[wn]),SELECTEDVALUE(dim_date[wn]),MAX(dim_date[wn]))
var revcw = CALCULATE([Occupancy %],dim_date[wn]= selv)
var revpw =  CALCULATE([Occupancy %],FILTER(ALL(dim_date),dim_date[wn]= selv-1))

return


DIVIDE(revcw,revpw,0)-1
---

---
ADR WoW change % = 
Var selv = IF(HASONEFILTER(dim_date[wn]),SELECTEDVALUE(dim_date[wn]),MAX(dim_date[wn]))
var revcw = CALCULATE([ADR],dim_date[wn]= selv)
var revpw =  CALCULATE([ADR],FILTER(ALL(dim_date),dim_date[wn]= selv-1))

return


DIVIDE(revcw,revpw,0)-1
---

---

Revpar WoW change % = 
Var selv = IF(HASONEFILTER(dim_date[wn]),SELECTEDVALUE(dim_date[wn]),MAX(dim_date[wn]))
var revcw = CALCULATE([RevPAR],dim_date[wn]= selv)
var revpw =  CALCULATE([RevPAR],FILTER(ALL(dim_date),dim_date[wn]= selv-1))

return


DIVIDE(revcw,revpw,0)-1
---

---
Realisation WoW change % = 
Var selv = IF(HASONEFILTER(dim_date[wn]),SELECTEDVALUE(dim_date[wn]),MAX(dim_date[wn]))
var revcw = CALCULATE([Realisation %],dim_date[wn]= selv)
var revpw =  CALCULATE([Realisation %],FILTER(ALL(dim_date),dim_date[wn]= selv-1))

return


DIVIDE(revcw,revpw,0)-1
---

---
DSRN WoW change % = 
Var selv = IF(HASONEFILTER(dim_date[wn]),SELECTEDVALUE(dim_date[wn]),MAX(dim_date[wn]))
var revcw = CALCULATE([DSRN],dim_date[wn]= selv)
var revpw =  CALCULATE([DSRN],FILTER(ALL(dim_date),dim_date[wn]= selv-1))

return


DIVIDE(revcw,revpw,0)-1
---

```
## Calculated Column That were created is given below:
```
wn = WEEKNUM(dim_date[date])
```

## Data Visualization

This Dashboard contains only Three Pages.

### Home Page:
- Total Revenue: 1,709M৳.This represents the total revenue generated across all properties.
- Revenue Loss: -299M৳.Indicates a significant revenue loss due to cancellations.
- Average Daily Rate (ADR): 12,696৳.The average revenue earned per occupied room per day.
- RevPar (Revenue per Available Room): 7,347৳ Measures the revenue generated per available room, combining both occupancy and ADR.
- Weekly Bookings vs Checked Out vs Cancelled Bookings:Line Graph: Shows trends over time for bookings, check-outs, and cancellations. Each line represents one of these categories, helping to visualize fluctuations and patterns.
- Weekly Trend of Revenue and Revenue Loss:Bar Graph: Displays weekly revenue and revenue loss. Dark bars represent revenue, while light bars indicate revenue loss, allowing for a quick comparison of financial performance week by week.
**Summary Table:**
Property Details: Lists various properties with metrics such as:
- Revenue: Revenue generated by each property.
- Revenue Loss: Revenue Lost by Cancellation.
- Total Booking: How Many Booking each property received.
- Occupancy Rate: Percentage of occupied rooms.
- Cancellation Rate: Percentage of bookings that were canceled.
- Realisation Rate: Succesful "checked out" percentage over all bookings happened.
- ADR (Average Daily Rate): Average revenue per occupied room.
- RevPar (Revenue per Available Room): Revenue per available room.
*Each row in the table represents a different property, with positive values in green and negive values in red, making it easy to identify which properties are performing well and which are not*

### City Page
- Total Guests: 408.7K.This represents the total number of guests across all properties.
- Total Capacity: 232.6K.Indicates the total capacity available across all properties.
- Total Bookings: 135K.The total number of bookings made.
- WoW Revenue and ADR Change Rate by Week:This graph shows the Week-over-Week (WoW) change in revenue and Average Daily Rate (ADR). It helps to track how these metrics are changing over time.
- Total Successful Bookings by City:This graph displays the number of successful bookings in different cities, providing insight into which locations are performing well.
- Average Rating by City:Shows the average rating given by guests in different cities, helping to assess guest satisfaction across locations.
- The Map Highlights various locations within Bangladesh where the properties are situated and which city is making more revenue.
**Property Table:**
- City Wise Property Name lists different properties anlong with their details such as:
- Total Guests: Number of guests at each property.
- Total Capacity: Capacity of each property.
- Revenue: Revenue generated by each property.
- Revenue Loss: Revenue Lost by Cancellation.
- Cancellation Rate: Percentage of bookings that were canceled.
- Realisation Rate: Succesful "checked out" percentage over all bookings happened.
- Occupancy Rate:Total successful bookings percentage happened to the total rooms available(capacity).

### Platform Page
- Total Guests by Booking Platform:This pie chart shows the distribution of guests across different booking platforms, such as direct online bookings, third-party platforms like MakeMyTrip, and others.
- Revenue by Room Class:This Pie Chart displays the revenue generated by different room classes, such as Premium, Presidential, and Standard rooms. It helps to identify which room types are the most profitable.
- Cancellation Rate by Booking Platform:This Bar chart illustrates the cancellation rates for bookings made through various platforms. It highlights which platforms have higher or lower cancellation rates.
- Revenue by Booking Platform:This Bar Chart illustrates the total revenue generated by different booking Platforms.
- Revenue by Property Name:This treemap shows the revenue generated by different properties. Each block represents a property, and the size of the block indicates the revenue contribution of that property.
- Occupancy Rate and Cancellation Rate by Week:This line chart shows occupancy rate and cancellation rate by week.
- Revenue Loss by Week:This line graph shows the weekly revenue loss, helping to identify periods with significant revenue drops and analyze potential causes.


## Report Snapshot (Power BI DESKTOP)

![Home Pg](https://github.com/user-attachments/assets/358a78fe-f295-429d-8dba-d61f1f44d4fd)
![City Pg](https://github.com/user-attachments/assets/2dfa65b1-b32d-4016-bf35-935d4efbd78c)
![Platform Pg](https://github.com/user-attachments/assets/6932a3be-00b3-4fef-adaa-ad3a129acd16)


## Conclusion

I thoroughly enjoyed working on this project from start to finish. Seeing the entire process unfold offers valuable insight into both the visuals and the data. I’m excited to take on more projects like this and work with even more complex datasets in the future.

