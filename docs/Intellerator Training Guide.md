---
title: Intellerator Training Guide
tags:
- Power BI
description: Introduction This guide will help to walk end users through the key features
  and functionality of Intellerator dashboards. The goal is to empower…
created: '2024-06-24'
modified: '2024-06-25'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Intellerator%20Training%20Guide.aspx
---

# Introduction

This guide will help to walk end users through the key features and functionality of Intellerator dashboards. The goal is to empower users to navigate, analyse, and extract insights from the dashboards effectively.

## Getting Started

1. Provide the dashboard link to the participants before the meeting.
2. Ask them to confirm if they can access the link successfully.
3. Share screen and request participants to open the link and follow along.

## Dashboard Overview

1. Direct attention to the left\-hand side of the screen:  
 "On the left, you'll see a list of available modules. Are there any particular dashboards you're interested in exploring today? Like Credit Control, Financial Statements, etc."
2. Based on their preference, open the requested dashboard.
3. If applicable, explain the multi\-company feature:  
 "This dashboard supports multiple companies. We can select one or multiple companies, and you'll see the dashboard values adjust accordingly."

## Navigation and Filtering

1. Introduce the left filter pane:  
 "Let's look at the filtering options on the left. We'll go through these slowly to ensure you're comfortable with each one."
2. Demonstrate the date filter:  
 "Here's the date filter. To select a specific date range, click here and choose your desired dates."
3. Explain other relevant filters, demonstrating how to use each one.

## Dashboard Structure

1. Explain the two\-page structure:  
 "Each dashboard consists of two main pages: a Summary page and an Analysis page. The Summary provides a quick overview, while the Analysis page offers more detailed information."

### Summary Page

1. Select 1\-2 charts on the summary page to explain:  
 "Let's look at this chart. It shows \[explain what the chart represents and its significance]."
2. Demonstrate the hover feature:  
 "If you hover over any part of the chart, you'll see more detailed information like account names or the total values in case of a donut chart."
3. Show the information icon:  
 "Notice the '?' icon near each chart. Clicking this will provide more context about what the chart represents."
4. Demonstrate chart filtering:  
 "You can filter data directly from the chart. Click on a bar to filter for that specific data point."
5. Show multi\-select filtering:  
 "To select multiple data points, hold the Ctrl key (or Cmd on Mac) while clicking different bars. This works across multiple charts too."

### Additional Features

1. Demonstrate table view:  
 "Any chart can be viewed as a table. Simply go to \[show location] to switch between chart and table views."
2. Show export functionality:  
 "To export any chart to Excel, click \[show location]. This allows you to work with the data offline if needed."

### Analysis Page

1. Briefly revisit the filter bar:  
 "Remember, the same filtering options we saw earlier apply here as well."
2. Select 2\-3 charts to explain in detail.

## Commenting Feature

1. Demonstrate the commenting feature:  
 "Let's try adding a comment together. First, we'll apply a date filter and select a specific data point on this chart."
2. Guide users through adding a comment.
3. Show how comments retain context:  
 "Now, let's remove our filters. If we click on the comment we just added, you'll see that it automatically reapplies the filters we had when we made the comment."

## Row\-Level Security (if applicable)

If the dashboard uses Row\-Level Security (RLS), sales, financial, nominal; then explain:  
 "This dashboard implements Row\-Level Security. This means \[explain the specific implications for this dashboard, such as data visibility restrictions based on user roles, eg. For sales dashboard, only manager can see sales for each location and salesperson won't be able to see sales data of other salespersons or locations]. \[Show them how they can implement it in Sage, if they are not using.]"  

# Intellerator Modules

There are 7 modules in Intellerator  

> 1\. Credit Control
> 
> 2\. Payments Control
> 
> 3\. Nominal Transactions
> 
> 4\. Financial Statements
> 
> 5\. SOP  
> 
> 
> 6\. POP
> 
> 7\. Stocks

## Credit Control:

### Credit Control \- Summary

![](images/PublishingImages_Pages_Intellerator_Training_Guide_CreditControlSummary.png)  

#### Total Base

> Total Outstanding Amount

Last Year

> Amount Overdue last year at the end (if no period is selected), or for the last year's period

