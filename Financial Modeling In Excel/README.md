
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

------------------------------------------------------

In our financial model, Year 0 is designated for acquisition costs because, at this point, no other income or expenses have yet been accrued. This represents the precise moment the property is purchased.I entered the purchase price in the property purchase column and, since it was an expense, I recorded it as a negative amount.I also applied a custom format to add "Year" text before the 0.
```
   "Year" 0
```

1|2| 
:-------------------------:|:-------------------------:
![1](https://github.com/user-attachments/assets/7176979f-50e8-4113-8d74-ee535f962847)|![2](https://github.com/user-attachments/assets/50708730-0395-4d59-a919-a4fc9ed17b2c)

### Step 3
Financial models are commonly used to assess an investment over time, incorporating assumptions to estimate future revenue and expenses. Growth rates help project these figures into the future. To calculate the future value with a growth rate, use the formula:Future Value=Previous Value*(1+Rate).

------------------------------------------------------

I copied the subtotal formulas from column B to the corresponding rows in columns D through N to calculate values for Year 0 through Year 10. This includes all subtotals:Total Rental Income,Total Operating Expenses,Net Operating Income,Total Capital Expenditures,Net Income.

------------------------------------------------------

Added some inputs to the Operational Assumptions section in the top of the sheet:
-	Added 2% for Cost Growth %.
-	Added 5% for Rent Growth %.
1|2| 
:-------------------------:|:-------------------------:
![1](https://github.com/user-attachments/assets/21f99c5b-251b-49ac-bcd7-5ca2facee61d)|![2](https://github.com/user-attachments/assets/8af8a80c-7fbe-4e27-bd01-587f103c6fd8)

------------------------------------------------------

Streit plans to remodel all units in the first year and start renting them in Year 2 for $2,300 per month. Rent is expected to increase annually based on the Rent Growth % assumption.

- I entered $2,300 in cell F19 to specify the rental income for Year 2.
- I created a formula in cell G19 to forecast rental income using the growth rate formula: : Previous Value * (1 +Rent Growth %). , ensuring the cell reference for Rent Growth % is locked.
- I dragged this formula across to cell N19 to extend the analysis through Year 10.

1|2| 
:-------------------------:|:-------------------------:
![1](https://github.com/user-attachments/assets/d86b5fa8-5d3b-479a-932a-6fdbd5404dfb)|![2](https://github.com/user-attachments/assets/c6ceafd9-1f50-4b8b-82b0-f3a1c1398b51)

------------------------------------------------------

Now that we know the monthly rent for each unit, we can calculate the net potential rent for each year. Net potential rent is simply the total amount of rent that could be potentially earned by the entire property.
To calculate the net potential rent for each year:

- In cell F18, I determined the Net Potential Rent by multiplying the value in F19 (monthly rent per unit) by the "Units" named range.
- Since the rent amount is monthly, I converted it to an annual figure by multiplying by 12.
- I then dragged this formula across to cell N18 to extend the analysis through Year 10.
1|2| 
:-------------------------:|:-------------------------:
![1](https://github.com/user-attachments/assets/16c60847-b8eb-4b66-a491-85a92db9caa2)|![2](https://github.com/user-attachments/assets/5aaf9eaf-592d-45f2-ac73-4d8ae219a38f)

### Step 4
To enable Streit's Chief Investment Officer to analyze the predicted sales price of West Ridge North for any year, we can use the cap rate formula: Property Value = Net Operating Income/Cap Rate.
------------------------------------------------------
Streit told me to put these value in the Sales Details at the top of the worksheet:
- Holding Period (Years): 5.
- Exit Cap Rate: 6.00%.

1|2| 
:-------------------------:|:-------------------------:
![1](https://github.com/user-attachments/assets/4b8587f4-6937-4e0b-b324-8f9fe0a921bb)|![2](https://github.com/user-attachments/assets/c0a7a04c-abcb-4674-98c3-9c4122fe8250)

------------------------------------------------------

To make the sales price calculation dynamic, I used the HLOOKUP() function to locate the net operating income for the year that matches the Holding Period (Years) assumption. Under the Sale Details in cell F8, I used HLOOKUP() as follows:

- The Holding Period (Years) is the lookup value.
- The table array is D16 through N46.
- The row index number corresponds to the last row in the table array.
- The range lookup is set to find an exact match.

------------------------------------------------------

Now I can calculate the sales price using the cap rate formula from before: Property Value = Net Operating Income/Cap Rate.
-	Divided the formula in F8 by the Exit Cap Rate.

https://github.com/user-attachments/assets/f62118d1-9d5d-45f5-b6d7-a20d91c5d8b8 

------------------------------------------------------

To make the financial model truly dynamic, I used an IF() statement to display the Sell Price for the appropriate year in the Property (Purchase) Sale line item.
```
IF(HoldingPeriod=E16,SalePrice,0)

```

- In cell E48, I used an IF() function that displays the Sell Price if the Holding Period matches the year in row 16.
- I locked the cell references for the Sell Price and Holding Period.
- If the condition is false, the value is set to 0.
- I then dragged this formula across columns E to N to extend it through Year 10.

https://github.com/user-attachments/assets/ca1adc5a-3cb9-45c9-b1fa-336962c15125
https://github.com/user-attachments/assets/8674849a-dbb0-4b1d-ba6c-cab18b1dfa49

## Step 5 (Scenario Manager)
The Scenario Manager in Excel is a tool that organizes different scenarios and their input changes, making it easier to compare them.
------------------------------------------------------
The first scenario I created will keep our model unchanged, allowing us to easily return to these values.
- I added a new scenario in the Scenario Manager called "Expected Rent."
- I set the Rent Growth % in B10 to 0.05 and the Starting Rent in F19 to 2300.
------------------------------------------------------
Next, I created another scenario with higher rent growth and rent amount assumptions.
- I added a new scenario named "High Rent."
- I set B10 to 0.08 and F19 to 2500.
------------------------------------------------------
Now that the scenarios were set up, I used the manager to compare net operating income for Year 10.
- I reviewed the different scenarios by clicking "Show" for each one.
- I used the Scenario Manager to create a summary of the scenarios, using the net operating income for Year 10 in cell N46 as the result.

https://github.com/user-attachments/assets/0332a431-dbc9-48d9-b894-bd4cb7b30802

## Step 6 (Goal Seek)
Manually changing inputs is a fine way to use a financial model, but what if we had a target or goal and wanted to know how much an input would need to change in order to meet it? The Goal Seek tool is especially useful in this case.

 ------------------------------------------------------

Streit asked me to determine what our starting rent would need to be in order to achieve $5M in net operating income by Year 10 under our Expected Rent scenario.
- I used the Scenario Manager to display the Expected Rent scenario.
- Then, I applied Goal Seek to determine what the Starting Rent in F19 would need to be for the Net Operating Income in N46 to reach $5,000,000.
https://github.com/user-attachments/assets/e143ef8e-8489-48ea-b57e-095ea68f9e91

 ------------------------------------------------------

Interesting,starting rent would need to be $3,655 to achieve a net operating income of $5M with the current Rent Growth %. But what if we adjusted the Rent Growth % instead of the Starting Rent to see the impact?

- I used the Scenario Manager to display the Expected Rent scenario.
- Then, I applied Goal Seek to find out what Rent Growth % in B10 would need to be for the Net Operating Income in N46 to reach $5,000,000.
https://github.com/user-attachments/assets/332bfdce-c70d-4924-bd37-f04549ebd242

## Step 7 (Sensitivity analysis)
We've explored some interesting what-if analyses by changing inputs one at a time, but there must be a more efficient way. Data Tables are excellent for sensitivity analysis, allowing us to examine how a range of input changes affects the output.

------------------------------------------------------

Streit asked me to conduct a sensitivity analysis on how the Rent Growth % affects net operating income. Here’s what I did:

- I used the Scenario Manager to reset the model to the Expected Rent scenario.
- In cells A58,I created a list starting at 0.00% and ending at 10.00% in increments of 2.50%.
- I formatted these cells as percentages with 2 decimal places.
- I set B57 to equal N46 to reference the output variable.
- I ran the Data Table analysis.
- I used the Rent Growth % in B10 as the column input variable.
- I left the row input variable empty.
- I formatted the results as numbers with 0 decimal places.
https://github.com/user-attachments/assets/2f3133d9-7a0d-402f-8b2e-4cb48d0a64b1

------------------------------------------------------

The real strength of Data Tables emerges when analyzing multiple variables. While we've seen how to perform sensitivity analysis with a single input, it's also valuable to explore how two inputs interact and affect the dependent variable. Streit asked me to examine how changes in our Rent Growth % and Starting Rent assumptions influence net operating income.

- I deleted cells B57 from the data table, leaving only the list of percentages from 0.00% to 10.00%.
- In cells B57,I created a row of numbers ranging from 2,000 to 3,000 in increments of 250.
- I formatted these numbers as standard currency with 0 decimal places.
- Next, I set A57 equal to N46 to reference the output variable, and then I ran the Data Table analysis:
- I used Starting Rent in F19 as the row input and Rent Growth % in B10 as the column input.
- I formatted the results as standard currency with 0 decimal places.
- Finally, I applied a color scale using the conditional formatting options.
https://github.com/user-attachments/assets/5ee388b5-2322-4258-bb62-caa9d5111c6f

## Step 8 (Return on investment)
Return on Investment (ROI) is a key profitability ratio that measures the profit generated per dollar invested. The formula is ROI = Total Return / Investment Amount. This metric is popular because it’s straightforward to calculate and easy to comprehend.

------------------------------------------------------

In the new section H1 to J10 titled "Profit Metrics", Streit has asked me to calculate the return on investment (ROI) for acquiring West Ridge North.

------------------------------------------------------

The first step is to identify the total amount invested, which will be our capital expenditures.
- I calculated the Total Investment in J2 by adding the Capital Expenditures from row 51 for Year 0 and Year 1. I used ABS() to make the Total Investment positive since the amount was negative.
```
  ABS(SUM(D51,E51)) 

```

https://github.com/user-attachments/assets/aade0383-3c3a-45f6-a2b3-abfaf5df1f64
------------------------------------------------------

The second step is to calculate the total return earned in each period, which does not include the capital expenditures since these are a part of our investment amount.
- In J3, I calculated the Total Return by summing the net income from row 53 for all years and then adding the Total Investment in J2 to account for the capital expenditures included in the net income.
```
SUM(D53:N53)

```
https://github.com/user-attachments/assets/1ed64989-7b4c-40c2-a77f-0b2261b0e74f
------------------------------------------------------

Finally, I calculated the return on investment (ROI) in J4 using the formula ROI = Total Return / Total Investment.

https://github.com/user-attachments/assets/22ec1695-b0cf-46c6-a6cc-65025170621c

------------------------------------------------------

## Step 9 (Future Value)
Benchmarks are a point of reference that can be used as a comparison.

------------------------------------------------------

Streit's Chief Investment Officer asked us to determine if a benchmark rate of 20.00% could be applied. I used the FV() function to calculate the future value of the investment amount based on this benchmark rate and the investment horizon.

```
FV(C2,C3,,-C4,)

```
------------------------------------------------------

First, I set the benchmark rate in J5 to 20.00%.On the TMV Analysis sheet, I started filling in the assumptions under Future Value in column C:

- C2 referenced the benchmark rate from Analysis!J5.
- C3 referenced the holding period from Analysis!F6.
- C4 referenced the investment amount from Analysis!J2.

https://github.com/user-attachments/assets/b117f773-e0b9-430e-b24a-87bbfea5ca83


## Step 10(Present Value)
The present value determines the amount needed to be invested at a specific rate and time to achieve a future return. The Chief Investment Officer requested a benchmark test using present value. If the total investment in West Ridge North is less than the present value amount, it indicates a good investment. This is because investing more at 20.00% would be necessary to match the same return as West Ridge North.I used the PV() function to calculate the Present value.

```
PV(G2,G3,,-G4)

```
------------------------------------------------------

On the TMV Analysis sheet, I began filling in the assumptions under Future Value in column G:

- G2 referenced the benchmark rate from Analysis!J5.
- G3 referenced the holding period from Analysis!F6.
- G4 referenced the total return from Analysis!J3.

https://github.com/user-attachments/assets/7a1ad74f-9484-4775-92ff-73ec0f7e4ee9


## Step 11(Net Present Value)
The Chief Investment Officer asked us to find the net present value (NPV) of the total net income earned over the lifetime of West Ridge North. I used the NPV() function to do this:
```
NPV(J5,E53:N53)+D53

```
- In J8, I applied NPV() to calculate the net present value of the net income cash flows from row 53 for Year 1 through Year 10.
- I used the benchmark rate in J5 as the rate input.
- I added the net income cash flow from Year 0 to the end of the formula.

https://github.com/user-attachments/assets/c288ed63-b2c8-41f2-bc32-916e0eac3428

------------------------------------------------------

We encountered a limitation with NPV() because it treated Year 0 as Year 1, not accounting for the exact timing of cash flows. We switched to using XNPV(), which is better for handling time series data and provides more precise calculations, as it doesn't require periods to be the same.

```
XNPV(J5,D53:N53,D15:N15)

```
------------------------------------------------------

To prepare for using XNPV(), I first provided it with dates:

- In D15, I added the date January 31, 2024, formatted it as a Short Date, and centered it in the cell.
- In E15, I used the EOMONTH() function to find the date 12 months after D15.
- I applied this formula to generate dates for the rest of the years.

https://github.com/user-attachments/assets/6a9883e6-5e10-441d-9599-f7690041ad54

------------------------------------------------------

Now that the dates are set up, I used the XNPV() function as follows:

- In J9, I applied XNPV() to calculate the net present value of the net income cash flows from row 53, using the date ranges created and the benchmark rate as the rate.
- I formatted the result as currency with 0 decimal places.

https://github.com/user-attachments/assets/90335f30-9a25-4c5c-9720-66947efa3b3c

## Step 12(Internal rate of return)
The internal rate of return (IRR) provides the discount rate that makes the net present value (NPV) equal to zero. It also represents the project's annualized rate of return.

------------------------------------------------------

Streit's Chief Investment Officer asked me to find the internal rate of return for West Ridge North as the final test of the project's profitability.In J10, I used the IRR() function to calculate the internal rate of return for the net income cash flows in row 53.
```
IRR(D53:N53,)

```
https://github.com/user-attachments/assets/633e9f49-45bc-4775-b7e6-97abd01ca885

------------------------------------------------------

Since we have dates associated with each cash flow, XIRR() would be a more precise function.In J11, I used the XIRR() function to calculate the internal rate of return for the net income cash flows in row 53, providing a more precise result given the associated dates.
```
XIRR(D53:N53,D15:N15,)

```
https://github.com/user-attachments/assets/9a5a650a-3844-47a7-b34d-5c1883dfae1d

## End










