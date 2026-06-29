---
title: Codis PPS - Phase 1b Requirements
tags:
- PPS
description: As a result of testing of Phase 1 at WBA, an issue was identified with
  Phase 1 of PPS. Phase 1A rectifies this issue. The DRPPP (section 41) refer to…
created: '2019-01-15'
modified: '2019-01-15'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Codis%20PPS%20-%20Phase%201A%20Requirements.aspx
---

As a result of testing of Phase 1 at WBA, an issue was identified with Phase 1 of PPS.  Phase 1A rectifies this issue.

The [DRPPP](https://assets.publishing.service.gov.uk/government/uploads/system/uploads/attachment_data/file/649941/payment-practices-performance-reporting-requirements-oct-2017.pdf) (section 41\) refer to 3 statistics.  The issue is with the 3rd statistic that has to be reported on. The [DRPPP](https://assets.publishing.service.gov.uk/government/uploads/system/uploads/attachment_data/file/649941/payment-practices-performance-reporting-requirements-oct-2017.pdf) defines this 3rd statistic:  
*"iii. the percentage of payments due within the reporting period which were not paid within the agreed payment period"*  

In [Phase 1](PPPS Phase 1 Requirements.md), this was taken to be just unpaid invoices when in fact invoices that were paid, but not within the agreed terms should also be included.  

There are a couple of keys points

- The first two statistics concern payments and when those payments are made.  But as only the final payment for an invoice needs to be considered (see Phase 1 notes) we look at invoices and find their payments.
- When selecting payments for the first two statistics, we consider whether the payment was made in the reporting period.  When selecting paid invoices for the 3rd statistic, we consider whether the invoice was due within the reporting period.  These may not be the same invoices.

To facilitate this change, the role of the tables will change.

- "PaidInvoices" This will hold fully settled invoices whose **due date or payment date** lies in the reporting period.
- "UnpaidInvoices" Open invoices whose due date lies in the reporting period. (this is not changed).

Neither of this will now map directly onto the statistics.  However, the program design (bulk copies and soft coded SQL) makes it practical to have these tables in these roles.  

1. The payment statistics will be based on the "PaidInvoices", but only selecting payments whose payment date was made in the reporting period.
2. The 3rd statistic will consider all the UnpaidInvoices \+ paid invoices whose payment date is after the due date, and whose due date is within the reporting period.

Because of the tables no longer direct map, reconciliation will become more difficult unless the two spreadsheets list the transactions included in deriving the statistics.  i.e. the "Payments" spreadsheet should use the selection criteria detail in 1\) and the "Invoices" spreadsheet should use the criteria detailed in 2\.
