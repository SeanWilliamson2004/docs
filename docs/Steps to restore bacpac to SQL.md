---
title: Steps to restore bacpac to SQL
tags:
- Sage 200 Extra Online
- Support
- Sage
- SQL
description: 'Download a bacpac to view the SQL data: Within SEOS (Sage ERP Online
  Services) you must download a backup of the data to restore locally. This may be…'
created: '2017-02-23'
modified: '2019-04-29'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Steps%20to%20restore%20BACPAC%20to%20SQL.aspx
---

## Download a bacpac to view the SQL data:

Within SEOS (Sage ERP Online Services) you must download a backup of the data to restore locally. This may be a nightly automatic backup or an on\-demand backup of the company and information on how to do this can be found [here](http://www.sage.co.uk/asksage/viewarticle.asp?p_faqid=31780).

## Import the bacpac into SQL Server Management Studio

Within SQL Server 2012 SP2, right click 'Databases' and select 'Import Data\-tier Application…' and follow the wizard to import the data.

Delete the following entities from the sql database if present:   

## Stored Procedures

Spr\_EstGetAmendedStatus  
Spr\_MrpUsageLevelGetUniqueProducts  
Spr\_UsageLevelWhereUsed  
spr\_ReseedTable  

## Functions (Scalar\-valued Functions)

Fn\_EstAppendTo  
Fn\_EstApplyMarkup  
Fn\_EstQtyBreakSellingPrice   
Fn\_EstStageAmended  

## Views

vw\_EstimateList  
vw\_MrpRecommendationsWithNeededByDate  
vw\_NeededByDate  
vw\_WorksOrderAllocatedComponentsList

Then run this [SQL Query](https://codislimited.sharepoint.com/sites/Wiki/Support/Support%20Wiki/Documents/SQL%20Queries/RemoveManufacturingDatabase.sql) to remove the manufacturing script.

You can now directly interrogate the data in SQL or open the data in Sage 200 by connecting the database in SA in the usual way.
