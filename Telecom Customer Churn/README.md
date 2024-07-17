
# Telecom Customer Churn 

### Dataset:https://www.kaggle.com/datasets/shilongzhuang/telecom-customer-churn-by-maven-analytics/data

## Problem Statement

This dashboard helps the telecom company understand why their customers churn. It helps the telecom company know if their customers are satisfied with their services. Through different ratings, they get to know their improvement area, & thus they can improve their services by identifying these area. It also lets them know the revenue loss by churned customer , thus since by using this dashboard they have identified this problem, they can further work on factors responsible for these losses.

Since, a revenue loss of $3.68 million is anticipated due to a customer churn rate of 26.54% (1,869 out of 7,043 customers), thus in all they must work on improving their services. 

### Steps followed 

- Step 1 : Load data into Power BI Desktop, dataset is a csv file.
- Step 2 : Open power query editor & in view tab under Data preview section, check "column distribution", "column quality" & "column profile" options.
- Step 3 : Also since by default, profile will be opened only for 1000 rows so you need to select "column profiling based on entire dataset".
- Step 4 : It was observed that in none of the columns errors & empty values were present except columns named "Avg.Monthly Long Distance Charge","Avg. Monthly GB downloaded","Online Security","Online Backup","Online Security" "Online Backup","Device Protection Plan","Premium Tech Support","Streaming TV","Streaming Movies","Streaming Music","Unlimited Data".
- Step 5 : For calculating average , null values were not taken into account.
- Step 6 : In the report view, under the view tab, theme was selected.
- Step 7 : Visual filters (Slicers) were added for four fields named "Risk Of Churn", "Internet Services", "Months Subscribed" & "Type of travel".
- Step 8: Several card visuals were added to the canvas.
           Using visual level filter from the filters pane, basic filtering was used & null values were unselected 
           
           Although, by default, while calculating average, blank values are ignored.
- Step 9: Bar chart, pie chart, tree chart were added. 
- Step 10 : In the report view, under the insert tab,several two text boxes were added to the canvas.
- Step 11 : In the report view, under the insert tab, using shapes option from elements group a rectangle was inserted & similarly using image option logo and stickers  were  added to the report design area.
- Step 12 : Several  Calculated column were created . They are given below.

   1.Tenure in months  was converted into tenure in years using conditional column.
