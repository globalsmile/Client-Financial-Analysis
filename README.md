# Client Financial Analysis with Excel

<img align="right" alt="Snoring Partner" width="1000" height = "400" src="https://i0.wp.com/leonine.com.ng/new/wp-content/uploads/2020/03/Leonine-Advisory-Page-Routine-Advisory-Services.jpg?resize=1024%2C729&ssl=1">

---


# Table of Contents

- [Introduction](https://github.com/globalsmile/Client-Finacial-Analysis#introduction)
- [Problem Statement](https://github.com/globalsmile/Client-Finacial-Analysis#Problem-Statement)
- [Data Sourcing](https://github.com/globalsmile/Client-Finacial-Analysis#Data-Sourcing)
- [Data Transformation](https://github.com/globalsmile/Client-Finacial-Analysis#Data-Transformation)
- [Data Modeling](https://github.com/globalsmile/Client-Finacial-Analysis#Data-Modeling)
- [Data Visualization](https://github.com/globalsmile/Client-Finacial-Analysis#Data-Visualization)
- [Data Analysis](https://github.com/globalsmile/Client-Finacial-Analysis#Data-Analysis)
- [Insights](https://github.com/globalsmile/Client-Finacial-Analysis#Insights)
- [Shareable link](https://github.com/globalsmile/Client-Finacial-Analysis#Shareable-Link)


---

# Introduction

The goal of this financial analysis is to analyze whether the client is stable, solvent, liquid, or profitable enough to warrant a monetary investment. 


---

# Problem Statement

Using the client's financial data:
- Help the client unlock the potential of analysis and reporting
- Produce everything the client need to know about her finances

---

# Data Sourcing

This Datasets were presented by [Finex Skills Hub](https://www.finexskillshub.com) and available at:

- https://tinyurl.com/OUINIG

---

# Data Transformation

Data transformation was done in Power Query and the datasets were loaded into Microsoft Excel Power Pivot for modeling.

The client's financial data consists of  2 worksheets containing 2 tables:

- `Transactions` which has `4 columns and 296 rows` of observation
- `Budget` which has `15 columns and 24 rows` of observation

The tabulation below shows the `Transactions` table with its column names and their description:
| Column Name | Description |
| ----------- | ----------- |
| Date | Represents the date of the transaction |
| Description | describes the transaction narration |
| Category | Describes the category of the transaction |
| Amount | Represents the amount  of the transaction |

The tabulation below shows the `Budget` table with its column names and their description:
| Column Name | Description |
| ----------- | ----------- |
| Category | Describes the category of the budget |
| Class | describes the class of the budget |
| Type | Describes the the type of the budget |
| Jan 2021 - Dec 2021 | Represents the budget amount for each month respectively |


Data Cleaning for the dataset was done in power query as follows:

- For the `Budget` table, the columns `Jan 2021` to `Dec 2021` where unpivoted
- The resulting `Attribute` and `Value` columns where renamed to `Date` and `Amount` respectively 
- Validated the accuracy of the of `Date` column by changing the type to `date only`
- Validated the accuracy of the of `Amount` column by changing the type to `whole number`
- A dimensions table named `categories` was created by referencing the `Budget` table
- Unneccessary columns were removed from the `categories` table
- Duplicate rows were removed from `categories` table

To ensure the accuracy of the dates in the `Date` column each of the tables, a date table was created for referencing using the M-formula:

`{Number.From(List.Min(Transactions[Date]))..Number.From(List.Max(Transactions[Date]))}`

Here is a breakdown of what the formula does:

For the dataset, we want the start date to reflect the earliest to latest date that we have in the data: January 01, 2021 - December 01, 2021.

`Month`,` Month Name`, `Year` columns were extracted from the date table

The date table was named `Calender`.

---

# Data Modeling

After the dataset was cleaned and transformed, it was ready to be modeled(using Power Pivot).

- The `Calender` table was marked as the official date table in the dataset.
- A `one-to-many (*:1) relationship` was created between the `Budget` and the `Calender` tables using the `date` column in each of the tables
- A `one-to-many (*:1) relationship` was created between the `Transactions` and the `Calender` tables using the `date` column in each of the tables 
- A `one-to-many (*:1) relationship` was created between the `Transactions` and the `Categories` tables using the `Category` column in each of the tables
- A `one-to-many (*:1) relationship` was created between the `budget` and the `Categories` tables using the `Category` column in each of the tables 
- The realtioships formed in the data model is a `Star Schema` and is shown below:

<img align="right" alt="Data Model" width="1000" height = "400" src="https://user-images.githubusercontent.com/106287208/183560342-f5e144bd-ffe1-476e-a264-172b0b23462f.png">

---

# Data Visualization

Data visualization for the datasets was done using Microsft Excel:

- The `Dashboard` worksheet: Shows the Actual amount, Budget amount, Balance, etc of the client.

Figure 1 shows visualizations from `Dashboard` worksheet

| Figure 1 |
| ----------- |
| ![image](https://user-images.githubusercontent.com/106287208/183564662-5a1714c7-610e-45f7-be17-6ae94c6a4628.png) |

---

# Data Analysis

Measures used in visualization are:

- Actual = `SUM(Transactions[Amount])`
- Balance = `SUM(Budget[Amount])`
- Balance = `[Budget]-[Actual]`


As shown from [Data Visualization](https://github.com/globalsmile/Client-Finacial-Analysis#Data-Visualization), It can be deducted that:

- The client budgeted a total amount of `3600`
- The client spent a total amount of `4260`
- The client remaining balance is `-660`

---

# Insights

As shown by [Data Visualization](https://github.com/globalsmile/Client-Finacial-Analysis#Data-Visualization), It can be deducted that:

- The client has set a monthly budget amount of `300`, however the client has been finding it difficult to stay afloat of this budget amount
- It appears the client has spent the most in the most of `July`
- It appears the client has spent the highest amount on `Consultancy`

---

# Shareable Link

You can interact with the report here: 

https://app.powerbi.com/view?r=eyJrIjoiMDVlNzU4MzUtY2UxOS00Yzk1LTlkNDAtZTA4Yzc5NjkwOTg3IiwidCI6IjQ5ODY4YWYzLWNjNWYtNDIxNC04YjdmLTQwZjM3NDY0OWEwOSJ9
