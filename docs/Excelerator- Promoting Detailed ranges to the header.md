---
title: 'Excelerator: Promoting Detailed ranges to the header'
tags:
- Development
description: Background - The challenges Excelerator Ranges Ranges are grouped together
  according to a logical data model, which is dictated by business rules.…
created: '2017-03-06'
modified: '2017-03-14'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Excelerator%20-%20Designing%20Ranges.aspx
---

# Background \- The challenges

## Excelerator Ranges

Ranges are grouped together according to a logical data model, which is dictated by business rules.  For instance, there can be multple invoices in a batch and the batch might have a batch number and a control total that are grouped together.  There is a rule that you can have multiple invoice per batch but not multiple batches per invoice.  Further rules tie together these groups of data.  The logical data model is independent of the physical data model (the database schema) but often maps closely to it.

Above this logical data model we have external views that allow users and APIs that allow 3rd parties to view and update the data.

Drawing these distinctions is important as entering data in Excel provides both flexibility and limitations to the external view that do not apply to the Business logic or physical layer. 

For instance, Sage 1000 has an NL Journal physical data model that was (wrongly) mapped to the external view as provided by Sage 1000\.  Entry is paged and so is the physical data model.  As we use only our own API for applying business rules for Sage 1000, we produced an API logical data model that applies the business rules for the journal, but hides the physical model.  In Excelerator, we can then work with this logical data model to provide different external views to fit requirements (see header detail ranges below).  

Although this explanation might seem very technical and inappropriate to present to users, experience has told us that users do expect the flexibility in their requirements and the limitations have to be addressed.

## Header or Detail ranges

Originally, Excelerator ranges were designated either header or detail.  They were either intended to be a single cell placed at the top of the spreadsheet (header) or part of a list consisting of multiple ranges with multiple cells below.   The names Header and Detail were probably chosen because of their meaning in relationship database design. 

It was soon realised that there was a user requirement to place some of the header ranges in the list to allow multiple entities to be entered on a single sheet.  These ranges were then called header\-detail.   However, it some cases, it was a requirement to allow one (or more) of those header\-detail ranges to be placed in the header so that a single default value can be entered for the entire sheet.

