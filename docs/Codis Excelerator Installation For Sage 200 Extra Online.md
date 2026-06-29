---
title: Codis Excelerator Installation For Sage 200 Extra Online
tags:
- Excelerator
- Sage 200
- Sage 200 Extra Online
description: 'Installation of SDBX Add-On In System Administration App Important Note:
  SDBX Add-On should be installed only once for the entire…'
created: '2018-02-07'
modified: '2020-05-28'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Codis%20Excelerator%20Installation%20For%20Sage%20200%20Extra%20Online.aspx
---

## Installation of SDBX Add\-On In System Administration App

**Important Note:** **SDBX Add\-On should be installed** **only once for the entire company/organisation** **by running Sage 200 System Administration App on that Customer's PC who has access to Sage 200 System Administration logging in by using their Sage ID.**

1\. Find out Sage 200 Extra Online Version by logging into [**https://www.sageerponlineservices.com**](https://www.sageerponlineservices.com/) with the customer's Sage ID. Check respective site Sage version.

![](images/Support_Support_Wiki_Images_Sage_200_Extra_Online_Excelerator_Installation_Capture.JPG)  

2\. Get the latest SDBX Add\-On file location from Agam for the required Sage 200 Excelerator to be installed based on the version found in Step 1\. Transfer the respective SDBX file through TeamViewer on Customer's PC who has got access to Sage 200 System Administration App. Example shown below  
 ![](images/Support_Support_Wiki_Images_Sage_200_Extra_Online_Excelerator_Installation_Capture1.JPG)

3\. Logon to Sage 200 System Administration App with customer's Sage ID who has got access to it.

![](images/Support_Support_Wiki_Images_Sage_200_Extra_Online_Excelerator_Installation_Capture2.JPG) 

4\. On the left hand side pane, right click on **Add\-Ons** Tab and select **Add New Add\-On**

![](images/Support_Support_Wiki_Images_Sage_200_Extra_Online_Excelerator_Installation_Capture3.JPG) 

5\. Click Next

![](images/Support_Support_Wiki_Images_Sage_200_Extra_Online_Excelerator_Installation_Capture4.JPG) 

6\. Browse and select the transferred SDBX file from user's PC. Click on Next.

![](images/Support_Support_Wiki_Images_Sage_200_Extra_Online_Excelerator_Installation_Capture5.JPG) 

7\. Ignore the digital signature warning and click on "I wish to proceed even though the package does not have a digital signature." Click Next

![](images/Support_Support_Wiki_Images_Sage_200_Extra_Online_Excelerator_Installation_Capture6.JPG) 

8\.  Click on Finish. SDBX file is now installed successfully.

![](images/Support_Support_Wiki_Images_Sage_200_Extra_Online_Excelerator_Installation_Capture7.JPG) 

## Install Codis Sage 200 Excelerator

On the client PC who needs excelerator, check that user has **[Sage 200 Extra Online Client App](Sage 200 Extra Online Client App Installation.md)** installed on their PC. Then do the standard Sage 200 Excelerator installation by running the relevant transfered/copied/downloaded StandardSage200vXXXXExceleratorSuite\_xx.x.x.x.exe as Administrator and following through the setup wizard clicking few Next Tabs and finally Finish Tab.

## Amend the Config File

Sage 200 Excelerator on\-line Installation requires that the ClientID \& Audience is inserted to the Codis.Excelerator.Sage200\.Standard.Addin.dll.config file \<AppSettings\> section.   
1\. To locate the exact settings for a specific customer \-\> you need to open the Sage200Desktop.exe.config file on that customer's PC.    
The location of this file is stored in the system registry \-\> Win\+R to open the Run dialog and type **regedit** and click OK or type **regedit** in search bar.

![](images/Support_Support_Wiki_Images_Sage_200_Extra_Online_Excelerator_Installation_Capture8.JPG)  
2\. Look for the following registry key \-\> **HKEY\_CURRENT\_USER\\Software\\Sage\\MMS\\ClientInstallLocation**   
Double click the **ClientInstallLocation** registry key and copy the Value data. 

(For example C:\\Users\\\<Your Username\>\\AppData\\Local\\Apps\\2\.0\\XWY6QC4X.3KP\\HVB6TX78\.RJH\\sage..tion\_f25e6d24a212fa69\_0014\.0000\_bad744f60e0581b5\)

![](images/Support_Support_Wiki_Images_Sage_200_Extra_Online_Excelerator_Installation_Capture9.JPG) 

3\. Open the copied folder location through Windows Explorer. Select the **Sage200Desktop.exe.config** file and open with Notepad

![](images/Support_Support_Wiki_Images_Sage_200_Extra_Online_Excelerator_Installation_Capture10.jpg) 

4\. Locate the appSettings section and copy the **sci:ClientID** and **sci:Audience**keys underneath **\<!\-\- Sage ID settings \-\-\>**.

![](images/Support_Support_Wiki_Images_Sage_200_Extra_Online_Excelerator_Installation_Capture11.jpg) 

5\. These settings are required to be inserted into **Codis.Excelerator.Sage200\.Standard.Addin.dll.config** file in C:\\Users\\\<Your Username\>\\AppData\\Local\\Codis Limited\\Codis Sage 200 2016 Standard Excelerator location. Open Codis.Excelerator.Sage200\.Standard.Addin.dll.config file with Notepad.

![](images/Support_Support_Wiki_Images_Sage_200_Extra_Online_Excelerator_Installation_Capture12.jpg) 

6\. Insert the copied **sci:ClientID** and **sci:Audience** keys under **\<appSettings\>** section which is

mostly towards the end of the file as shown below

![](images/Support_Support_Wiki_Images_Sage_200_Extra_Online_Excelerator_Installation_Capture13.jpg) 

7\. **Save** and **close** the Codis.Excelerator.Sage200\.Standard.Addin.dll.config file.

## Licence Codis Sage 200 Excelerator

Run **Excel.exe** as administrator and click on Excelerator Tab. Licence the same way as standard Sage 200 Excelerator installation.

![](images/Support_Support_Wiki_Images_Sage_200_Extra_Online_Excelerator_Installation_Capture15.jpg) 

Once licenced properly Codis Excelerator For Sage 200 Extra Online is all installed and configured successfully and can be accessed the usual way clicking on Excelerators Tab inside Microsoft Excel.