#### By Period Graph

> Graphical representation of outstanding amount for each month, if click on any bar of any period, it selects that period for entire summary page. To view a more detailed data like transactions, right click on any bar and select 'Drill Through\>Transactions' option.

#### By Ageing Period

> Donut chat representing outstanding amounts by ageing period. Selecting a aging period updates the dashboard to a focus mode for the selected ageing period, click on it again gets out of focus mode

#### Top 10 debtors

> Graphical representation of debtors with highest amount outstanding.

#### By Ageing Period Over Time

> The amount owed per ageing period at each financial period in the selected year. This lets you see the trend in your credit control over time. Better credit control maximises the "Current" area and minimises the other colours. To see your credit position with a particular customer over time, click on that customer in the "Top 10 Customers" chart.

### For Filters:

*\[image: clip\_image004\.png not found]*![](images/PublishingImages_Pages_Intellerator_Training_Guide_CreditControlFilter.png) 

There are 3 ways to apply filters.

1. Selecting desired options from left panel
2. Each visual has a filter icon, from where we can change the filter value
3. Interacting with the visuals, some visuals let select data like period, customers.

### Credit Control \- Analysis

*\[image: clip\_image006\.png not found]*#### By Company:

> If there are multiple companies then it shows the data for each company for each ageing period. Hovering mouse over the bar, shows the details for each ageing period.

#### By Query Flag:

> Transactions can have a query flag in Sage, this view shows balances for each query flag.

Although viewing the transaction does not specify the customer code, which can be complicated when reviewing the data.

### Sage200 Data Source:

This data can be cross checked with Aged Debtors report in Sage

Date in left panel of dashboard is the 'Base date for ageing' in Sage200 Report  

## SOP

### SOP \- Summary

![SOPSummary.png](images/PublishingImages_Pages_Intellerator_Training_Guide_SOPSummary.png)  

#### Total Net:

> Display total of SOP orders for the selected year

#### Prior Year:

> Total of last year's SOP orders (till the period of current year), if a period is selected then it is adjusted accordingly

#### Sales by Period:

> SOP order for each period of the selected year

> Right click\> Drill through\>Transactions: It lists all the transactions for the selected period, Sales returns have negative amounts.

Transaction's view doesn't have customer codes for each order, which can be confusing if user wants to filter for customers in the transactions view.

#### Top 5 customers:

> Lists top 5 customers based on total of SOP orders

#### Top 10 products group:

> It shows top 10 product groups, when we drill through it, it shows list of order which have the selected product group

Transactions view display all the order but the ones that don't have the selected product group, it shows order value as 0 which can lead to confusion as user might think it only shows the data for the selected product group.  

#### Map:

> It uses customers address and display it on the map. The bigger the circle, higher the total of SOP orders

### SOP \- Analysis

Different views display SOP orders based on different criteria. Each view has an option to drill through transactions.  

![SOPAnalysis.png](images/PublishingImages_Pages_Intellerator_Training_Guide_SOPAnalysis.png)  

## Payments Control

This module is similar to Credit Control, but for Purchase Ledger in Sage200\.  

### Sage200 Data Source:

In Sage200, this report can be compared with Aged Creditors report.

## POP

It is similar to SOP, but for purchase orders.  

## Financial Statements

![FinStatement01.png](images/PublishingImages_Pages_Intellerator_Training_Guide_FinStatement01.png)  

Financial Statements from Sage are pulled in this report, balance sheets, profit \& loss.  

Layotus are configurable in Sage200, and any changes made to these layouts in Sage200 will be applicable on this report in Intellerator.  

If the layouts are not designed in Sage200, you may refer to below article on how to configure it:  

