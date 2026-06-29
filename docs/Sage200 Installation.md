---
title: Sage200 Installation
tags: []
description: Steps for Sage Installation For installation on AVD, Local Admin account
  with installation permission will be required to install Sage Server and…
created: '2026-06-01'
modified: '2026-06-01'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Sage%20200%20Installation%20Steps.aspx
---

Steps for Sage Installation 

For installation on AVD, Local Admin account with installation permission will be required to install Sage Server and SQL. 

Step 1\.

Web Server (IIS) \> Web Server \> Common HTTP Features

- Default Document
- Directory Browsing
- HTTP Errors
- HTTP Redirection
- Static Content

Web Server (IIS) \> Web Server \> Application Development

- .NET Extensibility 4\.5 (or later)
- Application Initialization
- ASP
- ASP .NET 4\.5 (or later)
- ISAPI Extensions
- ISAPI Filters

Web Server (IIS) \> Web Server \> Security

- Request Filtering
- Windows Authentication

Web Server (IIS) \> Web Server \> Management Tools

- IIS Management Console

Web Server (IIS) \> Management Tools \> IIS 6 Management Compatibility

- IIS 6 WMI Compatibility
- IIS 6 Metabase Compatibilit

Step 2\.

Features  

![Step2-1.png](images/PublishingImages_Pages_Sage200_Installation_Step2-1.png)  

![Step2-2.png](images/PublishingImages_Pages_Sage200_Installation_Step2-2.png)  

![Step2-3.png](images/PublishingImages_Pages_Sage200_Installation_Step2-3.png)  

Step 3.

After selecting Roles and features, download SQL Server as per supported version with Sage from below link  

[Downloads \& Keys \- Visual Studio Subscriptions](https://my.visualstudio.com/Downloads?q=Windows%2010) 

Launch Setup.exe from ISO  

Click Installation as per screenshot

![Step3-1.png](images/PublishingImages_Pages_Sage200_Installation_Step3-1.png)  

 ![Step3-2.png](images/PublishingImages_Pages_Sage200_Installation_Step3-2.png)  

![Step3-3.png](images/PublishingImages_Pages_Sage200_Installation_Step3-3.png)  

Click Accept Next\>Next\>Next

 ![Step3-4.png](images/PublishingImages_Pages_Sage200_Installation_Step3-4.png)  

![Step3-5.png](images/PublishingImages_Pages_Sage200_Installation_Step3-5.png)   

![Step3-6.png](images/PublishingImages_Pages_Sage200_Installation_Step3-6.png)   

Click Collation 

Collation Must be Latin1\_General\_CI\_AS or check Sage guide. Click Customize to select correct Collation. 

![collation1.png](images/PublishingImages_Pages_Sage200_Installation_collation1.png)  

![collation2.png](images/PublishingImages_Pages_Sage200_Installation_collation2.png)  

Click Mixed Mode and enter password, click Add Current user 

![collation3.png](images/PublishingImages_Pages_Sage200_Installation_collation3.png)  

Note:\- Select Data Directories next to Server Configuration in case C drive doesn't have much space or sql needs to be installed on other drive.            If max memory usage by SQL need to be cap, select memory and use recommedned and select maximum memory.   

![colaltion4.png](images/PublishingImages_Pages_Sage200_Installation_colaltion4.png)  

Click Install.   

Step 4\.

Installation for Sage Server,   
Create S200Admins and S200Users group  
 Create S200SecuredServices and S200Services users with password expiry never  
 Make Current user and S200Services as member of S200Admins  
 Download Sage version and launch setup.exe. 

![Step4-1.png](images/PublishingImages_Pages_Sage200_Installation_Step4-1.png)![step4-2.png](images/PublishingImages_Pages_Sage200_Installation_step4-2.png) ![Step4-3.png](images/PublishingImages_Pages_Sage200_Installation_Step4-3.png) Enter the user names and passwords for the windows user accounts that you've set up to run Sage 200 Services and Sage 200 Secured Services. Click Install

From C:\\Sage\\Installers, install SA and Client.   

Post Installation:\-   

1\.       Local Intranet zone. 

a. In Windows settings, open Internet Options. 

b. Go to the Security tab, then select the Local intranet zone and select Custom Level. 

c. Set user User Authentication \> Logon to Automatic Logon with current user name and password.

2\.       Alternative Client Installation Method  

![Altrnative.png](images/PublishingImages_Pages_Sage200_Installation_Altrnative.png)  

  Unzip this file to any directory of your choice.  

 Return to the Installers folder in the Sage share directory, typically C:\\Sage\\Installers. Copy the file Sage200CommonAppSettings.config

Paste this into the extracted folder you created previously.  

Run the Sage200Dektop.exe file, you can also create a shortcut icon on the desktop that points to the Sage200Desktop.exe file within that folder. From here, the program can be launched in the normal manner.  

[Sage 200 \- Alternative Client Installation Method for remote desktop services environments](https://gb-kb.sage.com/portal/app/portlets/results/viewsolution.jsp?solutionid=200427112510764&page=1&position=0&q=alternative%20installation)  

3\.      Folders that stores Sage UI data

C:\\Users\\AnkitJain\\AppData\\Roaming\\Sage  

4\. Registry holding sage folder location  

Registry Editor\>Computer\\HKEY\_CURRENT\_USER\\Software\\Sage\\MMS
