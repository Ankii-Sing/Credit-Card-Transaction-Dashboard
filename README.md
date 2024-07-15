# Credit-Card-Transaction-Dashboard
This is Credit Card Financial Transaction Report made using PowerBi.

## What has Done in Project.
  * we made a multi-screen Dashboard and automated using SQL.
  * whenever new data is added to SQL we just need to refresh the Dashboard all charts and fields automatically updates with the new data.

## STEPS:
1. Prepare a csv file. 
2. In Postgre SQL
   * Create DataBase.
   * Create Tables and define its columns.
   *  import data into the tables form csv file.
3. Connect PowerBi with SQL.

## Note : 
* It is suggested to clean the data into the excel or SQL first then import the data into the powerbi. 
* if we try to clean the data in powerbi itself it will add more filters and constraints to the columns that will make the data processing slow on Dashboard.
* Because when we refresh the Dashboard , First it will apply all the filters and Constraints and then After it will process the Query.

# DAX Queries

* AgeGroup = SWITCH(
 TRUE(),
 'public cust_detail'[customer_age] < 30, "20-30",
 'public cust_detail'[customer_age] >= 30 && 'public cust_detail'[customer_age] < 40, "30-40",
 'public cust_detail'[customer_age] >= 40 && 'public cust_detail'[customer_age] < 50, "40-50",
 'public cust_detail'[customer_age] >= 50 && 'public cust_detail'[customer_age] < 60, "50-60",
 'public cust_detail'[customer_age] >= 60, "60+",
 "unknown"
)
* IncomeGroup = SWITCH(
 TRUE(),
 'public cust_detail'[income] < 35000, "Low",
 'public cust_detail'[income] >= 35000 && 'public cust_detail'[income] <70000, "Med",
 'public cust_detail'[income] >= 70000, "High",
 "unknown")

* week_num2 = WEEKNUM('public cc_detail'[week_start_date])

* Revenue = 'public cc_detail'[annual_fees] + 'public cc_detail'[total_trans_amt] + 'public cc_detail'[interest_earned]

* Current_week_Reveneue = CALCULATE(
 SUM('public cc_detail'[Revenue]),
 FILTER(
 ALL('public cc_detail'),
 'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2]))) 

* Previous_week_Reveneue = CALCULATE(
 SUM('public cc_detail'[Revenue]),
 FILTER(
 ALL('public cc_detail'),
 'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2])-1))

# Projct Insights Based on last weeks data.

1. Week on Week change: 
    * Revenue increased by 28.8%.
   
2. Overview YTD:
    * Overall revenue is 57M
    * Total interest is 8M
    * Total transaction amount is 46M
    * Male customers are contributing more in revenue 31M, female 26M
    * Blue & Silver credit card are contributing to 93% of overall transactions
    * TX, NY & CA is contributing to 68%
    * Overall Activation rate is 57.5%
    * Overall Delinquent rate is 6.06%
   
