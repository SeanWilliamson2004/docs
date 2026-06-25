---
title: Configuration of fiscal year and periods
tags:
- Sage X3
description: '1. Open Fiscal year for your company Transaction Code: GESFIY Description:
  Opening Fiscal year Fiscal years managed by legal company. Before…'
created: '2017-01-24'
modified: '2017-01-27'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Configuration%20of%20fiscal%20year%20and%20periods.aspx
---

# 1\. Open Fiscal year for your company

**Transaction Code: GESFIY       Description: Opening Fiscal year** 

Fiscal years managed by legal company. Before performing accounting operations or creating transactions, the accounting financial years must be created and open. This function is therefore used to manage, by company, the status of the financial years. The financial year is defined at the Company level. It cannot be earlier than the start date of the first financial year defined during the creation of the folder. The end date is by default 12 months later from the starting date. 

## Fiscal year beginning and end dates are specific to each company:

• Fiscal year states: Not open / Open / Closed. 

• Impossible to modify the end date of the end of a fiscal year. 

• If the fiscal year is opened for a specific ledger and it will be automatically opened for all the other ledgers for that company. 

**Path: Common data  G/L Accounting Tables  Fiscal years**

# 2\. Opening of Fiscal Periods

**Transaction Code: GESPER       Description: Opening Fiscal Periods** 

The accounting periods related to financial year must be created and opened before performing transactions. 

•       The period start date for the first period is based on the start date for the fiscal year and cannot be changed. 

•       The period end date for the last period is based on the fiscal year end date and cannot be changed. 

**Path: Common data  G/L Accounting Tables  Fiscal periods** 

Period Status The Period status column specifies if the period is open or closed to perform activity. To open a period, click Opening. We can only open periods within a fiscal year that is also open. 

Stock Status The Stock status column specifies if the period is open to any stock movements. Stock movements include such transactions as adjustments, receipts, and shipments. For example, we can have a period open for any necessary period\-end adjustments that still must be made but prevent any stock movement transactions from posting to that period. The statuses available include: 

•        Open \- The period is open to all stock movements. 

•        Balance adjustment – The period is open to only stock adjustment transactions. 

•        Closed – No stock movement transactions can post. 

Before you can close a fiscal year, the periods associated with that year must also be closed. You can close a period directly in this task by clicking Close. Periods are closed one after the other.
