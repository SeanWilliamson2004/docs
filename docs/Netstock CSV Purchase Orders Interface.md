---
title: Netstock CSV Purchase Orders Interface
tags:
- Orchestrator
description: Overview Codis has worked with Netstock to produce an interface between
  their inventory management software. Their software anticipates demand and…
created: '2021-12-07'
modified: '2023-05-19'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Netstock%20CSV%20Purchase%20Orders%20Interface.aspx
---

## Overview

Codis has worked with [Netstock](https://www.netstock.co/) to produce an interface between their inventory management software.  Their software anticipates demand and produces purchase orders as csv files that are imported into Sage 200 using [Orchestrator (Support notes).aspx](Orchestrator (Support notes).md "Orchestrator").  

It is currently used by Grant UK.  

## Details

Netstock will deposit files into a network share.  This share is used as an exchange for other forms of data so only files of the format po\*.csv will be processed.

Orchestrator will poll this folder on a regular interval e.g. 2 minutes and any files found in this folder will be processed and converted into Sage 200 Purchase orders.  

Successfully processed files will be stored in a folder (path in configuration).  

Failed files will be logged and will be stored in a folder (path in configuration).  

The shorter polling interval is always desirable but opens up the possibility of a new process clashing with a running process.  To this end it may be best to have a process lock that prevents a new import starting with before a previous import has been completed.  However, care must then be taken to try to avoid locks being left on when exception occur, which would then demand support intervention.  

Sample CSV File...  

OrderID, Supplier,Location, CreationDate,User, Email,Item, UOM,Quantity,Cost, DueDate,Comment  

16,CHOFU,G.Uk,2021/12/06,System Administrator,admin@netstock.co,H3223320R32BLYGOLDBODY,Each,23,1661\.76,2021/12/27,16,CHOFU,G.Uk,2021/12/06,System Administrator,admin@netstock.co,HP323323R32BLYGOLDBODY,Each,12,2280\.85,2021/12/27,  

There is one purchase order per CSV file.  In each CSV, the left hand columns contain header information and the right hand column contain detail (po line) information.  The header information is repeated on each detail line.  We have in the past had this flat format data where a change in the header information can indicate a new entity, but in this case no change is expected.  

The OrderID is   

| **CSV Field** | **Description** | **Populates** |
| --- | --- | --- |
| OrderID | Netstock orderID.  This is not used for the purchase order document number.  This is generated using existing API functionality. | It should be stored in a spare analysis code or spare text field.  Which field can be part of the interface configuration. |
| Supplier | Sage supplier.  Does not need to be mapped | PO header Supplier |
| Location | Sage warehouse.  Does not need to be mapped. | PO Header SupplyFrom field (called Supply To on the template) |
| CreationDate | PO Creation date | This is not currently available on our API |
| User | Not clear | User is readonly on our API |
| Email | Email address | PO Header Email |
| Item | Sage produce code.  Does not need to be mapped | PO Detail Code field |
| UOM | Unit of measure | PO Detail Buying Unit |
| Quantity | Quantity | PO Detail Quantity |
| Cost | Cost per unit ? | PO Detail Buying Unit Price |
| DueDate | Request delivery date | PO Detail RequestedDeliveryDate |
