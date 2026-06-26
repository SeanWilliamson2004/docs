---
title: Patterson and Rothwell Interfaces
tags: []
description: The Patterson and Rothwell interfaces are Orchestrator Sales Order interfaces.
  Patterson and Rothwell receive Sales Orders as pdf that they convert…
created: '2023-05-19'
modified: '2023-05-19'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Patterson%20and%20Rothwell%20Interfaces.aspx
---

The Patterson and Rothwell interfaces are Orchestrator Sales Order interfaces.  


Patterson and Rothwell receive Sales Orders as pdf that they convert to Excel using a tool.  These Excel files are then saved to a folder and are processed by Orchestrator.  


  


The original WI is https://dev.azure.com/codislimited/CodisDevelopment/\_workitems/edit/3009\.  Other WIs for work done for P\+R are tagged with P\+R.  


They've had two customisations made:  


- S200 Sales and Purchase Order MMS178 Excelerator support https://dev.azure.com/codislimited/CodisDevelopment/\_workitems/edit/3134\.  This is an API plugin: https://dev.azure.com/codislimited/CodisDevelopment/\_git/PattersonAndRothwell?path\=/Codis.PattersonAndRothwell.Customisation/Server/SalesOrderServerAPI.cs
- Orchestrator for Sage 200 Sales Orders to pick delivery address based on postcode https://dev.azure.com/codislimited/CodisDevelopment/\_workitems/edit/3412\. This is an interface plugin:
