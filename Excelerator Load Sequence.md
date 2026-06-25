---
title: Excelerator Load Sequence
tags:
- Excelerator
- Development
description: This is a description of the load sequence for Excelerator and is intended
  for developers.…
created: '2017-01-26'
modified: '2017-01-26'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Excelerator%20Load%20Sequence.aspx
---

**This is a description of the load sequence for Excelerator and is intended for developers.** 

[https://www.add\-in\-express.com/docs/net\-deploying\-addins.php](https://www.add-in-express.com/docs/net-deploying-addins.php) 

1. Excel loads registered COM\-Addins. The COM registration includes a path to the Dll Adx Shared Addin Codis.Excelerator.Standard.SharedAddin.dll is loaded as it is a registered COM\-Addin.
2. Event handler AddinModule\_OnRibbonBeforeCreate in SharedAddinModule.vb is invoked.
3. The GetContainers method searchs for all Container definitions (files named Codis.Excelerator.\*.ContainerDef.xml) in the folder where the dll is. The ContainerDef should contain the name of an Assembly and a method name that creates a Windsor container.
4. It then instantiates that assembly and invokes the method, and adds some common configuration to the Windsor container.
5. Next, the registered object for type ExceleratorLoader is found in the container and added to a list of loaders.
6. The method LoadRibbon is run for all ExceleratorLoader objects.
