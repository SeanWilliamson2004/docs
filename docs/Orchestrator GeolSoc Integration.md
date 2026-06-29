---
title: Orchestrator GeolSoc Integration
tags: []
description: For GeolSoc integration with Orchestrator, currently we are providing
  the Export feature only for exporting data of Stock, Stock levels and Nominal…
created: '2024-07-03'
modified: '2024-07-26'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Orchestrator%20GeolSoc%20Integration.aspx
---

For GeolSoc integration with Orchestrator, currently we are providing the Export feature only for exporting data of Stock, Stock levels and Nominal codes to flat files i.e. xlsx and csv only.

GeolSoc Export plugins in Orchestrator keeps track of last Sync time and fetch data after lastSyncTime only and produces the output file in the specified folder.  

**Resetting sync time to reload all data**

We keep track of last export's Sync time for each module in Orchestrator's database table i.e. GeolSocExportSyncTime. When there is no last sync time entry in this table for the specific module, then export will fetch all data related to that module and save the last sync time in the table. Afterwards, the lastSyncTime will be used to fetch updated data only.  

If we need to reset the export's last sync time to fetch all data, we need to delete the specific modules' entry from the give table i.e. GeolSocExportSyncTime from Orchestrator database.  

Below shows the information needed to do a manual run or Creating Schedule for GeolSoc export plugin.

**Export file type:** It can either be xlsx or csv

**Range definition file:**  Range definition file according to which data is written on the file. 

**NOTE:** Range definition file can be created/modified from Excelerator only for Stock. For Stock Level and Nominal code, the file has to be manually modified if needed. Range definition file for each module/plugin is         attached below  

**Output folder:** Folder where output files will be produced.

**Sage company:** Sage company to fetch data from.  

*\[image: GeolSocExportPlugin.jpg not found]*  

**Range Definition files:**  

**[StockRangeDefinition.def](https://codislimited.sharepoint.com/sites/Wiki/Pages/StockRangeDefinition.def)**

**[StockLevelRangeDefinition.def](https://codislimited.sharepoint.com/sites/Wiki/Pages/StockLevelRangeDefinition.def)**

[NominalCodeRangeDefinition.def](https://codislimited.sharepoint.com/sites/Wiki/Pages/NominalCodeRangeDefinition.def)  

[CustomerRangeDefinition.def](https://codislimited.sharepoint.com/sites/Wiki/Pages/CustomerRangeDefinition.def)
