---
title: 'First Choice: Fresho Integration'
tags: []
description: Project Objective & Background The purpose of this project is to migrate
  from a 3rd-party integration to Codis Orchestrator and Excelerator . The 3rd…
created: '2026-06-04'
modified: '2026-06-04'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Fresho-Sage-Integration.aspx
---

Project Objective \& Background

The purpose of this project is to migrate from a 3rd\-party integration to **Codis Orchestrator** and **Excelerator**.  

### The 3rd Party System

A 3rd\-party solution fetched order XML files exported by Fresho via SFTP. This solution generated Sales Orders (SOP) within Sage 200, which were then processed through standard Sales Order Processing to output customer invoices.

### The Core Issue

- **Invoice Number Disconnect:** Sage 200 automatically generated invoices utilising its own internal numbering sequence.
- **First Choice Impact:** FC's customers pay against original **Fresho order numbers**, making internal Sage order/invoice numbers completely irrelevant to them. Because the primary field did not match what the customers were seeing, it created reconciliation friction for the accounts team.

## The Solution Architecture \- Orchestrator and Excelerator

To address the numbering misalignment, the new Orchestrator integration completely **bypasses the Sales Order Processing (SOP) module**. Transactions are handled directly via a streamlined split workflow:

- **Financial Ledger:** Handled directly via the **Sales Ledger (SL) Invoice module**, allowing Fresho order numbers to be recorded as the primary reference field.
- **Inventory Control:** Handled simultaneously via the **Stock Adjustment module** to account for physical stock movements.
### Excelerator SL Invoice Module Enhancements

To support direct stock management out of a financial ledger layout, the SL Invoice module has been upgraded with custom data ranges. It now natively maps:

- Product Codes
- Quantities
- Warehouse Location
- Bin Location

> **Critical Requirement:** These extended inventory ranges within the SL Invoice module will *only* work when the **Stock Adjustment License** is activated.

## Key Configurations \& Considerations

Before deployment and during support queries, the following backend requirements must be explicitly met:

### Nominal Ledger Integration

Under the previous SOP architecture, stock movement values were automatically routed to the nominal ledger during standard order dispatch and invoicing routines.

- **Required Change:** Because the new process bypasses SOP in favor of direct Stock Adjustments, we **must** enable the **"Integrate Stock Management with the nominal ledger"** option within Sage 200 Stock Control Settings.
- **Impact:** If this setting is disabled, stock\-related nominal postings will fail to record during the adjustment process.

### XML Data Mapping \& XSLT

Orchestrator and Excelerator capabilities have been optimized to interact directly with raw XML structures.

- To map incoming Fresho XML order structures into the standardised tabular rows required by Excelerator, a **Transformation File (XSLT)** must be applied within the Orchestrator/Excelerator import routine.
## Automated Integration Process \& Workflow

```
The integration operates as a headless automated service managed by Orchestrator via an SFTP pipeline.


```
[ Fresho SFTP Server ] ──> [ Orchestrator Pulls XML ] ──> [ XSLT Map to Template designed using Excelerator ] ──> [ Validate & Save to Sage ]  

### Step-by-Step Execution

1. SFTP Retrieval: Orchestrator connects to the Fresho SFTP server and checks the directory for newly exported XML files.
2. Transformation: Orchestrator passes the raw XML data through the designated .xslt file to translate it into an Excelerator-ready data schema.
3. Validation & Post: Orchestrator validates the data. If cleared, it posts the financial data directly to the Sales Ledger and updates stock levels via a Stock Adjustment.
4. File Routing & Fault Tolerance:

	- Successful Runs: Successfully processed XML files are immediately moved out of the root folder and archived into the processed directory on the SFTP server.
	- Failed Runs: If a file fails validation or database entry, it remains in the root SFTP folder. It will be systematically picked up again for automated retries on subsequent scheduled execution loops.

### Automated System Alerts

- Failure Notifications: Schedules are configured to monitor transaction flags. If an integration run encounters an error or a file repeatedly fails validation, Orchestrator will automatically generate and send an email alert outlining the details of the failure.

```

```
