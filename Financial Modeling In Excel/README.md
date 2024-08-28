
# Financial Modeling

## Project Description
As a junior analyst for Streit, a fictional real estate investment trust (REIT), I am tasked with evaluating whether an apartment building in Downtown Detroit is a good investment. REITs manage and operate properties on behalf of investors, and my role involves using financial modeling skills to make this decision.

## What is a Financial Model
Financial modeling is the process of creating a mathematical representation of a real-world financial situation. These models are used to make predictions or analyze financial performance, typically combining historical data with assumptions to produce numerical results. They aim to answer specific questions posed by the analyst and can vary in form depending on the objective.

## Financial model color coding
Financial models can be complex, so it's important to keep them organized in Excel. One best practice is to color-code cells to make it easier to follow:
- Blue fonts: For hardcoded inputs and assumptions (independent variables).
- Black fonts: For calculations, outputs, and cell references within the same sheet (dependent variables).
- Green fonts: For cell references to another worksheet within the same Excel workbook.
- Red fonts: For any external links or references, such as to external workbooks.

## Tech Stack Used 
![Excel](https://img.icons8.com/color/256/microsoft-excel-2019.png)

## Skills showcased in this Project
- Making a Financial Model
- Excel Functions- Hlookup,NPV,XNPV,IRR,XIRR
## The steps followed to create the model are outlined below:

### Step 1
My initial task is to finalize an acquisitions model to evaluate the purchase of West Ridge North, a dilapidated apartment complex that Streit wants to buy, renovate, and make habitable. The seller, Shady Tree Management, has supplied an income statement for the previous year, and it's my responsibility to calculate the subtotals and net income.I used the SUM function to calculate the totals.
```
   SUM(___,___,___)
```
- Rental income pertains to the revenue collected from tenants. In real estate, it’s typical to display the total potential rent for the property and then subtract any uncollected rent due to non-payments or vacancies.Total Rental Income = Net Potential Rent + Vacancy + Delinquency
- Total Operating Expenses encompass all costs associated with the day-to-day operations of the business.
- Net Operating Income (NOI) is the income remaining after all expenses related to day-to-day business operations have been paid. NOI=Total Rental Income−Total Operating Expenses
- Capital expenditures are costs associated with acquiring or renovating property. These investments enhance the property’s longevity beyond routine maintenance.
- Net income is the remaining income after all expenses have been settled, representing the profit for the period.Net Income=Net Operating Income−Total Capital Expenditures

1|2| 
:-------------------------:|:-------------------------:
![1](https://github.com/user-attachments/assets/9ea13164-eb22-4650-a141-60fe392eb4b9)|![2](https://github.com/user-attachments/assets/288a2e6a-7411-4db0-980c-8b187fbb0eaa)

### Step 2
Real estate investors use the capitalization rate (cap rate) to determine their investment yield. The cap rate formula is:Cap rate=Net operating income/Property value.To find the property value, rearrange the formula:Property Value=Net Operating Income/Cap Rate.Streit has notified me that their target cap rate is 6.00%.Using this in the Acqusitions Details I have calculated the purchase price .

1|2| 
:-------------------------:|:-------------------------:
![1](https://github.com/user-attachments/assets/b3401760-d526-4409-bc9f-2dc65ec1c644)|![2](https://github.com/user-attachments/assets/5696c789-bdd3-476d-833c-602f6ec29500)

In our financial model, Year 0 is designated for acquisition costs because, at this point, no other income or expenses have yet been accrued. This represents the precise moment the property is purchased.I entered the purchase price in the property purchase column and, since it was an expense, I recorded it as a negative amount.I also applied a custom format to add "Year" text before the 0.
```
   "Year" 0
```

1|2| 
:-------------------------:|:-------------------------:
![1](https://github.com/user-attachments/assets/7176979f-50e8-4113-8d74-ee535f962847)|![2](https://github.com/user-attachments/assets/50708730-0395-4d59-a919-a4fc9ed17b2c)

### Step 3
Financial models are commonly used to assess an investment over time, incorporating assumptions to estimate future revenue and expenses. Growth rates help project these figures into the future. To calculate the future value with a growth rate, use the formula:Future Value=Previous Value*(1+Rate).

I copied the subtotal formulas from column B to the corresponding rows in columns D through N to calculate values for Year 0 through Year 10. This includes all subtotals:Total Rental Income,Total Operating Expenses,Net Operating Income,Total Capital Expenditures,Net Income.

Added some inputs to the Operational Assumptions section in the top of the sheet:
-	Added 2% for Cost Growth %.
-	Added 5% for Rent Growth %.
1|2| 
:-------------------------:|:-------------------------:
![1](https://github.com/user-attachments/assets/21f99c5b-251b-49ac-bcd7-5ca2facee61d)|![2](https://github.com/user-attachments/assets/8af8a80c-7fbe-4e27-bd01-587f103c6fd8)

Streit plans to remodel all units in the first year and start renting them in Year 2 for $2,300 per month. Rent is expected to increase annually based on the Rent Growth % assumption.

- I entered $2,300 in cell F19 to specify the rental income for Year 2.
- I created a formula in cell G19 to forecast rental income using the growth rate formula: : Previous Value * (1 +Rent Growth %). , ensuring the cell reference for Rent Growth % is locked.
- I dragged this formula across to cell N19 to extend the analysis through Year 10.

1|2| 
:-------------------------:|:-------------------------:
![1](https://github.com/user-attachments/assets/d86b5fa8-5d3b-479a-932a-6fdbd5404dfb)|![2](https://github.com/user-attachments/assets/c6ceafd9-1f50-4b8b-82b0-f3a1c1398b51)

Now that we know the monthly rent for each unit, we can calculate the net potential rent for each year. Net potential rent is simply the total amount of rent that could be potentially earned by the entire property.
To calculate the net potential rent for each year:

- In cell F18, I determined the Net Potential Rent by multiplying the value in F19 (monthly rent per unit) by the "Units" named range.
- Since the rent amount is monthly, I converted it to an annual figure by multiplying by 12.
- I then dragged this formula across to cell N18 to extend the analysis through Year 10.
1|2| 
:-------------------------:|:-------------------------:
![1](https://github.com/user-attachments/assets/16c60847-b8eb-4b66-a491-85a92db9caa2)|![2](https://github.com/user-attachments/assets/5aaf9eaf-592d-45f2-ac73-4d8ae219a38f)

### Step 4
To enable Streit's Chief Investment Officer to analyze the predicted sales price of West Ridge North for any year, we can use the cap rate formula:: Property Value = Net Operating Income/Cap Rate.

Streit told me to put these value in the Sales Details at the top of the worksheet:
- Holding Period (Years): 5.
- Exit Cap Rate: 6.00%.

1|2| 
:-------------------------:|:-------------------------:
![1](https://github.com/user-attachments/assets/4b8587f4-6937-4e0b-b324-8f9fe0a921bb)|![2](https://github.com/user-attachments/assets/c0a7a04c-abcb-4674-98c3-9c4122fe8250)

To make the sales price calculation dynamic, I used the HLOOKUP() function to locate the net operating income for the year that matches the Holding Period (Years) assumption. Under the Sale Details in cell F8, I used HLOOKUP() as follows:

- The Holding Period (Years) is the lookup value.
- The table array is D16 through N46.
- The row index number corresponds to the last row in the table array.
- The range lookup is set to find an exact match.

https://github.com/user-attachments/assets/f62118d1-9d5d-45f5-b6d7-a20d91c5d8b8 













