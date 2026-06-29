---
title: Sage 200 Excelerator Assembly Resolution
tags:
- Excelerator
- Support
- Development
description: Sage 200 Excelerator uses the Sage 200 API which is included with the
  assemblies ( https://docs.microsoft.com/en-us/dotnet/standard/assembly/ )…
created: '2020-03-27'
modified: '2020-03-31'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Sage%20200%20Excelerator%20Assembly%20Resolution.aspx
---

Sage 200 Excelerator uses the Sage 200 API which is included with the assemblies ([https://docs.microsoft.com/en\-us/dotnet/standard/assembly/](https://docs.microsoft.com/en-us/dotnet/standard/assembly/)) installed on any Sage client.   In order to use these assemblies, it has to find them on the computer.  

It uses the algorithm below to find them.  This method can be flawed and will only be used if the assembly hasn't somehow been loaded.  If there are other versions of the assemblies on the PC then if the wrong version of Sage.MMS.SAA.Client.dll is loaded, and then an error may occur.  This error may   

1. Look for registry key HKCU\\SOFTWARE\\Sage\\MMS\\ClientInstallLocation.  If it exists and if the path defined in it exists, use the path in it.
2. Otherwise look in HKLM\\SOFTWARE\\Sage\\MMS\\ClientInstallLocation.  If it exists and if the path defined in it existsuse the path in it.
3. If the assembly exists at this location, load it.
