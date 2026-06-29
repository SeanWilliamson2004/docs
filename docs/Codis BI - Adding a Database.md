---
title: Codis BI - Adding a Database
tags:
- Power BI
description: 'A. Restore a Database Copy your Backup file. Go to this path: C: > Program
  Files > Microsoft SQL Server > MSSQL15.MSSQLSERVER > MSSQL > Backup Paste…'
created: '2022-11-24'
modified: '2022-12-07'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Codis%20BI%20-%20Adding%20a%20Database.aspx
---

#### A. Restore a Database

1. Copy your Backup file.
2. Go to this path:  
C: \> Program Files \> Microsoft SQL Server \> MSSQL15\.MSSQLSERVER \> MSSQL \> Backup
3. Paste your Backup file.
4. Go to SQL Server Management Studio and Log in.
5. Right click on "Databases" under Object Explorer.
6. Click on "Restore Database".
7. Select Source where the Backup file is stored.
1. Click on Devices and then 3 Dots.
2. Then a "Select Backup devices" window will apper. Click on "Add".
3. Go to the path from step 2 again:  
C:\\Program Files\\Microsoft SQL Server\\MSSQL15\.MSSQLSERVER\\MSSQL\\Backup
4. Double click on your Back up file.

9. You can also select destination for your database, if you want.
10. Then click on "Ok".

#### B. Provide permissions to the database

> While using the "Codis BI Web Services" for making Power BI Reports/Dashbords/Apps for customers, **if we** **create or restore a new sage database****, then in that case we will have to run the following query on SQL Server.** Which will add Codis BI as a secure user of that database and will also provide some security permissions. Otherwise the data will not be fetched.

> > use DatabaseName;
> 
> 
> > CREATE USER \[NT SERVICE\\Codis BI] FOR LOGIN \[NT SERVICE\\Codis BI];
> 
> 
> > EXEC sp\_addrolemember 'db\_datareader', \[NT SERVICE\\Codis BI];

> Some points to be noted:

1. Run this Query on the same PC where Codis BI is already installed fro the customer.
2. You can Run this Query in SQL Server Management Studio.
3. Replace "DatabaseName" with New database name.

#### C. Get Access to Workspace and Data Gateway

> Ask the Codis Admin to give you the permissions in order to get the Access to Customer's workspace and Data Gateway.

#### D. Add the database to the Report

1. Go to powerbi.com.
2. Select Customer workspace from workspaces.
3. Move your mouse pointer on dataset and click on 3 dots.
4. Select settings.
5. Expand "Parameters"
6. Add database name in repective space.  
**Note:** In case of multiple databases, you can write them comma seperated without leaving any spaces*.*
7. Then click on "Apply".

#### E. Refresh the Dataset

1. Go to Customer workspace.
2. Click on Dataset.
3. Hit "Refresh" at top left side.
4. If successfull, it will show you date and time.

#### F. Revoke Access to workspace and Data Gateway.

> Ask the Codis Admin to revoke your Access to Customer's workspace and Data Gateway.