[Designing financial statements (sage.co.uk)](https://desktophelp.sage.co.uk/sage200/professional/Content/NL/Design%20Financial%20Reports.htm)  

Intellerator support multiple layouts, and can swtich quickly from one layout to another with a simple change in layout option in the left panel.  

Reports can be filtered by cost centres and departments, if required.  

If a line is selected in the report, a detailed version is loaded in the 2 views at the bottom as shown in below image:  

![FinStatement02.png](images/PublishingImages_Pages_Intellerator_Training_Guide_FinStatement02.png)  

Clicking on '?' icon, gives information about what that view represents.  

### Sage200 Data Source:

Nominal Ledger \> Reports \> Financial Statements  
To create new layouts:Nominal Ledger \> Ultitlies \> Ledger Setup \> Financial Statement Layouts  

## Nominal Transactions

### Nominal \- Summary

![Nominal01.png](images/PublishingImages_Pages_Intellerator_Training_Guide_Nominal01.png)  

#### Company and Filters

- **Company Selector**: Allows users to select the company for which they want to view the financial data. This is useful for organisations having multiple Sage200 companies.
- **Transaction Type**: Users can filter the data based on the type of transactions (e.g., current, deferred).
- **Report Category Type**: Filters the data by different report categories.
- **Date Range**: Users can select a specific date range to view the financial data for that period.
- **Module Selector**: Allows users to filter data by different modules within Sage 200\.

#### Key Financial Metrics

- **Net Income**: Displays the total net income for the selected period.
- **Net Income (Prior Year)**: Shows the net income for the same period in the previous year, allowing for year\-over\-year comparison.
- **Net Assets**: Displays the total net assets for the selected period.
- **Net Assets (Prior Year)**: Shows the net assets for the same period in the previous year.

#### Expense by Cost Centre

- **Pie Chart**: Visualizes the distribution of expenses across different cost centres. Each segment represents a cost centre, and the size of the segment indicates the proportion of total expenses.
- **Cost Centre List**: Lists the cost centres with corresponding expense values and percentages.

#### Income by Cost Centre

- **Pie Chart**: Visualizes the distribution of income across different cost centres. Each segment represents a cost centre, and the size of the segment indicates the proportion of total income.
- **Cost Centre List**: Lists the cost centres with corresponding income values and percentages.

#### Balance by Report Category

- **Bar Chart**: Displays the balance for different report categories. Each bar represents a category, and the length of the bar indicates the balance amount.
- **Report Category List**: Lists the report categories with corresponding balance values.

#### Net Income Trend

- **Line Chart**: Shows the trend of net income over the selected period. This helps in understanding the financial performance over time.
- **Monthly Data Points**: Each point on the line represents the net income for a specific month.

#### Interactive Features

- **Hover Information**: Users can hover over any chart or data point to see more detailed information.
- **Filter by Chart**: Users can click on any segment of a chart to filter the data based on that segment. For example, clicking on a specific cost centre in the pie chart will filter the entire dashboard to show data related to that cost centre.
- **Table View**: Users can switch any chart to a table view by using drill through option

### Nominal \- Analysis

![Nominal02.png](images/PublishingImages_Pages_Intellerator_Training_Guide_Nominal02.png)  

Analysis view has similar options to the Summary, but it has some additional options to filter the data like department and for each nominal code/account name.  

### Sage200 Data:

Nominal Ledger \> Reports\> Account Analysis  

## Stock Valuations

### Summary

![stock01.png](images/PublishingImages_Pages_Intellerator_Training_Guide_stock01.png)  

#### Company and Filters

- **Company Selector**: Allows users to select the company for which they want to view the stock data.
- **Product Group**: Users can filter the data based on different product groups.
- **Product**: Allows users to filter data by specific stock items.

#### Key Stock Metrics

- **Stock Value**: Displays the total stock value for the selected period. This is a crucial metric indicating the overall value of the stock held by the company.

#### Stock Value This Year vs Prior Year

- Compares the stock value of the current year against the previous year. This helps in understanding the trends and changes in stock value over time.

#### Top 10 Product Groups

- Visualizes the distribution of stock value across the top 10 product groups. Each block represents a product group, and the size of the block indicates the proportion of the total stock value.

#### Top 5 Products

- Displays the top 5 products by stock value. Each segment represents a product, and the size of the segment indicates the proportion of the total stock value.

#### Stock Value Over Time

- Shows the trend of stock value over the selected period. This helps in understanding the changes in stock value over time.

### Analysis

Analysis give more detailed inforamtion about the stocks  

![stock02.png](images/PublishingImages_Pages_Intellerator_Training_Guide_stock02.png)  

### Sage200 Data:

Stock Control \> Report \> Status \> Valuation
