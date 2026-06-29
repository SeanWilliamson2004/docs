---
title: Workflow for Implementing Snapshot versioning
tags:
- Development
description: Seperate the paket.dependencies and paket.references into two sections
  - one for snapshot versions and one for production builds. framework:…
created: '2017-03-16'
modified: '2017-03-29'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Workflow%20for%20Implementing%20Snapshot%20versioning.aspx
---

Seperate the paket.dependencies and paket.references into two sections \- one for snapshot versions and one for production builds.  

```
framework: auto-detect

source https://www.nuget.org/api/v2

source http://nuget.codis.co.uk/nuget

source C:\Nuget.Local



nuget Codis.Sage200.Base.Types

nuget Newtonsoft.Json



group LOCAL

	http file://C:/Users/SWilliamson/Source/Repos/CodisDevelopment/Assemblies/Codis.Excelerator.Plugin.Types.dll

	

group BUILD

	source C:\Nuget.Local

	nuget Codis.Excelerator.Plugin.Types


```

Public Class Class1  
    Dim i As Integer  
End Class

```
Public Class Class1

    Dim i As Integer

End Class


```

Note: I cannot get paket.local redirects to work with http so can't use that solution.

Use the http source with the file protocol
