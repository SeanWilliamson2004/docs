---
title: S200 Cash Entry and Allocation Excelerator
tags: []
description: 'This document describes the functionality released in May 2021 for the
  two menu options in S200 Excelerator: SL Receipt Allocation PL Pay Allocation…'
created: '2021-04-18'
modified: '2023-08-23'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/S200%20Cash%20Entry%20and%20Allocation.aspx
---

This document describes the functionality released in May 2021 for the two menu options in S200 Excelerator:  

- SL Receipt Allocation
- PL Pay Allocation

These provide the functionality for Sales and Purchase ledger to:  
1. Create cash items
2. Create and allocate cash items against invoices
3. Allocate existing open items (invoices, cash, credit notes etc) against one another.

The Excelerator will have two modes, depending on ranges on the sheet.  The first mode covers 1\. and 2\. \- where cash items are created.  Having a bank range on the sheet indicates this mode is active.  The other mode is for only allocations without any cash items being created.  

A typical sheet for just creating cash items might look like this...  

| Bank Code | 1 |  |  |  |  |
| --- | --- | --- | --- | --- | --- |
| Bank Name | Barclays Bank PLC |  |  |  |  |
| Supplier | Short Name | Account Name | Reference | Second Reference | Cash Amount |
| ABC001 | ABCooker | AB Cookers | ABCCSH1 | ABCSEC1 | 500\.00 |
|  |  |  | ABCCSH2 | ABCSEC2 | 200\.00 |
| DIR001 | Direct | Direct | CBRCSH1 | CBRSEC1 | 50\.00 |
|  |  |  | CBRCSH2 | CBRSEC2 | 70\.00 |

For cash creation and allocation.   For this, note that the cash payments appear as positive.  The browse on items to allocate to should only show debits  

| Bank Code | 2 |  |  |  |  |  |  |  |  |  |  |  |  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Bank Name | Barclays Bank |  |  |  |  |  |  |  |  |  |  |  |  |
| Supplier | Short Name | Allocation Date | Account Name |  | Reference | Second Reference | Alloc This Time | Cash Amount | URN | Reference | Second Reference | Outstanding | Allocate Amount |
| BGT001 | BGT Dist |  | BGT Dist |  |  |  |  |  | 6967 | BGT001\_ 04/06/2009 |  | 178\.75 | 178\.75 |
|  |  |  |  |  |  |  |  |  | 7355 | BGT001\_ 18/06/2009 |  | 315\.37 | 315\.37 |
|  |  |  |  |  |  |  |  |  | 7938 | BGT001\_ 09/07/2009 |  | 291\.92 | 291\.92 |

Allocations without creation of a cash item are done in a single set of columns.  Note that in this mode, both credit and debits are available from the browse, and that debitsappear as negatives...  

| Supplier | Short Name | URN | Ref | Outstanding | Allocate Amount |
| --- | --- | --- | --- | --- | --- |
| BGT001 | BGT Dist | 13482 | BGT001\_ 04/06/2009 | \-315\.37 |  |
|  |  | 7553 | BGT001\_ 25/06/2009 | \-291\.92 |  |
|  |  | 27067 |  | 240\.00 | 240\.00 |
|  |  | 26985 | 8445 | 264\.38 |  |
|  |  | 26992 |  | 174\.94 |  |
