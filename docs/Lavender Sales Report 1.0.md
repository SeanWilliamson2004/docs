---
title: Lavender Sales Report 1.0
tags: []
description: Ramzi Views.xlsm Pivot table is used to show the data. On clicking refresh
  button gives the latest data from database. Sales person and document…
created: '2022-09-23'
modified: '2022-09-23'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Lavender%20Sales%20Report%201.0.aspx
---

[Ramzi Views.xlsm](https://codislimited.sharepoint.com/sites/Wiki/PublishingImages/Pages/Lavender%20Sales%20Report%201.0/Ramzi%20Views.xlsm)  

Pivot table is used to show the data. On clicking refresh button gives the  latest data from database. Sales person and document status filters are used to get the specific sales and document data. Button for years are for getting the specific data for year(s) mentioned  on buttons . Indication and Customer, Indication and Customer buttons are used to generate the specific report and save it on the desktop.  

This workbook/report is digitally signed by Codis certificate and VBA project is locked with password \- L@\\/3nDerV8Apr0JEcT!  

PLEASE DO NOT SHARE THE VBA PROJECT PASSWORD WITH ANYONE OUTSIDE CODIS (Dont share with Lavender either)  

Prerequisits   

- The machine/user should be on companies network i.e he/she should have database access to download data from Server.

Codis\_CarriageValue  

SELECT        SUM(dbo.SOPOrderReturnLine.LineTotalValue) AS Expr1, dbo.SOPOrderReturn.DocumentNoFROM            dbo.SOPOrderReturn FULL OUTER JOIN                         dbo.SOPOrderReturnLine ON dbo.SOPOrderReturn.SOPOrderReturnID \= dbo.SOPOrderReturnLine.SOPOrderReturnIDWHERE        (dbo.SOPOrderReturnLine.ItemCode LIKE '%Carriage%') OR                         (dbo.SOPOrderReturnLine.ItemDescription LIKE '%Carriage%')GROUP BY dbo.SOPOrderReturn.DocumentNo  

The Codis\_CarriageValue view is define in Lavender server.  

[originalquery.sql](https://codislimited.sharepoint.com/sites/Wiki/PublishingImages/Pages/Lavender%20Sales%20Report%201.0/originalquery.sql)  

[Kurrens query.sql](https://codislimited.sharepoint.com/sites/Wiki/PublishingImages/Pages/Lavender%20Sales%20Report%201.0/Kurrens%20query.sql)  

The original query is missing out the discount for total number of sales order items. Kurrens query includes the discount for total number of sales order items which is used in **Codis\_LavenderVw** view.   

Note : **Codis\_LavenderVw** view in Lavender Server is called to retreive the latest data from the database.  

On 26\-03\-2023 this report will not work (automatically close if someone opens it with a Message Box "Your License has Expired. Please contact Codis")

Check with Sales if they have paid for the report and then go to VBA from developers tab  

![Lavender_dev1.PNG](images/PublishingImages_Pages_Lavender_Sales_Report_1.0_Lavender_dev1.PNG)  

Enter the password L@\\/3nDerV8Apr0JEcT! then double click Thisworkbook from the left window(VBA\-Project) and Extend the date in line If  todaydate \> \#3/26/2023\# with a year and Save the Macro enabled workbook.  

![Lavender_dev2.PNG](images/PublishingImages_Pages_Lavender_Sales_Report_1.0_Lavender_dev2.PNG)
