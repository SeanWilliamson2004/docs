---
title: Sage Company Creation
tags: []
description: 'Creation of a New Company in SAGE. Following are the steps: Go to Sage
  200 Administrator > Companies > Right Click Add New Company Enter the details,…'
created: '2023-06-19'
modified: '2023-06-19'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Sage%20Company%20Creation.aspx
---

**Creation of a New Company in SAGE.**

Following are the steps:

1. Go to Sage 200 Administrator \> Companies \> Right Click Add New Company
2. Enter the details, Company name, Server , Database Name.   

![Company Details.png](images/PublishingImages_Pages_Sage_Company_Creation_Company_Details.png)
3. Test , Update and Click OK.

**Once the company is created, it must have certain nominal accounts to function**

1. Create Nominal accounts with the following details.
2. You need to create 2 nominal accounts with the following Report Categories.  

**To create Report Categories**
1. Nominal Ledger\>Utlities\>Ledger SetUp\> Report Categories\>Add(make sure to add the following highlighted details)  

 ![Report Categories.png](images/PublishingImages_Pages_Sage_Company_Creation_Report_Categories.png)
2. Once Report Categories are created, Create a suspense account with the following details.  
![Suspense Acc.png](images/PublishingImages_Pages_Sage_Company_Creation_Suspense_Acc.png)
3. Create a Accumulated Profit account with the following details,  

 ![Acc Profit.png](images/PublishingImages_Pages_Sage_Company_Creation_Acc_Profit.png)  

Note: Both these accounts should have an **Empty** Cost Centre and Department.

**Once accounts are created, We need to assign Default Nominal Accounts.**

1. Nominal Ledger\> Utilities\> Ledger Setup\> Default Nominal Accounts
2. Enter the following accounts:  
![DefaultNA1.png](images/PublishingImages_Pages_Sage_Company_Creation_DefaultNA1.png)  

![DefaultNA2.png](images/PublishingImages_Pages_Sage_Company_Creation_DefaultNA2.png)

Note: Not necessary to enter the Creditors Control, you can create any nominal account and use it for the same.

You are all set to experiment with the Blank company created.