A good example of this is V1 Purchase Ledger Excelerator.  [http://www.codis.co.uk/sage\-1000\-excelerator\-help\-v1/excelerator\-modules/purchase\-ledger\-invoices/sample\-spreadsheets](http://www.codis.co.uk/sage-1000-excelerator-help-v1/excelerator-modules/purchase-ledger-invoices/sample-spreadsheets).  

As can be seen, supplier and invoice ranges can be in the head of the spreadsheet.  In this example, one invoices is entered with multiple NL distribution lines:

 

| **Batch** | 0001 |  |
| --- | --- | --- |
| **Supplier** | S001 |  |
| **Invoice** | INV1 |  |
| **Effective Date** | 01/01/2017 |  |
| **Nominal Code** | **VAT Code** | **Value** |
| 1\-01\-10\-10\-001 | V | 100 |
| 1\-01\-10\-10\-002 | V | 200 |
| 9\-99\-99\-99\-001 | V | 60 |

Or the invoice placed in the list.  In this example two invoices are entered:



|  | **Batch** | 0001 |  |
| --- | --- | --- | --- |
|  | **Supplier** | S001 |  |
|  | **Effective Date** | 01/01/2017 |  |
| **Invoice** | **Nominal Code** | **VAT Code** | **Value** |
| INV1 | 1\-01\-10\-10\-001 | V | 100 |
| INV1 | 1\-01\-10\-10\-002 | V | 200 |
| INV2 | 1\-01\-10\-10\-002 | V | 100 |

Or multiple suppliers and invoices entered in the list.  In this example, two invoices are entered for different suppliers:



| **Batch** | 0001 |  |  |  |  |
| --- | --- | --- | --- | --- | --- |
| **Supplier** | **Invoice** | **Effective Date** | **Nominal Code** | **VAT Code** | **Value** |
| S001 | INV1 | 01/01/2017 | 1\-01\-10\-10\-001 | V | 100 |
| S001 | INV1 | 01/01/2017 | 1\-01\-10\-10\-002 | V | 200 |
| S001 | INV1 | 01/01/2017 | 9\-99\-99\-99\-001 | V | 60 |
| S002 | INV1 | 01/01/2017 | 1\-01\-10\-10\-001 | Z | 100 |
| S002 | INV1 | 01/01/2017 | 9\-99\-99\-99\-001 | Z | 20 |

## Promotion to Header

We then also had further requirements to allow some ranges from the invoice header or detail in the head of the sheet in a single cell, whilst other ranges such as invoices were placed in the list detail section.  The value entered in the head would be used for all header\-details or details in the list.  The table below shows an example of this where the project code, which is on the invoice detail nominal and project distributions, is promoted so that a single project code "ADVERTISING" used for all nominal and project distributions.

 

| **Batch** | 0001 |  |  |  |  |
| --- | --- | --- | --- | --- | --- |
| **Project Code** | ADVERTISING |  |  |  |  |
| **Supplier** | **Invoice** | **Effective Date** | **Expense Code** | **VAT Code** | **Value** |
| S001 | INV1 | 01/01/2017 | EXP1 | V | 100 |
| S001 | INV1 |  | EXP2 | V | 200 |
| S001 | INV1 |  | VAT | V | 60 |

So, in these circumstances, what is a header, a header\-detail and detail?  The orginal idea of these terms no longer seem to be appropriate.

## Control Ranges

When 'header' ranges like this are placed in the list, there has to be means of determining when a new invoice has been entered.  This is achieved by looking for changes in designated "Control" ranges.  The multiple supplier and invoice example above shows an example of this.  A new invoice starts on Row 4 of the data because the control range "invoice" changes value.  

Really, all ranges should be control ranges and there are rules about what data has to change when any data changes.  

## Blank Values carried forward (speed entry)

The multiple supplier and invoice example shown above works well where data is imported from a 3rd party source, but if using Excelerator to speed enter data then there is a lot of unnecessary rekeying of data.  In these circumstance, entering data as shown in the table below may be easier and this has been found to be a user requirement.  

 

| **Batch** | 0001 |  |  |  |  |
| --- | --- | --- | --- | --- | --- |
| **Supplier** | **Invoice** | **Effective Date** | **Nominal Code** | **VAT Code** | **Value** |
| S001 | INV1 | 01/01/2017 | 1\-01\-10\-10\-001 | V | 100 |
|  |  |  | 1\-01\-10\-10\-002 | V | 200 |
|  |  |  | 9\-99\-99\-99\-001 | V | 60 |
| S001 | INV2 | 01/01/2017 | 1\-01\-10\-10\-001 | Z | 100 |
|  |  |  | 9\-99\-99\-99\-001 | Z | 20 |

## Key Ranges

Another consideration is when to stop reading data from the spreadsheet.   Reading all rows until the end of the range was not considered optimal as was reading from all ranges until no values were found.  Instead, some ranges were designated "Key" ranges.  Data is read from all ranges as long as data is found in those ranges.  If all key range cells in a row are found to be blank then processing stops.  In the examples given above "Value" is a key range.  

## Multiple Children (Array Ranges)

The logical data model can have parent\-child relationships.  For instances batch may be the parent of invoices which are parents of invoice distribution lines.  As seen above in the various examples, Excel provides a few ways of entering parent\-child data by having a list of the children below or alongside parent data.   

However, there is a challenge if a logical data entity has multiple children.  If all the parent data is in the header, then it could possible to have two lists.  



| **Account** | S001 |  |  |  |  |  |
| --- | --- | --- | --- | --- | --- | --- |
| **Reference** | XXXX |  |  |  |  |  |
| **Allocations** |  |  |  | **Bank Charges** |  |  |
| **Type** | **Reference** | **Value** |  | **Nominal Account** | **Description** | **Charge** |

But if the parent data is in a list, then this will not work.

One other possible solution is to have a single list common for all children data but this only work where the children entities have similar properties. (For example \- product, service and at a stretch, comment lines on an order.)  

Another possible solution is to limit the size of the extra children data's list and then to have that data entered in different columns (rather than rows) across the sheet.



| **Account** | S001 |  |  |  |  |  |  |  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| **Reference** | XXXX |  |  |  |  |  |  |  |
| **Allocations** |  |  |  |  |  |  |  |  |
| **Type** | **Reference** | **Value** | ****Bank Charges 1** \-Nominal** | **Bank Charges 1\- Desc** | **Bank Charges 1\-Charge** | **Bank Charges 2\- Nominal** | **Bank Charges 2\- Desc** | **Bank Charges 2 \- Charge** |

## Master Data with Child Data

Master logical data types (e.g. supplier's, customer's, stock) can have single or multiple children.  For instance, customers and suppliers can have lists of contacts associated with them.  In these cases even having any lists may not be appropriate as usually the best way to enter a master data entity is one entity per row.

# V1 Excelerator

V1 Excelerator evolved from a basic idea.   In V1, the Excelerator framework simply handled reading data and putting data to a single cell in a range.  All the challenges  (except Multiple Children) above had to be supported to some extent in some modules, but in each case this had to be coded for each module.  

This was typically done over time as the requirements came to light, and not consistently for each module.  This continued for V1 Enterprise Excelerator.

# V3 Excelerator

For V3, a new development environment (.net) and Excelerator framework was introduced.  When designing the new Excelerator framework, an attempt was made to extract some rules out of the ad\-hoc practices we had been applying to invididual modules.  The V3 Excelerator framework allows entire sheets of data to be extracted or uploaded to in single calls and uses metadata to apply these rules.

As mentioned above, the concept of ranges being either header, headerdetail or detail is outdated.   In V3 allows you to mark ranges as header, headerdetail or detail.  This information is displayed on the tooltip help on the designer when the mouse hovers over the range.   However, the only rule that is applied is where it checks that a "Header" type range does not have more than one cell, which is probably just an unnecessary restricition to place on a range.   This marker should probably considered either just a hint to users, or deprecated.

Control, Key ranges and Blank Values carried forward are implemented as part of the framework.  

Promotion to header is supported via the CanBeHeader property which currently has to be specified on ranges that can be promoted.  

Mutiple children and children on master data are supported by designating them as "Array" ranges with allow a fixed number to be entered in columns across the sheet.
