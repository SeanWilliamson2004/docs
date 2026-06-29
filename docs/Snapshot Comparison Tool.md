---
title: Snapshot Comparison Tool
tags:
- Testing
description: The snapshot comparison tool is a tool used by the development and testing
  departments to verify that parts of the Codis APIs work correctly.…
created: '2017-01-23'
modified: '2017-01-30'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Snapshot%20Comparison%20Tool.aspx
---

The **snapshot comparison tool** is a tool used by the development and testing departments to verify that parts of the Codis [APIs](https://en.wikipedia.org/wiki/Application_programming_interface) work correctly. 

## Overview

Testing of Sage 500/1000 Excelerators and APIs has always involved comparing data created by Sage with data created by our APIs. In the past, two methods have been used: 

- Manual inspection. This is very laborious and error prone
- Using an unload of the entire database following a Sage update then comparing with an unload of an entire data following an API update. This is also quite laborious, and differences are difficult to decipher.

Note: 

- "Expected" data – is the Sage data.
- "Actual" data – is the Excelerator/API version of the data.

The Data Snapshot Comparison tool has been developed to make this process easier. It provides two key areas of functionality: 

- A snapshot tool. This allows snapshots of Expected data to be taken. This then avoids the need to restore databases holding Expected data whenever a comparison with Actual data has to be made. The snapshot data is stored on the TestingConfiguration database.
- A comparison tool. This allows Actual data to be compared, on a column by column basis with the Expected data held in a snapshot, and then report details of any differences.

The model and service code is in Codis.Test.Utility. Sample setup methods are in Codis.Test.Utility.Test. 

## Entity Model

### Table Definitions

This defines a table that can be used in a snapshot. Included in the definition is the database table name, a description, a list of select keys and comparison keys. 

Select keys define the columns that are used to select a set of table rows that should be compared. The select keys may not define an individual table row, but a set of rows. The comparison keys are then used select individual rows within the sets for comparison. 

**Example 1**: a singleGL journal might have a number of records on the table scheme.nljrnm. All rows for the journal in the Expected data should be compared with their corresponding row in the Actual data. A select key of journal\_no will define the row set to be compared. A comparison key of page\_no will ensure that the correct row is chosen from the row sets. 

**Example 2**: a sales invoice can be identified by its item number, but there might be multiple pages for data for a single item. So again, page\_no will be a comparison key. You can also define which table columns to exclude from the comparison. Select keys (which can be different) and rowstamps are excluded automatically. 

### Snapshot Templates

These provide a template for a snapshot. They define which tables should be included in the snapshot, which system keys and project values should be included in the snapshot. 

### Snapshots

A snapshot only needs to have which template it relates to defined. The snapshot data will be populated when a snapshot is taken. 

### Setup and Configuration

If you right click in the TestingConfig entity diagram the option "Generate Database from Model" will be displayed. You can use this to create all the tables for the entity. Although the intention is to create a User Interface, at the moment configuration data and snapshots must be created and initiated from test projects. Having code that creates table, templates and snapshots means that this data can be quickly recreated should the database have to be remodelled. You then need to populate the Table Definition and Snapshot Template tables using a test method. 

### Taking Snapshots and Comparing

Use the ShapshotService class. 

The process usually is: 

- Carefully enter data into Sage.
- At the same time create and API/Excelerator test data holder that holds the same data you are entering into Sage. This could be a DTO generator class, or a spreadsheet.
- Take a snapshot of the Sage data using the TakeSnapshot method.
- Save your Test data in your DTO or spreadsheet to the Sage database using the API or Excelerator.
- Compare the Sage entered data with the API/Excelerator generated data using the CompareToSnapshot method.

The CompareToSnapshot method returns false if any differences are found. Differences are reported to the Debug output and to a logger configured in your test applications app.config 

### System Keys and Project Settings

The snapshot template includes a definition of the system keys and project settings that are likely to influence how data is entered and saved in Sage. When the snapshot is taken, the values stored in those system keys is recorded. Project settings cannot be captured in this way, as they are held in an encrypted table. These have to be specified when the snapshot is defined using: 

| ``` 1 ``` | ``` UseProjectInSnapshot(context, snapShot, "DA0370") ``` |
| --- | --- |

When the comparison test is run, the system key setting can be applied by running: 

| ``` 1 ``` | ``` RowComparisonHelper.SetSystemKeys(db, snapShotCompareTo) ``` |
| --- | --- |

And project settings by running:

| ``` 1 ``` | ``` RowComparisonHelper.OverrideProjects(db, snapShotCompareTo) ``` |
| --- | --- |

Often, both these are called as part of a 

| ``` 1 ``` | ``` Protected Sub CompareResultToSnapshot(baseDTO As NLJournalBaseDTO, snapShotDesc As String)
  ``` |
| --- | --- |

method that is included in the base comparison test class. 

See also [Automated Testing \- Sage 1000 APIs](Automated Testing - Sage 1000 APIs.md)
