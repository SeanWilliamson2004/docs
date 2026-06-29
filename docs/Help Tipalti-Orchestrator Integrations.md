---
title: Help Tipalti-Orchestrator Integrations
tags:
- Orchestrator
description: Tipalti-Sage Integration Tipalti is a cloud-based financial technology
  platform designed to simplify and automate global accounts payable (AP),…
created: '2025-02-26'
modified: '2025-02-27'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Help%20Tipalti-Orchestrator%20Integrations.aspx
---

# Tipalti\-Sage Integration

Tipalti is a cloud\-based financial technology platform designed to simplify and automate global accounts payable (AP), procurement, expense management, and payment processes.  

## 1\. Overview of Tipalti Sandbox

The Tipalti Sandbox is a testing environment that simulates real\-world operations without connecting to the public banking system. Key features include:

- Testing Capabilities: Create payees, bills, and payments using fake money.
- Permissions: Full permissions are granted in Sandbox, unlike the Production environment.
- Limitations: Payments remain in a "Submitted" status and must be manually marked as paid or rejected.

## 2\. Key Processes in Tipalti Sandbox

## Adding a Payee

1. Navigate to the "Payees" section and click "Add Payee."
2. Complete the form; Tipalti can generate an ID automatically.
3. Click "Create." Note that there may be no immediate feedback.
4. Wait 60 seconds, then click "Cancel."
5. Search for the payee using their name in the search bar.

## Making a Payee Payable

- A payee must be marked as payable before processing payments.
- Refer to this [video guide](https://share.vidyard.com/watch/nhUqaH1FELgwNHEhNpzsEp?).

## Creating and Approving a Bill

1. Follow this [video guide](https://share.vidyard.com/watch/FdN5FL4t5CfEpLim8Qee1h?) to create a bill record with an approver.
2. Approve the bill using this [video guide](https://share.vidyard.com/watch/f2mAo8W1La64J6rgc5wfB1?).

## Processing Payments

1. Create a payment batch (even for a single payment) and approve it using this [video guide](https://share.vidyard.com/watch/mMm5ExyovTQuG8YRVBcHaW?).
2. Payments will enter a "Pending Funds" status before being processed.

## Downloading Files for Sage

- Files show changes from the last download only.
- Create or modify records to generate new files.
- Refer to this [video guide](https://share.vidyard.com/watch/JzZUEqEVWnWh2hJEjz8F2o?).

## 3\. Integration with Sage 200

The integration between Tipalti and Sage 200 supports both purchase orders (POs) and non\-PO workflows.

## Key Features

- Vendor Onboarding: Managed within Tipalti.
- Invoice Capture: Begins in Tipalti, with full payment details visible in the system.
- Matching: Supports 2\-way and 3\-way matching for POs.

## 4\. Integration Using Orchestrator

The integration process involves three modules: suppliers, invoices, and payments. \-\-\- (for Omnes Healtcare)  

## Prerequisites

- Access to Tipalti export functionality.
- Permissions for designated file system folders.
- Range definition files for field mapping.

## Folder Structure

Orchestrator

- Company1/
- Suppliers/
- Invoices/
- Payments/

- Company2/
- Suppliers/
- Invoices/
- Payments/

## Step\-by\-Step Process

1. Export Data from Tipalti
- Log into Tipalti, navigate to the export functionality, and export data for one company at a time as a CSV file.
- ![image001.png](images/PublishingImages_Pages_Help_Tipalti-Orchestrator_Integrations_image001.png)
- ![image003.png](images/PublishingImages_Pages_Help_Tipalti-Orchestrator_Integrations_image003.png)
- To amend the export data templates (making any changes to the export file templates will require changes in Orchestrator range definition files, which cannot be amended directly):
- ![image005.png](images/PublishingImages_Pages_Help_Tipalti-Orchestrator_Integrations_image005.png)

3. Place Files in Correct Folders
- Copy CSV files to the appropriate module folder (e.g., Suppliers, Invoices, Payments).
- ![image007.png](images/PublishingImages_Pages_Help_Tipalti-Orchestrator_Integrations_image007.png)

5. Configure Range Definition Files
- Map fields from Tipalti to Sage using range definition files.
- Example of a range definition file showing field mappings, if any change is required, Codis needs to be contacted for making amendments in the ranges.
- ![image009.png](images/PublishingImages_Pages_Help_Tipalti-Orchestrator_Integrations_image009.png)

7. Set Up Orchestrator
- Configure folder locations:
- Source folder: Location of CSV files.
- Processed folder: Successfully processed files.
- Error folder: Files with processing errors.
- ![image013.png](images/PublishingImages_Pages_Help_Tipalti-Orchestrator_Integrations_image013.png)

9. Handle Errors
- Check error logs for issues such as duplicate invoice numbers or missing fields.
- ![image017.png](images/PublishingImages_Pages_Help_Tipalti-Orchestrator_Integrations_image017.png)
- To specify any error/warning to ignore, error codes are available in the log file. In the above screenshot, error code is InvalidAccountReference

11. Verify Processing
- Ensure successful processing by checking Sage records.

## 5\. Common Issues and Troubleshooting

## Common Errors

- Duplicate invoice numbers.
- Missing required fields or invalid data formats.
- Failed field mappings in range definition files.

## Troubleshooting Steps

1. Review logs in Orchestrator for detailed error messages.
2. Correct errors in CSV files or range definitions before reprocessing.

## 6\. Testing Checklist

Use this checklist to ensure all steps are completed successfully:

- Export data from Tipalti.
- Place files in correct folders.
- Verify range definition files.
- Configure Orchestrator folders.
- Complete test runs without errors.
- Validate successful processing in Sage.
