---
title: Sage 200 - Attempted to read or write protected memory
tags:
- Sage 200
- Support
description: 'When you access a list view in Sage 200 the icons may be grey or missing
  or you might get one of the following error messages: Attempted to read or…'
created: '2019-07-16'
modified: '2019-07-16'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Sage%20200%20-%20Attempted%20to%20read%20or%20write%20protected%20memory.aspx
---

When you access a list view in Sage 200 the icons may be grey or missing or you might get one of the following error messages:

- Attempted to read or write protected memory.
- Unexpected Exception occurred. The specified resource type cannot be found in the image file.

To resolve this follow the steps below.

#### Sage 200 List View \- Icons are grey or missing or you get an error about protected memory or the specified resource type

 #### 

#### Sage 200 List View \- Icons are grey or missing or you get an error about protected memory or the specified resource type

1. Close Sage 200\.
2. Using Windows Explorer navigate to **C:\\Users\\Username\\AppData\\Roaming\\Sage 200**
3. Delete the file **sage.mms.desktop.common.resources.dll**
4. Open Sage 200.
