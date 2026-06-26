---
title: Failed to load control 'C1Elastic' from C1Sizer.ocx
tags:
- Solution
description: 'To resolve issue mentioned, C1Sizer.ocx has to be unregistered and registered
  via command prompt to its default location. See instruction below: Run…'
created: '2017-03-22'
modified: '2017-03-22'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Failed%20to%20load%20control%20'C1Elastic'%20from%20C1Sizer-ocx.aspx
---

To resolve issue mentioned, C1Sizer.ocx has to be unregistered and registered via command prompt to its default location.

See instruction below:

Run command prompt as Administrator.   
First locate c1sizer.ocx   
As a default location for :   
64 bit machines C:\\Windows\\SysWOW64   
32 bit machines C:\\Windows\\System32   


Change to that location 

First unregister :\-   
regsvr32 –u   C:\\Windows\\system32\\c1sizer.ocx        
Then register :\-   
regsvr32   C:\\Windows\\system32\\c1sizer.ocx
