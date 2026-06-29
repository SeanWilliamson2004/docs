---
title: Requested registry access is not allowed
tags:
- Solution
description: 3 Solutions for Reqistry access This is the message in Excelerator we
  expect if solution 1 or 2 are required :- Requested registry access is not…
created: '2017-03-31'
modified: '2017-05-25'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Requested%20registry%20access%20is%20not%20allowed.aspx
---

**3 Solutions for Reqistry access**

This is the message in Excelerator we expect if solution 1 or 2 are required :\- Requested registry access is not allowed   
**Solution 1**  
Run regedit   ( as admin)   
Give user permissions to :   
In the Registry   
\>HKEY\_LOCAL\_Machine\\ SOFTWARE\\Microsoft\\Office\\15\.0\\ClicktoRun\\REGISTRY\\MACHINE\\Software\\Wow6432Node\\Codis   
Also check this folder permissions:\-   
Access to the registry (this entry was not there on Karol's PC and EE worked without it. key 'HKEY\_LOCAL\_MACHINE\\Software\\Codis\\Enterprise\\Security\\Settings'      

**Solution 2**   
Access to the registry key 'HKEY\_CURRENT\_USER\\Software\\Microsoft\\Office\\Excel\\AddIns\\ADXXLForm' is denied.   
Go into regedit.exe (just type regedit in Windows search) and right click the above folder \-\> Permissions. Tick the full control tickbox. (Give full access to Addins folder).  

**Solution 3** 

if the registry key is not there go into Excel as administrator.   
On the first addin tab, click on options   
Edit the Authentication address by adding a 1 behind it then search for that value in the registry.   
The value to search for will be: \- "AuthenticationService1" 

When you find the folder   
Give permissions to everyone or to the current user  
 you can change the setting in the registry back to Authentication Service

OR change the setting back in Excelerator before you exit as administrator and login as the user.

![](images/Support_Support_Wiki_Images_Images_for_solutions_regisrty1.jpg) 

This screen shot above shows the entry into the registry added by the Codis installation of Enterprise Excelerator. (On a 64 bit PC)  

Either permission to access this key is removed or the complete entry is removed.

If the entry is there grant permission to everyone.  If not you can add this key by logging into Excel as administrator. Then go to the Excelerator tab and rather than logging in go to Options.

![](images/Support_Support_Wiki_Images_Images_for_solutions_registry2.jpg) ![](images/Support_Support_Wiki_Images_Images_for_solutions_registry3.jpg)

That takes you to this screen. Change the entry highlighted to AuthenticationService1/   

Then close Excel and search the registry (logged in as admin) for AuthenticationService1

This action will have created the entry shown in the first screen above. Then you can grant permission to everyone on this folder. 

You can also edit the value of the key from AuthenticationService1 back to Authentication Service. Either here in the registry or by going back into Excel as you did before.
