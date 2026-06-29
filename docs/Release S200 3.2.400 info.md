---
title: Release S200 3.2.400 info
tags: []
description: 'Notes for release Sage 200 Standard Excelerator Suite V3.1 Release Release
  Number : 3.2.400-1 Release completed : Wed Jan 19 2022 15:13:33 GMT+0000…'
created: '2022-02-17'
modified: '2022-02-21'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Notes%20for%20release%20Sage%20200%20Standard%20Excelerator%20Suite%20V3.1%20Release%203.2.400-1.aspx
---

# Notes for release Sage 200 Standard Excelerator Suite V3\.1 Release

**Release Number** : 3\.2\.400\-1 

 **Release completed** : Wed Jan 19 2022 15:13:33 GMT\+0000 (Greenwich Mean Time)  
**Build Number**: 

 **Compared Release Number** : 3\.2\.86\-1  
**Build Trigger PR Number**: 

### **S200 User Stories**

- **1896** S200 Sale Quotations \-when we select a stock Item we need to default the VAT and Nominal Codes for that item
- **2342** S200 Price Bands Excelerator
- **2364** CodisDevelopment VS2019 Update
- **2386** Show correct release info in About screen
- **2419** Save as File functionality should save a copy of the file
- **2426** S200 Price Bands \- add option to specify number of ranges for side by side price band ranges
- **2428** S200 Price Bands should have browse on the stock name field like other excelerators (SOP and SOP Quotes for example)
- **2440** Excelerator Colours should be same as Sage's colour
- **2448** S200 PL Pay Alloc and SL Receipts Aloc modules only allow for open invoices to be allocated
- **2465** Move remaining Sage 1000 projects in Common to be under the Sage 1000 folder
- **2523** Browse should use Async with busy indicator shown.
- **2543** Excelerator Designer validation window should allow more complex validations
- **2564** Show progress on Excel Stats Bar if NonInteractiveMode\= True
- **2571** Resize detail ranges form should use new standard forms
- **2573** S200 Custom Fields for Sales Order Excelerator
- **2576** Purchase Order \- Header Ranges only
- **2611** Invoice status range to add S200 Invoicing template
- **2621** Sage 200 Customer Delivery Addresses Excelerator
- **2647**Show full message on S200 connection error
- **2659** Map Sage 200 NL Journal with ID to identify whether it is posted/saved before saving
- **2662** Add functionality to Sage 200 NL Journal for imbalance journal
- **2680** Enhancements to new browse
- **2682** Sage 200 Printing SOP \& POP and Quotations
- **2691** Add logic to print selected order if selected cell in range. Show a list of orders that will be printed before they are printed
- **2724** Changes for sales order print
- **2759** Update Installer Ism file for NLJournals Service
- **2760** Sage200 Webservice NLJournals Licence code update
- **2766** S200 Sales Invoices performance for large number of invoices (also PL Invoices)
- **2783** Invoicing Printing
- **2789** Purchase Returns Printing
- **2803** Browse on delivery address on S200 sales orders
- **2807** SO and PO should work for header only
- **2809** S200 PL/SL Allocation context sensitive Allocate rt. click
- **2817** S200 Quotations should have a Calculate Values option
- **2824** Add Codis.Sage200Enterprise.SOPInvoice project to Codis.Sage200 and Codis.Sage200\.WithInstallers solution to generate nuget package for it
- **2841** Add functionality to map Purchase Order with External ID

### **S200 Bugs**

- **1802** S200 Suppliers \- Resize detail ranges does not accept value of 100,000
- **2365** Further issues Invoicing modules
- **2388** Sage 200 Quotation doesn't get owner value if new user added to CRM
- **2392** Error occurred while deleting Sales Order
- **2393** Error occurred while saving and validating Sales Returns.
- **2394** Error occurred while deleting Purchase Order
- **2396** Browse not working for PriceList Template
- **2401** Sage 200 NL Journals Narrative range does not clear
- **2402** Mandatory Analysis code field does not validate in Customer Module
- **2407** S200 Sales Order Quotations message: Invalid Stock/Addition charge code
- **2410** S1000 Price lists don't display errors
- **2414** S200 Sales Orders downloads clears sheet regardless of what you select
- **2415** S200 Sales Orders download displays EnumDocumentStatusLive
- **2417** PL Invoice does not validate
- **2421** Build failed for S200 Price Bands
- **2422** S200 SOP Excelerator\-Message when saving order with a traceable stock not in stock
- **2427** S200 Price Bands Excelerator \- Populate button should only bring down details for stock items entered on sheet
- **2429** Fix Sage 200 2011 Build issue
- **2430** S200 Sales order download order status
- **2434** S200 Sales Quotations and Sales Orders ignore 0 quantity lines giving an error
- **2436** S200 Sales Quotations \- Can't amend the Promised Date
- **2438** S200 Stock Excelerator not able to amend the Stock Unit
- **2446** S200 Supplier \- Cannot update Email/Phone number while keeping Name ranges blank
- **2452** Warnings during build of Codis.Sage200\.IP
- **2464** S200 Sales Invoice Transaction Enquiry bug
- **2466** S200 SOP Entry \- Item/Line/Detailed Analysis code does not allow to enter free text
- **2470** S200 Customer \- Memo Range throws an error for Invalid Characters
- **2471** S200 SOP Entry \- Nominal Codes are not copied while saving Order
- **2528** S200\- PL Invoice does not ignore duplicate Invoices
- **2531** S200 Ex 2011 \- Purchase Order Entry \- Browse cell throws an error
- **2533** Excelerator ribbon buttons do not show tooltips
- **2536** S200 CB Payment Single Sheet \- Does not update Transaction Analysis Code Range
- **2538** Sheet rename and copy sheet don't work
- **2553** S200 Nl Journals \- date changes on first line of new journal in multiple journals template
- **2563** S200 \- Stock Template does not update Country of Origin
- **2566** Sage 200 login crashes Excel
- **2568** S200 NL Journal Ex \- Locked Journal Type range throws an Error but Saves
- **2569** S200 Price Bands \- Support for limited price bands
- **2575** Whitelist check fails in MJ French customization
- **2577** S200 Plugin issue
- **2578** S200 POP\- Part ref detail range is not available
- **2579** S200 PO\-Excelerator keeping order on hold for supplier whose credit limit has exceeded
- **2581** S200 Templates bug
- **2582** Incorrect field heading on Purchase order browse window
- **2583** Sage200 PO browse issue
- **2584** Sage200 Sales Quotation module is not working
- **2585** New browse limit width and height and use ConfigureAwait, pass back tasks directly
- **2586** S200 NL Journal \- Fast entry defaults to the first record
- **2587** S200 Stock \- 'OK' button does not work for Warehouse and Stock Unit Browse window
- **2588** S200 PO error on Calculate values
- **2595** S200 Stock \- Price Source(supplier) range does not fetch the price name from browse but it does populate while downloading a stock
- **2599** Module name not defined in S200 Stock AddinDef file
- **2600** Sage 200 2011 build fails
- **2602** S200 PL Pay Allocation Template \- The given key was not present in the directory
- **2603** New browse double click error when scrolling
- **2605** Download event not raised in Stock Server DAO and SetStringToDecimal function not written in SpreadSheetIOAPI
- **2607** S200POPEntryTemplate \- 'Request delivery date' range not updating the date in Sage after 'Save to sage'
- **2609** S200 Price Bands \- Populate gives error
- **2610** Codis.Framework is not generating source link info in output nuget package
- **2619** New price band Stock browse falls over if filtered.
- **2620** S1000 Enterprise Build failing
- **2622** S200 NL Journal \- Browse giving error
- **2631** S200 NL Journal \- Fast Entry/Browse does not pull Nominal Code Names
- **2632** S200 NL Journal \- Unposted Journal warning message
- **2633** S200 NL Journal Single sheet\- Different Tax Codes Defaults to Exempt
- **2634** S200 NL Journal \- Error (Operator 'Not' is not defined for type 'DBNull'
- **2636** S200 SOP\- while adding stocks, it does not populate selling price, tax code, unit price on the template
- **2637** New Browse Fixes
- **2638** S1000 Connection Errors
- **2639** S200 Webservice build fails
- **2642** S1000 NL Journal Excelerator tests to build and pass
- **2644** S1000 PL Invoice tests
- **2649** Package creation in S200 build
- **2653** S200 Price Bands \- Error "the standard price band cannot be edited"
- **2654** Build Sage 200 Excelerator fails
- **2657** Sales order picks default nominal code from Customer. Should picks based on the settings
- **2658** Errors on Purchase returns S200 Ex. 2019 v3\.2\.236
- **2660** Error on all S200 Ex. templates when saving to file \- Unable to cast object of type 'Codis.Wpf.ViewModels.CodisButtonFormViewModel'
- **2663** S200 POP\- Multiple Dates on PO lines do not upload
- **2665** Supplier stock code missing from supplier drop down at S200 Stock template
- **2668** Stock browse throw an exception in Sage 200 2019
- **2669** Sage 200 Stock service gives an error on stock browse
- **2672** Sage 200 packages not generating correctly\-
- **2673** Critical Error in version 3\.2\.247\.0
- **2676** S200 Invoicing \- 'Access Denied' error when trying to validate/Save/ download data
- **2677** S200 Ex. Invoicing template Stock code browse error and Cost centre browse
- **2678** S200 NL Journal \- Journal imbalance and NA Tax type error
- **2679** S200 Supplier price list \- Unable to update price source \& last order price and Invalid lead time unit error
- **2683** Errors on Purchase returns S200 Ex. 2019 v3\.2\.251
- **2685** Fast entry does not work on new browse
- **2686** S200 Invoicing date format and Browse error
- **2688** S200 Stock template \- Data not populating
- **2693** S200 Excelerator error on module selection
- **2698** S200 Invoicing template error during download and validation
- **2699** S200 PL payment allocation errors
- **2700** S200 SL Receipt allocation errors
- **2702** S200 Stock transfers \- buttons missing
- **2704** S200 Customer and Supplier \- Error on validate/Save to Sage
- **2707** S200 Amended work books and Header only templates
- **2713** Extra buttons visible in Options screen.
- **2720** S200 Ex v3\.2\.287 Module selection error
- **2721** Sage 200 Invoicing download issue
- **2723** S200 SL Receipt allocation browse error
- **2726** S200 Amended workbooks with Header only
- **2727** S200 Customer Delivery Address module browse error
- **2728** S200 Customer and Supplier Account browse error
- **2729** S200 CB Payments \- Load Range Definition pops\-up with error
- **2730** S200 POP \& SOP download and data update errors
- **2731** Sage 1000 PL Invoice Excelerator V3 index error on saving batch
- **2732** S200 PL \& SL Invoices data populate error
- **2733** Sage 200 PL Payment errors on search and allocation
- **2735** Sage 200 Stock transfers validate/Save to Sage errors
- **2738** Sage 1000 PL Invoice Excelerator V3 DA0904 saved data is not consistent with Sage
- **2741** Sage 200 Amended workbooks
- **2742** S200 Excelerator \- TC license does not license User Profile/ instance from PR 1266
- **2758** S200 2011 Build fixes
- **2761** Sage 200 PL \& SL Invoice download confirmation message pops\-up twice
- **2765** S200 PL Payments \& SL Receipts browse issues
- **2770** SOP 200 Order Entry \- stock browse does not populate fields other than the code
- **2771** S200 Sales Order \- calculate values throws unhelpful exception in any validation failure
- **2772** Sage 200 Purchase Order line deletion error
- **2775** Sage 200 Customer delivery address browse error
- **2776** Sage 200 Supplier module payment term basis range error
- **2799** Sage 200 Price band download or browse error
- **2804** Sage 200 PO total amount not updating at Sage after stock code line deletion
- **2806** S200 SOP delete order line item error
- **2808** S200 Sales Quotation Print issue
- **2810** Sage 200 Amended workbooks for ranges format \& to exclude additional templates
- **2811** Sage 200 Purchase \& Sales Invoice error on download
- **2814** S200 PL Pay allocation error
- **2816** S200 Quotations allow generate doc number
- **2818** S200 PL Invoice message issues when saving to sage
- **2819** S200 Stock details update issue while click save to sage.
- **2820** S200 CB Receipts \- using project analysis causes object not set.
- **2821** S200 Sales orders download and error on save at Sales returns
- **2823** S200 Invoicing Credit note "Object reference not set to an instance of an object."
- **2825** S200 Sales quotation error on calculate values
- **2827** S200 SL Receipts validation error
- **2831** New browse doesn't "Add All" just filtered records
- **2832** Sage 200 Tax code error on Purchase order
- **2838** S200 Purchase Return detail ranges not detected
- **2839** S200 Purchase Returns error on browse \& validation
- **2840** S200 PL Pay allocation error on save to sage
- **2842** S200 Nominal code and browse error
- **2844** Sage 200 NL Journal Amended workbooks
- **2849** S200 CB Payments/Receipts tax posting error
- **2851** S200 POP Returns error on calculate saves \& save to sage
- **2853** File save options are not working
