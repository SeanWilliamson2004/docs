---
title: Error while trying to log on - Sage 200
tags: []
description: ID 7529 Issue Details 200c and if you enable enforced login and then
  close the program the next time you try and access it you get a error message:…
created: '2021-10-13'
modified: '2021-10-13'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Error%20while%20trying%20to%20log%20on%20-%20Sage%20200.aspx
---

#### ID 7529 Issue Details

200c and if you enable enforced login and then close the program the next time you try and access it you get a error message:  
Could not load file or assembly 'Sage.Common.Controls, Version\=19\.0\.0\.0, Culture\=neutral, PublicKeyToken\=b2daa66d74953d11' or one of its dependencies. The system cannot find the file specified.  

**Steps to replicate**  
• Open System Admin  
• Enable enforced login  
• Close and then reopen System Admin  

**Observed behaviour**  
You will get an error  

System.IO.FileNotFoundException, mscorlib, Version\=4\.0\.0\.0, Culture\=neutral, PublicKeyToken\=b77a5c561934e089  
Could not load file or assembly 'Sage.Common.Controls, Version\=19\.0\.0\.0, Culture\=neutral, PublicKeyToken\=b2daa66d74953d11' or one of its dependencies.  

**Expected behaviour**  
You should be able to access SA  

**Workaround**  
In the Config Database go to tblparameters and then the Enforced Login column and change from True to False. Retry System Administrator.
