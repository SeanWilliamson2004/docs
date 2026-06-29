---
title: Codis PPS - Mappings
tags:
- PPS
description: Overview Codis PPS converts data from multiple Sage (1000 or 200) companies'
  purchasing transactions to centralised repository. In the process, data…
created: '2018-09-19'
modified: '2020-02-27'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Codis%20PPS%20-%20Mappings.aspx
---

## Overview

[Codis PPS](Codis Payment Practices Statistics.md) converts data from multiple Sage (1000 or 200\) companies' purchasing transactions to centralised repository.  In the process, data is converted to a form meaningful for the calculating of the PPS statistics.

To do this in a flexible way, PPS uses configurable data sources and column mappings.  This configuration is stored in Codis IP policies (see Installation Guidelines) in an XML format.  The data in the XML is used to build a [Transact SQL Select query](https://docs.microsoft.com/en-us/sql/t-sql/queries/select-clause-transact-sql?view=sql-server-2017).  The XML configuration is in 3 sections:columns (source and destination), a source table(s) and a where condition.

There are two tables (Paid and UnpaidInvoices) that are populated, and each has its own mappings.  

Column mappings map from a source column to predefined destination columns.  Source columns are used to build the column part of an SQL statement and, as such, can be expressions.  Most columns are common to both tables and mappings to these should be identical, but they have to be replicated in both mappings.  

Tables are populated from a TableName.  This is "from" clause of an SQL select statement and can join multiple tables together.

Which records are selected depends on the WhereClause.  This is "where" clause of the SQL select statement.

***The SQL required will vary both by product and by customer.   Different source tables, relationships and selection will be required for different products.  In addition to this, individual customers have their own business rules to apply.  Typically, this will involve selection of suppliers based on per site rules.***  

## Unpaid Invoices

### Destination Columns

The mappings map to target data.  The data required in the target data is shown below.  Some data is crucial for the calculation of PPS statistics, other data is to make checking that data easier.

| **Column Name** | **Description** | **Notes** |
| --- | --- | --- |
| Company | The company ID | System generated |
| SupplierAccountNumber | Supplier account number |  |
| ID | A unique ID for the transaction. | The combination of company\+supplier\+ID must be unique. |
| TransactionReference | A transaction reference. |  |
| InvoiceDate | The date on the invoice |  |
| InvoiceReceivedDate | The date the invoices was received. | Used in PPS statistics. |
| DueDate | The due date of the invoice. |  |
| GrossInvoiceValueLocal | Value of the invoice in base currency |  |
| ItemType | The type of item. | Invoice or payment. |
| Source | The source of the transaction. |  |

### 

### Table Name section

This has to include the table where the transactions are held, joined to any other tables needed to give the columns in the column mappings needed to populate the destination columns.  

### Where and Join Clause

This should be used to limit selected transactions to those that fit the criteria for unpaid invoices and also apply and bespoke per customer limitations.  

The mapping text can contain placeholder tokens that will be substituted:

{0} \- will be substituted with the from date of the entered date range for the period data being reported.

{1} \- will be substituted with the to date of the entered date range for the period data being reported.  

### Sage 1000 Example Paid Invoices

[PPS \- How it works.aspx](PPS - How it works.md) describes the "Paid Invoices" tables as holding " paid invoices that were due to be paid or were paid in the reporting period. **Note that these are distinct criteria**."    

Table Name section should be:

```
scheme.plitemm i inner join scheme.plsuppm s on i.supplier=s.supplier 

inner join (select s.customer,s.transaction_item, Max(s.allocated_date) as allocated_date from scheme.plxrefm s 

group by s.customer, s.transaction_item) as x on i.item=x.transaction_item and i.supplier = x.customer


```

In this example plitemm is the main table holding purchase invoice items. The PaidInvoices table definition says that this table should just contain paid invoices so to get paid invoices we have an inner join to the payment transaction cross references.  There may be multiple payments against a single invoice, and we need to determine the date the final payment is made so we select the latest allocation date (payment date is approximated to this).  An inner join is made to only get invoices that have been paid.    

As there is also a customer site specific selection based on supplier criteria (see below), we join to the supplier table to get supplier information.  

The where section should be:  

```
where ((x.allocated_date between  ''{0}'' and ''{1}'' and i.open_indicator=''C'') 

or i.due_date between  ''{0}'' and ''{1}'') and i.kind=''INV'' 


```

In this example for Sage 1000 the selection criteria is on   

- allocated\_date (the payment date) being in the reporting period, and a check that the item is closed to eliminate partial payments.
- due\_date (when payment is due) being in the reporting period.  This data will be filtered again when reporting to get payments that were paid past their due date.
- kind \= 'INV' to look at only invoices

There may be further selection criteria that implement customer site specific rules.e.g.
```
and s.analysis_codes3&lt;&gt;''N''


```

In this example, the supplier's analysis code3 is used as a selection criteria.  
## Paid Invoices Mappings and Source

Paid invoices have the same columns as Unpaid, but with the addition of the columns below.

| **Column Name** | **Description** | **Notes** |
| --- | --- | --- |
| PaymentDate | The date the invoice was paid | Used in PPS statistics.  Paidinvoices table only.  The days to pay (used for PPS) is the difference between this and the InvoiceReceivedDate. |
| AllocationDate | The date a final item payment was allocated | Paidinvoices table only. |

### Table Name section

This has to include the table where the transactions are held, joined to any other tables needed to give the columns int he column mappings needed to populate the destination columns.  This may include joining to allocations to find the date of the final allocation.

### Where Clause

This should be used to limit selected transactions to those that fit the criteria for paid invoices.   Typically this will involve a selection based on the payment date (sometimes approximated to the allocation date.)

## XML Format and editing

The XML data is held in a single policy key.  The simpliest way to edit it is to use a query tool to obtain the current value of the key, or of another similar key.  Then to edit it and change to update and save using the query tool.  

The XML data can be on multiple lines and sample XML is stored in this format.  Having it in this format makes it a lot easier to change.

The XML itself is a serialised object.  Its basic structure cannot be altered but line breaks between elements is tolerated.

The SQL to insert a key would be like this (with the mapping added in the ArrayOfMapping section.

The ArrayOfMapping will have to be XML in the format:

NOTE: The mappings are stored in XML and inserted using SQL.  Both place limitations on which characters can be used.  Inverted commas have to be escaped using another inverted comma to prevent SQL thinking they indicate the end of the text.  \< and \> characters have to be escaped to prevent then being assumed to be the start or end of an XML element.  So the SQL not equal to operation "\<\>" has to be \&lt;\&gt;.  

## Changing mappings at a customer's site

Mappings will be altered on a per customer basis.  It is important the current version is considered and probaby used as a base version when making alterations.  To ensure you get the latest version do the following on the customer's site:

Run the following SQL statement on the active CodisMaster database:

```
select [Value] from PolicyValue where [Key]='PPSKeyName'


```

To get the active PPS Key.  Then run using the value returned from the above query as the PPS Key Name

```
select [Value] from PolicyValue where [Key]=<PPS Key Name>


```

This will return the mapping string detailed above.  It can then be amended in e.g. notepad\+\+ or the query editor.  However, the double inverted commas used to prevent single inverted commas being seen as string endings by SQL will have been lost.  These can be restored by a global  replacement.

The run an update statement to store the amended mappings:

!\-\- HTML generated using hilite.me \-\-\>
```
update PolicyValue 

set [Value]='<the mappings>'

where [Key]=<PPS Key Name>


```
