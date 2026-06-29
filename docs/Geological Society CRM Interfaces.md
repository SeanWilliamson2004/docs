---
title: Geological Society CRM Interfaces
tags: []
description: These interfaces superceeded the FelineSoft interfaces . The interfaces
  import data from a CRM system - a customised Dynamics CRM, into Sage200. The…
created: '2025-08-20'
modified: '2025-08-20'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Geological%20Society.aspx
---

These interfaces superceeded the [FelineSoft interfaces](Geological Society Felinesoft interfaces.md).  

The interfaces import data from a CRM system \- a customised Dynamics CRM, into Sage200\.   The interfaces are a combination of Excelerator imports and Orchestrator exports.  There are plans to move the Excelerator imports to Orchestrator at some point.  The Excelerator imports use the CSV Import tool.  

The touchpoints are:  

| **Touchpoint** | **Notes** |
| --- | --- |
| CRM customers \=\> Sage customers | Customers Excelerator import |
| CRM customers \=\> Sage customer contacts | Customers Excelerator import (at the same time as customers). |
| Sage products \=\> CRM | Orchestrator export |
| Sage stock levels \=\> CRM | Orchestrator export |
| CRM sales orders \=\> Sage sales orders | Sales Orders Excelerators import. |

Other touchpoints were considered and progressed, but it was decided to limit the scope of the implementation.  

Sales Cash  
Sales Invoices
