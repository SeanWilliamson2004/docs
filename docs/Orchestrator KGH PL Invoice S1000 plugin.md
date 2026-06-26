---
title: Orchestrator KGH PL Invoice S1000 plugin
tags: []
description: Overview This is a Orchestrator plugin used to process S1000 PL Invoice
  for KGH. Description This plugin uses S1000 PL Invoice service installed on…
created: '2025-08-20'
modified: '2025-08-20'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Orchestrator%20KGH%20PL%20Invoice%20S1000%20plugin.aspx
---

**Overview**  


This is a Orchestrator plugin used to process S1000 PL Invoice for KGH.  


**Description**

This plugin uses S1000 PL Invoice service installed on the server. Orchestrator acts as a client for the wcf service.  


Orchestrator reads file from a specified folder using Range definition and sends them to the wcf service for processing.  


  


**Licence**

Customer must have S1000 Enterprise PL Invoice licence i.e. W1000PLIMDPR on the server  


**Sample files**

Sample csv file and range definition files are attached below  


[PLInvoiceS1000\.csv](https://codislimited.sharepoint.com/sites/Wiki/SiteAssets/Pages/Orchestrator%20KGH%20PL%20Invoice%20S1000%20plugin/PLInvoiceS1000.csv)[PLInvoiceS1000\.def](https://codislimited.sharepoint.com/sites/Wiki/SiteAssets/Pages/Orchestrator%20KGH%20PL%20Invoice%20S1000%20plugin/PLInvoiceS1000.def)    


  


**Note**: KGh is not using Orchestrator anymore for PL Invoice processing as licences in CRM are expired and Sean also confirmed that.
