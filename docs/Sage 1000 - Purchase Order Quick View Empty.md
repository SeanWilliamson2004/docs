---
title: Sage 1000 - Purchase Order Quick View Empty
tags:
- Sage
- Support
- Sage 1000
description: 'S1000 - Purchase Order Quick View Empty Following screenshots of error:
  Brief Description of Error: In Sage 1000 Purchase Order Enquiry and…'
created: '2018-08-07'
modified: '2018-08-08'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Sage%201000%20-%20Purchase%20Order%20Quick%20View%20Empty.aspx
---

# S1000 \- Purchase Order Quick View Empty

## Following screenshots of error:

 ![](images/Support_Support_Wiki_Images_Sage_1000_Purchase_Order_Quick_View_Empty_problem1.PNG)![](images/Support_Support_Wiki_Images_Sage_1000_Purchase_Order_Quick_View_Empty_problem2.PNG)

## Brief Description of Error:

In Sage 1000 Purchase Order Enquiry and Requisitions \- Quick View attachment for order number does not show Purchase Order name with date and time \- from here user can select purchase order to email in pdf format. The problem is that instead the box shows empty as shown above in the screenshot. 

## Solution from Reg Perrins \- Sage Support:

As discussed, I ran SQL

Profile and checked that the Drilldown request was actually being seen on the

Sage instance of SQL (look for "tcr" in the TextData) \- this at least

showed that the Drilldown service was looking at the correct database instance.

I then took the example SQL Statement and tried to run it whilst logged into

SSMS as "tcruser" \- this failed as it didn't recognise

"TcrGB" table. I then tried "tcruser.TcrGB" and it

recognise that. This normally indicates a security issue so I checked and

tcruser had "sysadmin" Roles in SQL \- I removed that and re\-started

the Drilldown service and all is now working. 

## Screenshots of solution on server:

![](images/Support_Support_Wiki_Images_Sage_1000_Purchase_Order_Quick_View_Empty_sol1.PNG)![](images/Support_Support_Wiki_Images_Sage_1000_Purchase_Order_Quick_View_Empty_sol2.PNG) 

![](images/Support_Support_Wiki_Images_Sage_1000_Purchase_Order_Quick_View_Empty_sol3.PNG)  

**Make sure that for tcruser sysadmin is not ticked in roles.**
