# Client Financial Analysis with Excel

<img align="right" alt="Snoring Partner" width="1000" height = "400" src="https://i0.wp.com/leonine.com.ng/new/wp-content/uploads/2020/03/Leonine-Advisory-Page-Routine-Advisory-Services.jpg?resize=1024%2C729&ssl=1">

---


# Table of Contents

- [Introduction](https://github.com/globalsmile/Airline-Analysis#introduction)
- [Problem Statement](https://github.com/globalsmile/Airline-Analysis#Problem-Statement)
- [Data Sourcing](https://github.com/globalsmile/Airline-Analysis#Data-Sourcing)
- [Data Transformation](https://github.com/globalsmile/Airline-Analysis#Data-Transformation)
- [Data Modeling](https://github.com/globalsmile/Airline-Analysis#Data-Modeling)
- [Data Visualization](https://github.com/globalsmile/Airline-Analysis#Data-Visualization)
- [Data Analysis](https://github.com/globalsmile/Airline-Analysis#Data-Analysis)
- [Insights](https://github.com/globalsmile/Airline-Analysis#Insights)
- [Shareable link](https://github.com/globalsmile/Airline-Analysis#Shareable-Link)


---

# Introduction

To help the client unlock the potential of financial analysis and reporting, I’ve analyzed the client's financial data 

The goal of this financial analysis is to analyze whether the client is stable, solvent, liquid, or profitable enough to warrant a monetary investment. 


---

# Problem Statement

Using the client's financial data:
- help the client unlock the potential of analysis and reporting
- produce everything the client need to know about her finances

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


Data Cleaning for the 2 datasets was done in power query as follows:

- Unnecessary columns were removed. The remaining columns were tailored to provide answers to the [Problem Statement](https://github.com/globalsmile/Airline-Analysis#Problem-Statement) and are shown below:

| Column Name |
| ----------- | 
| End | 
| Sleep Quality | 
| Regularity | 
| Time in Bed | 
| Time Asleep | 
| Snore Time |

- Validated the accuracy of the of `End` column by changing the type to `date only`
- Removed error rows from the `End` column

To ensure the accuracy of the dates in the `End` column, a date table was created for referencing using the M-formula:

`List.Dates(#date(2020,01,01), 365*1, #duration(1,0,0,0)`

Here is a breakdown of what the formula does:

For the 2 datasets, we want the start date to reflect the earliest date that we have in the data: January 01, 2020. Additionally, you want to see date for 1 year(time frame for our anlysis), including dates in the future.This approach ensures that, as new observation flows in we won't have to re-create this table.Also the duration represents observation for everyday.

The date table was named `Calender`.

---

# Data Modeling

After the datasets were cleaned and transformed, it was ready to be modeled.

- The `Calender` table was then marked as the official date table in the dataset.
- To reference the dates in the `End` column of the 2 tables named `Client` and `Partner` respectively more accurately, a `one-to-many (*:1) relationship` was created between the 
`Client` and the `Calender` tables using the dates column in each of the tables, also a `one-to-many (*:1) relationship` was created between the 
`Partner` and the `Calender` tables using the dates column in each of the tables in a `Star Schema` as shown below:

<img align="right" alt="Data Model" width="1000" height = "400" src="https://user-images.githubusercontent.com/106287208/183488382-e73927a3-8147-4f85-a837-18806d704e4f.png">

After [Data Visualization](https://github.com/globalsmile/Airline-Analysis#Data-Visualization), the all the columns in both the `Client` and `Partner` tables were hidden.

---

# Data Visualization

Data visualization for the datasets was done in two folds using Microsft Power BI Desktop and Microsoft PowerPoint:
- `Client Sleeping Habit Analysis`: Shows the average time in bed per day, average time asleep per day, average snore time per day, etc for the client.
- `Partner Sleeping Habit Analysis`: Shows the average time in bed per day, average time asleep per day, average snore time per day, etc for the Partner.

Figure 1 shows visualizations from `Client Sleeping Habit Analysis`

| Figure 1 |
| ----------- |
| ![image](https://user-images.githubusercontent.com/106287208/183494154-37e8bb69-20a0-4cc8-a6b7-2529d462350f.png) |

Figure 2 shows visualizations from `Partner Sleeping Habit Analysis`

| Figure 2 |
| ----------- |
| ![image](https://user-images.githubusercontent.com/106287208/183493702-dd7748af-115b-4e35-ac8c-a87b0a58b7d3.png) |

---

# Data Analysis

Measures used in visualization are:

- Average Regularity = `AVERAGEX(Client,Client[Regularity])`
- Average Sleep Quality = `AVERAGEX(Client,Client[Sleep Quality])`
- Average Time in Bed = `AVERAGEX(Client,Client[Time in bed (seconds)]) / 3600`
- Average Time Asleep = `AVERAGEX(Client,Client[Time asleep (seconds)]) / 3600`
- Average Snore Time = `AVERAGEX(Client,Client[Snore time]) / 60`
- Background Transparency = `"rgba(255,255,255,0)"`

As shown by [Data Visualization](https://github.com/globalsmile/Airline-Analysis#Data-Visualization), It can be deducted that:

- Both the client and partner snores, however the partner(`Average Snore Time = 15 min`)  snores longer than the client(`Average Snore Time = 3`)
- The partner(`Average Time in Bed = 7 hours`) spends more time in bed than the client(`Average Time in Bed = 5 hours`)
- The partner(`Average Time Asleep = 6 hours`) spends more time asleep than the client(`Average Time Asleep = 4hours`)

---

# Insights

As shown by [Data Visualization](https://github.com/globalsmile/Airline-Analysis#Data-Visualization), It can be deducted that:

There is a strong negative correlation between the sleep quality and the snoring time of both the client and partner, hence we can not make any recommendations as to improving the quality of sleep

This can be caused by an overestimation of snoring by the app. For clinical practice, the present results indicate that the app should not be used for OSA screening, but can possibly be a helpful tool for monitoring snoring e.g., inconjunction with the evaluation of different treatment modalities.

---

# Shareable Link

You can interact with the report here: 

https://app.powerbi.com/view?r=eyJrIjoiMDVlNzU4MzUtY2UxOS00Yzk1LTlkNDAtZTA4Yzc5NjkwOTg3IiwidCI6IjQ5ODY4YWYzLWNjNWYtNDIxNC04YjdmLTQwZjM3NDY0OWEwOSJ9
