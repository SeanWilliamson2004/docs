---
title: V3 Licencing - DeviceID
tags: []
description: Background Our Excelerator software has always tried to identify the
  PC it is running on for licencing purposes. Typically, it would look at various…
created: '2024-02-27'
modified: '2024-02-28'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/V3%20Licence%20Methods%20-%20DeviceID.aspx
---

## Background

Our Excelerator software has always tried to identify the PC it is running on for licencing purposes.  Typically, it would look at various characteristics of the PC, and create an identifier string or number (and ID) that represents those characteristics.  This ID needs to remain unchanged; otherwise, the licence granted to a PC might suddenly expire.    

This has proven challenging.   PC architecture has changed over the years.  Characteristics that were considered static became virtual, meaning that licences would start to expire following an upgrade of PC or the introduction of virtual PCs.  

The algorithms used in V1 are detailed here: [V1 Licence Methods.aspx](V1 Licence Methods.md).  

V3 uses different algorithms.   Earlier versions used the SoftwareKey library.  This changed as of release [Release 3\.3\.137 (codis.co.uk)](https://help.codis.co.uk/articles/#%21sage-200-excelerator-online-help-publication/release-notes-3-3-137), as Intellerator needed to use a library that worked with .net 6\.  

## V3 Device ID Algorithms

This uses this https://github.com/MatthewKing/DeviceId?tab\=readme\-ov\-file library.

Because of possible issues we encountered with WMI corruption, a fallback algorithm was used.  

We first attempt to query the WMI database to get the machine name, the processor ID, the motherboard serial number and the system drive serial number.  It will build an id using these.  

However, corruption of the WMI database is quite common, so we fall back to using [DeviceId.Windows](https://www.nuget.org/packages/DeviceId.Windows) to get an ID based on the Machine Name \+  adds the machine GUID from `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Cryptography.`  
If that fails, it then uses DeviceID to get the machine name.
