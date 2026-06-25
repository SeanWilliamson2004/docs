---
title: Excelerator Installation in Citrix
tags:
- Solution
description: 'Download correct version of Excelerator from our website: http://www.codis.co.uk/excelerator/download
  Save the setup to the folder C:\Codis Install…'
created: '2017-03-16'
modified: '2022-03-15'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Excelerator%20Installation%20in%20Remote%20Desktop%20Server%20and%20Citrix.aspx
---

Download correct version of Excelerator from our website: <http://www.codis.co.uk/excelerator/download>

Save the setup to the folder C:\\Codis Install and follow step by step instructions (with screenshots) on how to install Excelerator on Citrix below.

- Need to have local admin privileges
- Run "CMD" as administrator
- Change Logon /Query (command can be used to find the current mode)

            ![](images/Support_Support_Wiki_Images_Images_for_solutions_citrix1.jpg)  


- Need to disable all users: (It is extremely important to check before running this command as this will log everyone out).
- Change Logon /Disable (turn off the logged client sessions)

            ![](images/Support_Support_Wiki_Images_Images_for_solutions_Citrix2.jpg)

- Put SERVER in Install Mode
- Change User/Install

          ![](images/Support_Support_Wiki_Images_Images_for_solutions_cirtix3.jpg)

- Install (while at Install Mode)  
Change directory in control panel to the location where setup (MSI) is copied \- cd \<location\>

          ![change location.png](images/PublishingImages_Pages_Excelerator_Installation_in_Citrix_change_location.png)

       Type msiexec /a \<setup name\> and press enter to run the MSI  


  


         ![MSI command.png](images/PublishingImages_Pages_Excelerator_Installation_in_Citrix_MSI_command.png)  


       Install the MSI in a centralised location for eg \- C:\\Program Files (x86\)  


       Go to the install location from windows explorer, edit adxloader.dll.manifest and change the privileges to administrator and save the file  


         ![Privileges.png](images/PublishingImages_Pages_Excelerator_Installation_in_Citrix_Privileges.png)  


           


  


       Open CMD as admin and navigate to the install location \- cd \<location\>  


          Run command in CMD \- adxregistrator.exe /install\=Codis.Excelerator.Sage200\.Standard.Addin.dll /privileges\=administrator     

        ![administrator command.png](images/PublishingImages_Pages_Excelerator_Installation_in_Citrix_administrator_command.png)  


- Then change back to Execution mode
- Change User/Execute

        ![](images/Support_Support_Wiki_Images_Images_for_solutions_citrix5.jpg)

- Enable client logons
- Change Logon/Enable

           ![](images/Support_Support_Wiki_Images_Images_for_solutions_citrix6.jpg)

- Check if each users have been licensed.
