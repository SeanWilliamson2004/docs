---
title: "Excelerator Browses"
tags: ["Development", "Support"]
description: "Overview Browses help data entry by displaying cross referenced data for the range on the sheet currently selected. They allow the user to select…"
created: "2021-04-26"
modified: "2021-09-27"
original_url: "https://codislimited.sharepoint.com/sites/Wiki/Pages/Excelerator%20Browses.aspx"
---

<Note>
  This page covers the internal design and implementation of Browses. For end-user documentation on how Browses work in the product, see the relevant page in the [Excelerator help](https://help.codis.co.uk) — for example, the [Browses section of Sales Orders](https://sage-200-excelerator.help.codis.co.uk/sales-orders/#browses).
</Note>

## Overview

Browses help data entry by displaying cross referenced data for the range on the sheet currently selected.  They allow the user to select data that is then returned to the sheet.

Some functionality has been applied inconsistently as the product has evolved and as standards have not been cleared.  The document belows discusses the best methodology and how this has been applied.

In 2021, a new browse was introduced.  This has been used in a few S200 Excelerators, and is being used in Sage 50.  These were introduced to allow asynchronous data retrieval, meaning that the form is displayed immediately and populated when the data is retrieved.  

## New Browses

We have introduced new browses in some V3 S200 Excelerators.  These are similar in functionality, but they store their settings in a setting file and get the data asynchronously, meaning that the browse screen is displayed almost immediately whilst the data is retrieved.  Note: settings are held in files in the AppData\\Roaming\\Codis\\Excelerator\\BrowseSettings folder.

## Invoking Browses

There are 4 ways to show a browse:

- A right click on a browseable cell will display the usual Excel context menu, with a Browse option will be added at the top.
- Clicking the Browse button on the left hand Excelerator toolbar menu.
- Entering Ctrl-F2
- In Fast Entry mode.  Users can choice to activate fast entry mode.  In this mode, on exiting a cell in Excel, browses are automatically opened.

## Data Displayed

For browse datasets with a large number of fields, it can be better to limit the data fields that are displayed for performance and usuabilty.    The field that you are browsing on must always be displayed.  Other mandatory fields may depend on whether you a populating directly from the browse data (see Populating the Sheet below).  Browses with very few possible data fields may not allow fields to be selected.

**Old Browse**: some browses allow selection and reordering of fields.  Historically, the fields displayed were chosen by the developer and were hard coded.  Newer versions of the browse class force some mandatory fields.  

**New Browse**: most will allow selection and reordering of fields.  If the browse contains just a code and description, we don't allow selection.

This video shows how to add a field then reorder fields in the new browse.

## Primary Data Browse

Some browses are on datasets that drive the entry of data in that Excelerator and often populate multiple fields.  For instance, when browsing on a master record (customers, stock etc) Excelerator, if the browse is on the data itself being maintained (e.g. browsing on customers in Customers Excelerator).  These can be considered Primary Data browses.   If using a transactional Excelerator (SOP orders, POP Orders etc) then transactions are usually created for another primary data type.  For instance, orders are created for products or services and journals are for nominal codes.   These can also be considered Primary Data browses.  Secondary Data  browses will usually populate one cell, although some might populate two if the data type being browsed as e.g. a description range (like Vat code, Vat description).

## Single or Multiple Record Selection

The browse can allow either a single record or multiple records to be selected.  Single record selection browses will normally be faster as they require less key strokes.

If browsing on a single cell (in a header) then a single selection browse should always be displayed. 

If browsing on primary data (see above), multiple selection should be allowed.   Others should be single selection.  This is to follow the way that users tend to enter data.  They may want to create an order for multiple products, picking those products in one browse.   But it is unlikely that they would then select multiple VAT codes.  This functionality may be made user controlled.

When selecting multiple records, usually the selected record will not be removed from the list of records to select.  This is because, for instance, you can have orders that have multiple lines for the same product.  In some cases they will be removed from the list - when you should not repeat selections, like the stock browse in S200 Price Bands.

This video shows how to change from multi selection to single selection in the new browse.

\*\*Old Browse:\*\*implementation is inconsistent.

**New Browse:** applies the above rules except that where multiple or single selection could be used, it will allow the user to select whether to use multi or single when multi is possible.

## Populating the Sheet

When records are selected, the Excel sheet should be populated with the selected records.  There is then a decision as to what ranges on the sheet should be populated as a result of the selection.  If the browse is on primary data then all ranges for that line on the sheet should be populated, even if it involves overwriting blank values.  So, when browsing on stock when entering an order, selecting a product should populate all the cells on that line with whatever default data can be taken from the product.

**Old Browse**: implementation is inconsistent and is applied in the individual modules and browses

**New Browse**: provides a framework for automatically detecting whether data is needed to populate the sheet (including whether the range is on the sheet), and can populate the line or lines.  If another trip to get data is required, it is done asynchronously.  

## Filters

There are two different types of filter that can be used.  

- Full text search  - one piece of text that applies to the entire dataset displayed in the browse.
- Column filters - each column in the browse can be filtered by text entered per column.

These should have the following features:

1. When the browse is launched, if there is a value entered in the cell then this is placed in the full text search.  If the value results in a single row selection (unless in Fast Entry Mode) then the filter should be cancelled.
2. In Fast Entry mode a single row filter result
3. Full text search is incompatible with column filters.  One or the other has to be used.

**Old Browse**: column filters are only available on selected records which is pretty well pointless.

\*\*New Browse:\*\*the user can choose to have column filters on the selection window.  We need to resolve and test how this works with pre-entered text and Fast Entry mode.

This video shows how the full text filter is used.  It also shows full and partial matches using Fast Entry.  In Fast Entry mode, the tab key was used to move to the next cell, which activates Fast Entry.

## Downloads

In S1000 V1 Excelerator, downloads had ranges to select from.  In V3, downloads tend to be browses and the browses that have filters that provide functionality similar to the range selection (although this doesn't seem to work in the old browse).

There are usually primary data browses that function in an identical way to the downloads, the only difference being that the downloads clear the entire sheet (sometimes not header data) and then copy data in from the first line in the range.  

**Old Browse**: In some cases, possible all, common code is used, but that code, like the browse, does not handle the problem of field selection then populate fields well.

\*\*New Browse:\*\*the framework simplifies the tasks and suggests a generalised approach, as described above.

All downloads using the new browse should default to column filters.

## 