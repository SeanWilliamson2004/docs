---
title: How to Create BACPAC for Azure SQL
tags:
- Solution
description: A BACPAC is a Windows file with a .bacpac extension that encapsulates
  a database’s schema and data. The primary use case for a BACPAC is to move a…
created: '2017-03-17'
modified: '2019-04-29'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/How%20to%20Create%20BACPAC%20for%20Azure%20SQL.aspx
---

A BACPAC is a Windows file with a .bacpac extension that encapsulates a database’s schema and data. The primary use case for a BACPAC is to move a database from one server to another – or to migrate a database from a local server to the cloud. 

If you want to prepare BACPAC file from your sql database, you need to run Microsoft SQL Management Studio and find your local database from where you want to create BACPAC file. 

![](images/Support_Support_Wiki_Images_Images_for_solutions_bacpac1.jpg) 

Right\-click on database and choose **Task \> Export Data\-tier Application**. Click Next and choose where you want to save your BACPAC file. 

If you want to save it on local HDD, choose "Save to local disk" and browse the location where you want to save this file on your local computer. 

![](images/Support_Support_Wiki_Images_Images_for_solutions_bacpac2.jpg) 

If you want to deploy it to Azure storage, choose "Save to Windows Azure", click **Connect** and type your **Storage Account** and **Storage Key** and choose **Container**. If you want to change BACPAC temporary name and location, change the file name and browse the location. This temporary file and location is file where system will put BACPAC file before it’ll be uploaded to Azure storage; after that system will delete it. Click **Next** and **Finish** and wait. System will create BACPAC file.
