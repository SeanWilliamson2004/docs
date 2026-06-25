---
title: Excelerator Metadata
tags:
- Development
- Metadata
description: This page describes how Excelerator metadata is built and is intended
  for developers only. Overview Excelerator metadata defines the ranges that can…
created: '2017-01-26'
modified: '2017-01-26'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Excelerator%20Metadata.aspx
---

**This page describes how Excelerator metadata is built and is intended for developers only.** 

## Overview

Excelerator metadata defines the ranges that can be used by Excelerator. It is used by the framework to list the ranges available in the Excelerator Designer screen, and all the details associated with the ranges such as a description and type of data. 

Excelerator metadata is built by combining metadata from two sources: 

- "API Metadata" \- metadata associated with the API data transfer objects
- "Excel Metadata" \- metadata that extends the API metadata with information relating to spreadsheet type input and output.

## API Metadata

API Metadata was always extracted from data transfer objects (DTOs). These DTOs are light\-weight classes that have properties that are decorated with attributes that hold metadata. Utilities are used to extract the metadata from the DTOs. These utilities understand any parent\-child relationship between DTOs and recurse this relationship to build a list of all properties in the parent\-child tree. API Metadata should be generated in a class that implements the IMetaDataSource interface, and then injected into the container. 



| ```  1  2  3  4  5  6  7  8  9 10 11 ``` | ``` Public Class MetaDataSource         Implements IMetaDataSource         Protected Property AttributeBasedMetadataBuilder As New AttributeBasedMetadataBuilder           Public Overridable Function GetMetaData() As API.Types.MetaData.MetaDataDefinition Implements IMetaDataSource.GetMetaData             Dim metaDataList As MetaDataDefinition = AttributeBasedMetadataBuilder.GetDTOInformation(GetType(TransdataBaseDTO))               metaDataList.DebugMe()             Return metaDataList         End Function     End Class  ``` |
| --- | --- |

From version V3\.1 of the Excelerator framework, the ability to generate metadata from separate code has been added. This allows attribute free DTOs that can be accepted by the Sage 200 Cloud version whitelist. 



| ``` 1 2 3 4 5 6 7 ``` | ``` Public Overridable Function GetMetaData() As API.Types.MetaData.MetaDataDefinition Implements IMetaDataSource.GetMetaData             Dim metaDataBuilder As New MetaDataBuilder               With metaDataBuilder                 .AddGroups(Of TransdataDetailDTO)(2, "") ...              .Add(Of TransdataHeaderDTO)(Function(x) x.Prop1, "Prop1 desc", 10)  ``` |
| --- | --- |

## Excel Metadata

Excel metadata allows some API metadata like descriptions to be overridden, and extends the metadata with information like defining any browses associated with the property and display groups used in Designer. Excel metadata must be generated in a class that implements the IExcelMetaDataSource interface and injected by the container. Metadata is specified in code in a similar way to the new API metadata creation option in V3\.1\. 



| ```  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 ``` | ``` Implements IExcelMetaDataSource Public Overridable Function GetMetaData() As MetaData.ExcelBasicMetaData Implements IExcelMetaDataSource.GetMetaData             Dim metaData As New ExcelBasicMetaData             metaData.HasDownloadOnlyRanges = False             With metaData.GroupHeadingsList                 .Clear()                 .Add(New ExcelDisplayGroup("HeaderGroup", "Header Group"))             End With             With metaData.MetaDataFields                 Dim fld As ExcelBasicMetaDataField = .Add(Of TransdataHeaderDTO)(Function(x) x.HeaderStringProp1, HeadDetailInd.HeaderDetail, "HeaderGroup")                 fld.SpecialProperties = ExcelSpecialProperties.IsControlRange                 .Add(Of TransdataHeaderDTO)(Function(x) x.HeaderStringProp2, HeadDetailInd.HeaderDetail, "HeaderGroup")                 With fld                     .OverrideRangeName = "OverrideProp1"                     .PreviousVersionRangeName = "PreviousNameProp1"                 End With  ``` |
| --- | --- |

## Special Metadata

[Excelerator Metadata \- Arrays](Excelerator Metadata - Arrays.md)
