---
title: PPPS Phase 1 Requirements
tags:
- PPS
description: Overview The primary requirement is to produce a solution that will allow
  Kew Green to conform with the reporting duties placed on it by section 3 of…
created: '2018-09-01'
modified: '2018-11-23'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/PPS%20Phase1%20Requirements.aspx
---

## Overview

1. The primary requirement is to produce a solution that will allow Kew Green to conform with the reporting duties placed on it by section 3 of the Small Business, Enterprise and Employment Act with regards to reporting on payment practices as detailed in "Duty to Report on Payment Practices and Performance" guidance (DRPPP).
2. A secondary requirement is to extend functionality such that to allow the software to be sold to other end\-users.  Only certain business qualify as having to report this information.

## Reporting Period

1. The reporting period is approximately every 6 months.  Details are defined in the DRPPP section 82 onwards.
2. A reporting period will have to be entered before any reporting run.
3. Payment and invoice data will be copied from each Sage company at the invoice and payment level of detail to a central reporting database.
4. It is important that each data consolidation run can be identified in the target database, and that trial runs can be distinguish from those that actually have figures submitted for.   This is:
- For auditing.  It will be important to be able to support and analyse reported statistics.
- To prevent reporting twice on the same data.

6. Each run will have a unique identifier set up for it
- One solution could be to have target tables named after the unique identifier.
- Another would be to have each row stamped with the unique identifier for the run.

## Data To Report

1. The DRPPP describes 3 sections.
- Narrative descriptions
- Statistics
- Statements

3. The narrative and statement sections will not be address by this solution.
4. Statistics will be addressed by this solution and are discussed below.
5. The solution will consolidate the details requirement to calculate these statistics from multiple Sage companies into a single database.  Having the detail will allow drill down into the data that makes up the statistics.
6. Whether the solution will calculate the statistics is still to be determined.
7. Partial payments are not addressed by DRPPP.  It will be assumed that partial payments other than the final payment against an invoice will not count in any way towards the statistics.
8. The date of receipt of the invoice is not usually captured in Sage.  This will have to be approximated to the invoice date.
9. The date of payment is meant to be when the supplier receives payment, unless delayed by circumstances outside of the business reporting, in which case it ends when the supplier would have received payment if the delay had not occurred.  (DRPPP 58\).
10. It may be necessary to approximate the payment date based on a date captured in Sage (the allocation date) and add expected processing time.  The processing time might vary by payment method

## Statistics

The DPRRR describe the following sub\-sections: 

1. The average number of days taken to make payments in the reporting period, from the date of receipt of invoice or other not
- Invoices that a business has received but has not yet paid should not be included in this figure (63\).
- Payments will be included in a reporting period if their payment date is made in the reporting period

3. The percentage of payments made within the reporting period which were paid in 30 data or fewer between 31 and 60 days, and in 61 days or longer.
4. The percentage of payments due within the reporting period which were not paid within the agreed payment period.
- The DRPPP states: "This is the percentage of the payments contractually required to be made within the reporting period, which were not paid within the agreed payment period. The agreed payment period is the period within which the customer is required to pay the supplier. It is usually set out in the contract, but there may be instances where it depends on details in the invoice or other documents. It may be explicitly negotiated, or may form part of standard contract term"
- It will be assumed that the agreed payment period is defined by the payment terms held against the supplier in Sage.
- Invoices will be included if their due date falls in the reporting period.  Reporting periods that are used to actually report.

## Selection of supplier

1. The DRPPP defines certain contracts between the report companies and their suppliers that have to be reported on and even describes how to treat supplier invoices that cover multiple contracts (some eligible, some not).
2. A complete solution would have to tie invoices items to contracts and allow contracts to be identified as eligible.  However, as this is not possible without considerable work, a compromise solution would to be assume that any supplier either qualifies for all contract or doesn't qualify and so have suppliers identified as qualifying or otherwise.
3. A solution just for Kew Green selection would be based on a single analysis code (providing one is available in the Kew Green databases).
4. A more general solution would allow the field used to be specified by company.    Which field used would have to be entered into configuration in CodisIP.
5. In these cases, Excelerator could be used to maintain which suppliers are eligible.
6. An extended solution would allow the suppliers to be identified using markers stored in the CodisIP database.
7. It may be easier to have suppliers marked as opting out, rather than in.

## Company selection

1. The CodisIP database will be used as a definition of the company but it may be necessary to select or exclude certain companies from this list.  How this is to be done is still to be determined but might be based on a pre\-defined role and defined in CodisIP.

## Processing

1. The user will have to enter a reporting period.  These must be two dates, the second after the first.
2. Invoice and payment data will be collected from all selected companies and stored in a central database in two tables.
- Paid (closed) invoices and the associated payment information will be selected if the payment date falls within the reporting period.  The following information will be collected:
- The Sage company
- The supplier being paid
- The invoice number
- The invoice date
- The invoice due date
- The invoice value
- The payment date

4. Unpaid (open) invoices will be selected if their due date falls within the reporting period.  The following information will be stored:
- The Sage company
- The supplier being invoiced
- The invoice number
- The invoice date
- The invoice due date
- The invoice value

## Housekeeping

1. There is likely to be a requirement to run trial reports.  The data from each run will be stored in target tables.  An option to remove data for a given run might be needed.
2. The might be a requirement to track whether any particular run is reported to the web service and to prevent deletion of datasets that have be used as a basis for the report.

## Caveats

1. Approximation that all a suppliers contracts are either eligible or not (see Selection of Supplier).
2. All invoices are to be treated the same way.  (DRPPP mentions different processing for e\-invoices or supply chain finance or construction contracts).
3. Date point for "invoice received".
4. Narrative and Statement sections will not be addressed by this solution..
5. Submissions to the "web service" will not be covered by this solution.
6. Payments without an invoice?  (61\) specifies how they should be treated.
7. It will be assumed that partial payments other than the final payment against an invoice will not count in any way towards the statistics.
8. It will be assumed that the agreed payment period is defined by the payment terms held against the supplier in Sage
