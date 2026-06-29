---
title: PPS - How it works
tags:
- PPS
description: See also Codis Payment Practices Statistics.aspx . PPS has to generate
  the following statistics. It also has to provide a means of understanding what…
created: '2019-09-25'
modified: '2020-02-27'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/PPS%20-%20How%20it%20works.aspx
---

See also [Codis Payment Practices Statistics.aspx](Codis Payment Practices Statistics.md).  

PPS has to generate the following statistics.  It also has to provide a means of understanding what data has been used to derive these figures.

The statistics are (copied from [the guidance](https://assets.publishing.service.gov.uk/government/uploads/system/uploads/attachment_data/file/831507/payment-practices-performance-reporting-requirements.pdf)):

1. the average number of days taken to make payments in the reporting period, measured from the date of receipt of invoice or other notice to the date the cash is received by the supplier
2. the percentage of payments made within the reporting period which were paid in 30 days or fewer, between 31 and 60 days, and in 61 days or longer
3. the percentage of payments due within the reporting period which were not paid within the agreed payment period

It does this over a number of companies in a group, and for two different financial system (Sage 200 and Sage 1000\). Each company is in a different database.

To do this, it first has to generate intermediary table holding data relevant to calculating those statistics for the reporting period.  In doing so it consolidates the data from the multiple databases into a single source, and calculates some data that is not easily available in the original source.  It does this using configurable SQL statements as detailed in [Codis PPS \- Mappings.aspx](Codis PPS - Mappings.md).  

There are two intermediary tables required:  

## PaidInvoices

This table is used to calculate the first two statistics and is part of the calculation of the 3rd statistic.  It contains paid invoices that were due to be paid or were paid in the reporting period. **Note that these are distinct criteria**.     

The generation SQL calculates a payment date for invoices that have been paid (see [Codis PPS \- Mappings.aspx](Codis PPS - Mappings.md).).  This can involve finding invoices that are paid then finding payment for that invoice, and finding the payment that fully paid the invoice.  

Having one SQL statement used to prepare data that is used for what are two similar but then one quite different statistic makes the selection of records difficult to follow.  Although the criteria are distinct, there are similarities between and it is probably optimal for performance to have them combined.  It also means that some rules don't have to be repeated across different sql statements.  

## UnpaidInvoices

This is used as part of the calculation of the 3rd statistic.  "Payments due within a reporting period which were not paid within the agreed terms" includes invoices that were not paid at all, as well as those paid, but not within the agreed terms.

The criteria used to extract this data, and the data stored are different.  It would not make sense to try to combine the data storage, even if they are combined for statistics.

## Statistics

### "The average number of days taken to make payments in the reporting period"

This is clarified in the guidance as being:  
*57\. This is the average (mean) number of days within which payments are made under qualifying contracts during the reporting period. To find the mean, add the number of days it took to make all payments to be reported, and divide it by the number of those payments. All payments that are made under a qualifying contract, during the reporting period, should be included.*   
*58\. Invoices that a business has received but has not yet paid should not be included in the figure. These payments should be reported in the reporting period in which they are paid, should the reporting business still be in scope of the requirement.* 

To calculate this stat we are only concerned with all PaidInvoices records where the Payment date is within the reporting period.  The following is shown:

1. Total number of payments made in the reporting period.
2. Total number of days to pay
3. 2 / 3 (x100\)

### 

### "The percentage of payments made within the reporting period which were paid in 30 days or fewer, between 31 and 60 days, and in 61 days or longer"

This is clarified in the guidance as being:

*To calculate this stat we are only concerned with all PaidInvoices records where the Payment date is within the reporting period.  We need to show:*  
*A business needs to report on what proportion of the payments they made within the reporting period, under qualifying contracts, were paid:*   
*• between day 1 and day 30 (including day 30\)*   
*• between day 31 and day 60 (including days 31 and 60\)*   
*• on or after day 61*   
*60\. All payments that are made under qualifying contracts during the reporting period must be included.*   
*61\. Any invoices that are received but not paid in the reporting period should be recorded in the reporting period in which they are paid. For example, if an invoice was received in the middle of the reporting period and was not paid before the end of the reporting period, it would not be included in the figures for that report. It would only be included if it had been paid.*   
*62\. The proportion paid in each timeframe should be worked out by calculating the number of payments made within each specified timeframe as a proportion of the total number of payments made in that reporting period. The percentage will only reflect the numbers of payments made, not the value of those payments. The three figures should add up to 100% when entered onto the form. You may need to round each figure up or down.* 

This is concerned with the same PaidInvoices records where the Payment date is within the reporting period as the first stat.  

The first two statistic are displayed by the PPS program as follows:

| **Company** | **Company Name** | **Total Invoices Paid** | **Total Days to Pay** | **Average Days to pay** | **Within 30 days (%)** | **31\-60 days (%)** | **\> 60 days (%)** |
| --- | --- | --- | --- | --- | --- | --- | --- |
| COMP1 | Comp 1 Name | 45 | 100 | 4\.5 | 30 | 10 | 5 |
| COMP2 | Comp 2 Name | 50 | 130 | 3\.8 |  |  |  |
| Total |  | 95 | 230 | 4\.13 |  |  |  |

The Total Invoice Paid is the total number of invoices where the Payment date is within the reporting period .

The total days to pay is the total of the DaysToPay column where the Payment date is within the reporting period .  Other columns are calculated.

## To aid reconciliation of the first two set of statistics and csv report will be provided named "PaidInvoices".    This will be a list of PaidInvoices records where the Payment date is within the reporting period.

"The percentage of payments due within the reporting period which were not paid within the agreed payment period"

This is clarified in the guidance as being:

*63\. This is the percentage of the payments contractually required to be made within the reporting period, which were not paid within the agreed payment period. As payments may have been made outside the reporting period, this is a separate set of data from that required to calculate the other statistics.*

*65\. This part of the reporting covers every payment due in the reporting period in question which is not paid in the agreed payment period. This includes invoices or payments which are under dispute, if they have not been paid in the agreed payment period.* 

This statistic has to include both invoices that were paid, but not within the agreed term but also invoices that were not paid at all.  It has to consider:

1. PaidInvoices where the **due date** is within the reporting period whose payment date is after its due date.
2. UnpaidInvoices where the due date is within the reporting period.
3. All invoices, paid or not paid that were due to be paid within the current period.

The percentage required is the sum of the first two statistics divided by the 3rd (x100\)

These statistics are displayed as:

| **Company** | **Company Name** | **Total Invoices Due** | **Total Not Paid** | **Paid but Outside Agreed Terms** | **Period Outside Agreed Terms (%)** |
| --- | --- | --- | --- | --- | --- |
| COMP1 | Comp 1 name | 40 | 5 | 10 | 37\.5 (\=(15/40\)\*100\) |
| COMP2 | Comp 2 name | 50 | 3 | 22 | 50 (\=(25/50\*100\) |
| Total |  | 90 | 8 | 22 | 30 (\=(30/90\)\*100\) |

The Total Invoices Due is the total PaidInvoices where the due date is within the reporting period \+ total UnPaidInvoices where where the due date is within the reporting period.

The Total Not Paid is the total UnPaidInvoices where where the due date is within the reporting period (as used as part of the Total Invoices Due)

The Paid But Outside Agreed Terms will be  total PaidInvoices where the due date is within the reporting period and where the PaymentDate \> DueDate.

They will be supported by two reports:

1. A report DueInvoicesNotPaid \- all invoices due in the reporting period that were not paid.  This will be the UnPaidInvoices where the due date is within the reporting period.
2. A report DueInvoicesPaid \- all invoices due in the reporting period that were paid.  This will be PaidInvoices where the due date is within the reporting period.  Those paid but not within the contracted period can be identified within this sheet by comparing the paymentdate with the due date.

## See Also

[Codis Payment Practices Statistics.aspx](Codis Payment Practices Statistics.md)

[Codis PPS \- Mappings.aspx](Codis PPS - Mappings.md)

[Implementation of Codis IP V3\.aspx](Implementation of Codis IP V3.md)
