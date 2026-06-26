---
title: Automated Testing - Excelerator
tags:
- Testing
description: This page describes how to build fully automated tests for Sage 1000
  Excelerator using OpenXML. Overview Testing Excelerator itself rather than the…
created: '2017-01-23'
modified: '2017-02-08'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Automated%20Testing%20-%20Excelerator.aspx
---

**This page describes how to build fully automated tests for Sage 1000 Excelerator using OpenXML.** 

## Overview

Testing Excelerator itself rather than the API can present some challenges. The Excel interface itself is not easily automated using e.g. CodedUI and the Excel application is very heavy and difficult to create and teardown as part of a unit test run. 

OpenXML (see below) allows for lightweight and efficient interaction with spreadsheets and using it we can create relatively fast unit tests for the Excelerator programs. The Excelerator framework interacts with the spreadsheet for basic IO and adding named ranges via our own interfaces. In normal operations, these interfaces are implemented by classes that use the Excel object model. We have created similar classes that implement these interfaces but interact with the spreadsheet using OpenXML, and in the testing environment we can use our IOC architecture to inject these OpenXML classes in place of the Excel classes, meaning apart from the interactions with the spreadsheet that are carried out using OpenXML, all other functionality should be as for an Excel implementation. For the most part, the OpenXML classes provide identical functionality, except that they do not require Excel to be running and are far lighter and faster. 

Ranges can be added to sheet, values populated in those ranges and values read from the ranges. This means that the framework functionality above the basic IO can be tested using automated tests and OpenXML. This includes the algorithms used to convert the hierarchal DTOs into the grid structure spreadsheet. (These tests are in Codis.Excelerator.Tests) 

In addition to this we provide hook in points at a level just below user interactions, allowing powerful tests at a higher level to be run without any user interaction. 

## OpenXML

[https://en.wikipedia.org/wiki/Office_Open_XML](https://en.wikipedia.org/wiki/Office_Open_XML)

Note that OpenXML is the default format from Office 2007\. .xls files are not in OpenXML format. OpenXML includes a API for accessing and manipulating OpenXML format spreadsheets. An xlsx file (for instance) can be accessed directly using this API. 

The OpenXML API itself is a bit basic, so at Codis we've tried to use wrapper APIs. We tried ClosedXML but preferred EPPLUS. (Can't recall why at time of writing.). We have in turn wrapped these APIs in our own interfaces and created base and helper classes. 

## Test Classes

There are a few base classes that can be useful. 

### General Excelerator

**TestBaseOpenXMLBase**\- inherits an API specific version of a base class such as TestBaseEPPlusBase, which itself needs to be a sub\-class of AbstractDependencyInjectionSpringContextTests (see [http://www.springframework.net/doc\-latest/reference/html/testing.html](http://www.springframework.net/doc-latest/reference/html/testing.html). 

**TestBaseEPPlusBase** \- This class include some public properties can be useful in tests, and that will be instantiated by the container. It has a utility method OpenWorkbook It then sets any spreadsheet IO objects on this properties to use the appropriate EPPlus OpenXML API. 

**CustomOptionsProvider** \- Use this class to override client side options.

```vbnet
Try
    Dim customOptions = new CustomOptionsProvider(Excelerator)
    customOptions.OverrideOption("IgnoreBlankCells", False)
    Excelerator.OptionsConfigurationProvider = customOptions

    InitialiseStatus()
    ' ...

Protected Overrides Sub InitialiseStatus()
    SetUpObjects
    Excelerator.DefineRanges
    Excelerator.ValidateRanges
End Sub
```

### Sage 1000

**TestBaseOpenXML** \- inherits TestBaseOpenXMLBase with its spring ioc and spreadsheet manipulation functionality, but adds functionality to allow the standard connection configuration to be changed. 

**TestBaseOpenXMLRollback** \- inherit this class to create a test class that will automatically wrap each test in a transaction that is rolled back at the end of each test. It inherits TestBaseOpenXML and uses the utility RollbackHelper to control the transaction. 

### Browses

TestBaseOpenXMLBrowseAndPopulate superceeds TestBaseOpenXMLBase2Browse. Both classes offer a means of automatically testing what is a process that normally involves manual UI. They do this by injecting a different browse form factory into the browse base class, which produces a class that does't display a form and automates the interactions. Both test that records are returned to the browse. The former extends the functionality of the latter by adding the capability to select a record from a browse and populate the sheet, and testing the value that appears in the sheet. 

The BrowseRanges method of the ExceleratorBase class is called by both classes. This method does not throw exceptions but will appear to have found 0 records. As such, a broad range of errors in this method can appear as 0 record found assert failure.

## Sage 1000 Enterprise and Standard testing

It is generally good practise to produce Excelerator tests that can be used in both Enterprise and Standard configurations. The obvious technique to this is to have a common assembly that is used by two different test assemblies for the different configurations. This was used successfully but a problem has appeared at some point. 

Test methods on classes inherited from different assemblies are not picked up by either mstest or reshaper test runners. see [this stackoverflow article](http://stackoverflow.com/questions/6002424/inherited-test-class-from-generic-base-is-ignored-in-mstest).

To get around this, and to still have a shared codeset between the configurations, we can use linked source files. 

To add a linked item: In Solution Explorer, right\-click your project, and then select Add Existing item Or, you can type Shift\+Alt\+A. In the Add Existing Item dialog box, select the file you want to add, and in the Add drop\-down list, click Add As Link. 

Tests that update records should rollback those changes (see above as to how. This is not supported in the Enterprise configuration so these tests must only be in the standard test assembly.) 

**Assembly not loaded error:** Sometimes when running tests you can get an error that an assembly won't load because the file is found despite it being referenced and marked to copy local. A workaround for this problem is to either include the item as a DeploymentItem on the tests\-see below. This can be a bit labourious, and another technique that can work is to directly use the assembly in code.



```vbnet
<TestMethod()>
<DeploymentItem("Codis.SageEnterprise.Distribution.Common.dll"), DeploymentItem(TestWkb1Deploy)>
Public Sub TestSettlementDiscountCategoryBrowse()
    TestBrowsePopulates(TestWkb1, "CL3", "SettlementDiscountCategoryBrowse", "L1", Function(x) x.SettlementCategory)
End Sub
```

### Sage 1000 Standard Excelerator Connection Configuration

TestBaseOpenXML and TestBaseOpenXMLRollback both use the **TargetDatabase** to determine which Sage database to use.  This is set to S5V71B1 by default but can be overridden in sub\-classes.  


This is acheived by having the Codis.Excelerator.Standard.ConfigurationProvider replace the usual configuration provider.  The database settings in this object are then overridden in the SetUpObjects method.
