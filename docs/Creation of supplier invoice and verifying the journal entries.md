---
title: Creation of supplier invoice and verifying the journal entries
tags:
- Sage X3
description: '1. Creation of Supplier Invoice Transaction Code: GESBIS Description:
  Supplier Invoice The supplier BP invoice entry function is used to manage the…'
created: '2017-01-25'
modified: '2017-01-27'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Creation%20of%20supplier%20invoice%20and%20verifying%20the%20journal%20entries.aspx
---

# 1\. Creation of Supplier Invoice

**Transaction Code: GESBIS       Description: Supplier Invoice** 

The supplier BP invoice entry function is used to manage the supplier invoicing outside of the "typical" purchasing cycle: In this context, it is not necessary to manage the order, the receipt note with stock receipt. 

## Fields explanation:

Site \& Company \- This site which must be a financial one, determines the site and the company for the entry posting. 

Invoice type \- Invoice type code referencing the invoice category as well as the entry structure used upon accounting validation of the invoice. 

Document No. – This number will be auto\-generated based on the sequence number setup and after creating invoice. 

Accounting date \- This date determines the accounting date of the generated journal. 

Supplier – We need to specify/select the BP from the list to be invoiced. 

Collective \- Call code of the BP collective account initialized by default with the accounting code of the invoice BP. 

Tax rule – This field will be fetched based on the BP Supplier setup tax settings. 

Pay\-to – This field is auto\-fetched based on the BP supplier initialization. 

Due date basis – This is the date from which the payment schedule will be calculated. 

Payment terms \- This field indicates the payment conditions that will be applied in order to determine the invoice schedule. The latter can be manually modified later on. 

Discount/bank charge \- Code used by default for the current BP to identify a series of early discount and late charge rates (up to 12\) to be applied to a payment according to a number of days in advance or days late with respect to the open item date. 

**Path: A/P\-A/R Accounting  Invoicing  Supplier BP Invoices** 

## Lines Tab:

Site \- It is possible to modify the site on the line and so to carryout the inter\-site operations in the same legal company. 

Collective Account \- The account posting is determined by: •       By a collective account: the account that is associated with it is displayed by default, the BP must be specified. •       By a general account. •       By the Business partner (BP): by default, the control account code and the associated account are displayed. 

TRA Legal B – This field will be auto\-fetched after selecting the collective code/we need to give the GL account manually to fetch the collective code – vice versa. 

BP – We need to specify the BP supplier used on the Header. 

Inv. amt – tax – This is purely the base amount without tax calculations. 

Tax – We need to specify/select the tax rules from the list. 

Inv. amt \+tax – The field is auto\-fetched and cumulate the tax values with base amount. 

Purchase type \- This field can take two values : Purchase or Fixed assets, It is used to define the VAT type applicable on the invoice line and it therefore conditions the VAT account that will be automatically used upon accounting posting of the document.

# 2\. Journal entry for the Supplier Invoice

**Transaction Code: GESGAS       Description: Journal entry** 

Once the Supplier Invoice is created and posted, the Batch server should be active and Accounting Tasks functions should also be in "Active" status to auto\-generate the Journal entries. Below, we can see the journal entry generated automatically based on the setup used for the invoice types linked with automatic journal. 

**Path: Financials  Journals  Journal Entry** 

## Lines Tab:

**Note:\-** Similarly, the journal entries will auto\-generate for Sales Invoice, Purchase Invoice, Customer Invoices, Payments \& Receipts etc. from all the other relevant modules.