![tenure in years convertion](https://github.com/user-attachments/assets/532b45f1-f623-47c1-bf55-4519d8f9de71)
   
   2.Customer Status was converted to churn category using conditional column.
![Conditional column](https://github.com/user-attachments/assets/36a022f4-bea0-4c4b-8e0b-4cdd4081c004)
   
   3.Senior citizen column was calculated from age column using conditional column.
   ![senior citizen](https://github.com/user-attachments/assets/07257a87-9673-4f92-a52a-f2448e2a829f)

   4.Dependent was also calculated from number of Dependents using conditional column.
   ![Dependent](https://github.com/user-attachments/assets/3e7ccf24-4fe8-4beb-b9f1-af0a6f8fb217)
   
   5.Number of Referal  was also calculated from Referal  using conditional column.
   ![Referal](https://github.com/user-attachments/assets/109bf619-9a50-4c05-a5e2-294f776a0dc7)
   6.Replaced null values from Internet type column to No .
   ![replace](https://github.com/user-attachments/assets/c7c91a96-6a2f-4fc4-b2f6-1578a0f9f55d)

- Step 13 : New measures were created using dax .

   Following DAX expressions were written :

        % Churn Rate = DIVIDE(CALCULATE(COUNT(churn[Churn]), churn[Churn] = "yes" ),COUNT (churn[Churn]), 0)
        
        % Device protection = DIVIDE(CALCULATE(COUNT(Churn[Device Protection Plan]), Churn[Device Protection Plan] ="Yes", churn[Churn]="Yes"),CALCULATE(COUNT(Churn[Device Protection Plan]),churn[Churn]="Yes"),0)

        % NO-Multiple lines = DIVIDE(CALCULATE(COUNT(churn[Multiple Lines]), churn[Multiple Lines]="No", churn[Churn]="Yes"),CALCULATE(COUNT(churn[Multiple Lines]),churn[Churn]="Yes", churn[Multiple Lines] <> "No phone service"),0)

        % of Dependents = DIVIDE(CALCULATE(COUNT(Churn[Dependents]),Churn[Dependents]="Yes",Churn[Churn]="Yes"),CALCULATE(COUNT(Churn[Dependents]),Churn[Churn]="Yes"),0)

        % of Married = DIVIDE(CALCULATE(COUNT(Churn[Married]),Churn[Married]="Yes",Churn[Churn]="Yes"),CALCULATE(COUNT(Churn[Married]),Churn[Churn]="Yes"),0)

        % of Referrals = DIVIDE(CALCULATE(COUNT(Churn[Referrals]),Churn[Referrals]="Yes",Churn[Churn]="Yes"),CALCULATE(COUNT(Churn[Referrals]),Churn[Churn]="Yes"),0)

        % of Senior Citizen = DIVIDE(CALCULATE(COUNT(Churn[Senior Citizen]),Churn[Senior Citizen]=1,Churn[Churn]="Yes"), CALCULATE(COUNT(Churn[Senior Citizen]),Churn[Churn]="Yes"),0)

        % Online Backup = DIVIDE(CALCULATE(COUNT(churn[Online Backup]), churn[Online Backup]="Yes", churn[Churn]="Yes"),CALCULATE(COUNT(churn[Online Backup]),churn[Churn]="Yes"),0)

        % Online Security = DIVIDE(CALCULATE(COUNT(churn[Online Security]), churn[Online Security]="Yes", churn[Churn]="Yes"),CALCULATE(COUNT(churn[Online Security]),churn[Churn]="Yes"),0)

        % Phone Service = DIVIDE(CALCULATE(COUNT(churn[Phone Service]), churn[Phone Service]="Yes", churn[Churn]="Yes"),CALCULATE(COUNT(churn[Phone Service]),churn[Churn]="Yes"),0)


        % Premium Tech Support = DIVIDE(CALCULATE(COUNT(Churn[Premium Tech Support]), churn[Premium Tech Support]="Yes", churn[Churn]="Yes"),CALCULATE(COUNT(churn[Premium Tech Support]),churn[Churn]="Yes"),0)

        % Streaming Movies = DIVIDE(CALCULATE(COUNT(churn[Streaming Movies]), churn[Streaming Movies]="Yes", churn[Churn]="Yes"),CALCULATE(COUNT(churn[Streaming Movies]),churn[Churn]="Yes"),0)

        % Streaming Music = DIVIDE(CALCULATE(COUNT(Churn[Streaming Music]), Churn[Streaming Music]="Yes", churn[Churn]="Yes"),CALCULATE(COUNT(Churn[Streaming Music]),churn[Churn]="Yes


        % Streaming TV = DIVIDE(CALCULATE(COUNT(churn[Streaming TV]), churn[Streaming TV]="Yes", churn[Churn]="Yes"),CALCULATE(COUNT(churn[Streaming TV]),churn[Churn]="Yes"),0)


        % Unlimited Data = DIVIDE(CALCULATE(COUNT(Churn[Unlimited Data]), Churn[Unlimited Data]="Yes", churn[Churn]="Yes"),CALCULATE(COUNT(Churn[Unlimited Data]),churn[Churn]="Yes"),0)

        % Yes-Multiple Lines = DIVIDE(CALCULATE(COUNT(churn[Multiple Lines]), churn[Multiple Lines]="Yes", churn[Churn]= "Yes"), CALCULATE(COUNT(churn[Multiple Lines]), churn[Churn]="Yes", churn[Multiple Lines] <> "No phone service"),0)

        Churn Count = CALCULATE(COUNT(Churn[Churn]),Churn[Churn]="Yes")

        CLV = 
        SUMX(
        Churn,
        'Churn'[Monthly Charge] * Churn[Tenure in Months]
        )


        Lost Revenue = SUMX(FILTER('Churn', 'Churn'[Customer Status] = "Churned"), 'Churn'[Total Revenue])


        Refund Rate = 
        DIVIDE(
        COUNTROWS(FILTER('Churn', Churn[Total Refunds] > 0)),
        COUNTROWS('Churn')
        )


 
 # Report Snapshot (Power BI DESKTOP)

 
![Churn dash](https://github.com/user-attachments/assets/4dcab37e-bfa8-4b8c-bfd0-5b6606d87c95)

 ![map dash](https://github.com/user-attachments/assets/5af3c824-4899-4302-a89b-24f8bc76b365)

 ![customer risk dash](https://github.com/user-attachments/assets/c7b7a2f9-b35a-4122-bc56-42b90f02cfeb)

 ![insight dash](https://github.com/user-attachments/assets/705a3083-32ba-4b2e-82d5-e98d1aea74cc)


