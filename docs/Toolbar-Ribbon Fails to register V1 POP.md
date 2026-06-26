---
title: Toolbar/Ribbon Fails to register V1 POP
tags:
- Solution
description: POP S1000 toolbar fails to register 2013 onwards The file MSADDNDR.DLL
  needs to be on the system. This file is added in our installers and installs…
created: '2017-03-22'
modified: '2017-03-22'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/ToolbarRibbon%20Fails%20to%20register%20V1%20POP.aspx
---

POP S1000 toolbar fails to register 2013 onwards   
The file **MSADDNDR.DLL** needs to be on the system.   
This file is added in our installers and installs with the excelerator but if it not present on the system then the following steps need to be taken.    


Places to check that the file is present are:   
• The Codis Install folder (or folder where the downloaded file was extracted to).   
• C:\\Program Files (x86\)\\Codis Excelerator   
• C:\\Program Files (x86\)\\Common Files\\DESIGNER   
• C:\\Program Files (x86\)\\Common Files\\Codis 

  
If this file is not there then it has to be copied to the following location:   
C:\\Program Files (x86\)\\Common Files\\DESIGNER 

  
After the file has been copied to the above location then:   
• Run Command Prompt as Administrator   
• C:\\Program Files (x86\)\\Common Files\\DESIGNER\>regsvr32 msaddndr.dll   
• C:\\Program Files (x86\)\\Codis Excelerator\>regsvr32 POOrderExcel.dll   
If you can’t register POOrderExcel.dll using the above path then register it using the path below:   
  
• Wasn’t the path also C:\\Program Files (x86\)\\Common Files\\Codis\>Regsvr32 POOrderExcel.dll
