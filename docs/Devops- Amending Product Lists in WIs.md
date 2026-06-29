---
title: 'Devops: Amending Product Lists in WIs'
tags:
- TFS
description: Amending the product lists used in work items is a little laborious.
  Based on instructions in this StackOverflow article. First, you need to export…
created: '2022-06-16'
modified: '2022-06-16'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Devops%20Amending%20Product%20Lists%20in%20WIs.aspx
---

Amending the product lists used in work items is a little laborious.  

Based on instructions in [this StackOverflow article.](https://stackoverflow.com/questions/53268163/import-global-list-to-azure-devops-hosted-xml-process-template#54295011)

First, you need to export the process:  

.![ExportDevOpsProcess.gif](images/PublishingImages_Pages_Devops_Amending_Product_Lists_in_WIs_ExportDevOpsProcess.gif)  

Then, unzip the process file.  

Open CodisDevelopment 1\.3\\WorkItem Tracking\\TypeDefinitions\\Bug.xml  

You will see content like this the sample below.  Its straightforward to add an item to the list.  The relationship between product group and sublists is described in the Fields section further down.    
There does seem to be an issue with adding groups sometimes.  Not sure what it is exactly but e.g. Sage 50 Excelerator products aren't appearing.

\<?xml version\="1\.0" encoding\="utf\-8"?\>\<witd:WITD application\="Work item type editor" version\="1\.0" xmlns:witd\="http://schemas.microsoft.com/VisualStudio/2008/workitemtracking/typedef"\>  \<WORKITEMTYPE name\="Bug" refname\="Custom.Bug"\>    \<DESCRIPTION\>Describes a divergence between required and actual behavior, and tracks the work done to correct the defect and verify the correction.\</DESCRIPTION\>    \<GLOBALLISTS\>      \<GLOBALLIST name\="S1000V3Modules"\>        \<LISTITEM value\="ALL" /\>        \<LISTITEM value\="Aged Creditors" /\>        \<LISTITEM value\="Aged Debtors" /\>        \<LISTITEM value\="Cash Book Multicompany" /\>        \<LISTITEM value\="CashBook Payments" /\>        \<LISTITEM value\="CashBook Receipts" /\>        \<LISTITEM value\="Cost Of Sales" /\>        \<LISTITEM value\="Customers" /\>        \<LISTITEM value\="Exchange Rate" /\>        \<LISTITEM value\="Nominal Ledger Journals" /\>        \<LISTITEM value\="Nominal Posting Codes" /\>        \<LISTITEM value\="Purchase Ledger Invoices" /\>        \<LISTITEM value\="Purchase Order Receipts" /\>        \<LISTITEM value\="Sales Ledger Invoices" /\>        \<LISTITEM value\="Sales Ledger Journals" /\>        \<LISTITEM value\="Sales Ledger Refunds" /\>        \<LISTITEM value\="Stock Master" /\>        \<LISTITEM value\="Suppliers" /\>      \</GLOBALLIST\>      \<GLOBALLIST name\="ExceleratorS1000V1Modules"\>        \<LISTITEM value\="Aged Creditors" /\>        \<LISTITEM value\="Aged Debtors" /\>        \<LISTITEM value\="ALL" /\>        \<LISTITEM value\="Analyser" /\>        \<LISTITEM value\="BOM Assemblies" /\>        \<LISTITEM value\="Budget Master" /\>        \<LISTITEM value\="CashBook Payments" /\>.Then zip up the whole folder and import it:  

![ImportDevOpsProcess.gif](images/PublishingImages_Pages_Devops_Amending_Product_Lists_in_WIs_ImportDevOpsProcess.gif)
