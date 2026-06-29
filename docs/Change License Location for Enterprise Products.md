---
title: Change License Location for Enterprise Products
tags: []
description: Default Location The default location for Enterprise licenses is C:\ProgramData\Codis\License
  Define location in Codis IP - Login to Codis IP - Go to…
created: '2021-07-30'
modified: '2021-07-30'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Change%20License%20Location%20for%20Enterprise%20Products.aspx
---

Default Location

The default location for Enterprise licenses is C:\\ProgramData\\Codis\\License

Define location in Codis IP  

\- Login to Codis IP  

\- Go to COnfiguration\> System Parameters\> Edit  

\- Change the override license parh to the location we need for License files  

Define location in Database

\- Open Microsoft SQL Server

\- Navigate to Codismaster Database

\- Click on new Query

\- run the query below

Update PolicyValue  

Set Value \= '\<path\>'  

where EnterpriseLicenceFolder like ""  

\*note \- \<path\> is the path we need for license folder. Please enter it without adding \<\>
