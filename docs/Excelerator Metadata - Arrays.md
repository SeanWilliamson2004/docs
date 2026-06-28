---
title: Excelerator Metadata - Arrays
tags:
- Development
- Metadata
- Arrays
description: This page is intended for developers only and describes Excelerator arrays.
  Arrays Arrays metadata allows you add list of data against a single…
created: '2017-01-26'
modified: '2017-01-26'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Excelerator%20Metadata%20-%20Arrays.aspx
---

**This page is intended for developers only and describes Excelerator arrays.** 

# Arrays

Arrays metadata allows you add list of data against a single record of data. They are distinct from [Child Lists](Excelerator Metadata - Child Lists.md) in that they do not relate to open\-ended list of transactional details. They can be open\-ended or of fixed length. 

In Excelerator child lists are entered in multiple lines on the spreadsheet. Arrays are expected to have a limited number of items and can be entered on the same line as the row they relate to, on in a header at the top of the sheet. 

At the API level the array is a list property on the DTO class. In Excelerator the lists must to be of fixed length and ranges are generated with postfixes for the array index, allowing the ranges to be entered, for instance across a single row of the spreadsheet. 

## Array API Metadata

Arrays are list(of \< type \>) properties on the DTO. They have to be designated as arrays in the metadata, and metadata included about their properties, for the framework to be able to create, write to and read from ranges for the properties for elements on the array. 

To designate a property as an array you must either decorate it with the DTOFieldArray property: 



```vbnet
<DataMember()>
<DTOFieldArray("HeaderContactArray1Desc", 20, SpecialProperties.ComplexType, 3)> _
    Public Property HeaderContractArray1() As List(Of Contact)
```

or added to the metadata in separate code: 



```vbnet
Dim arrayList As ArrayMetaData
arrayList = .AddArray(Of TransdataHeaderDTO)(Function(x) x.HeaderContractArray1, 3)
```

The type used in the array should have the usual attributes added to its properties or added to the metadata in separate code: 



```vbnet
arrayList.Add(Of Contact)(Function(x) x.Name, "Name", 20)
arrayList.Add(Of Contact)(Function(x) x.Address, "Address", 30)
```

Note that the properties' details are being added to a list on the array not to the main metadata list

  
The array length is a default length. 

## Excel Metadata

In order to appear as ranges the array has to be included in the Excel metadata. The array itself needed to be specified, as do the individual properties. At this point the array length and descriptions can be overridden. 



```vbnet
With metaData.ExcelArrayMetaDataList
    Dim fld As ExcelBasicMetaDataField
    Dim fldArray As ExcelArrayMetaData = .Add(Of TransdataHeaderDTO)(Function(x) x.HeaderContractArray1)
    ' Add to list so that you can define properties on it.
    With fldArray
        fld = .ExcelBasicMetaDataList.Add(Of Contact)(Function(x) x.Name, HeadDetailInd.HeaderDetail, "")
```

Note that the properties' details are being added to a list on the array not to the main metadata list

  
It is also possible to override the description on the individual rows of the array: 



```vbnet
' Override the row description for element 3 of Name
fld = ExcelBasicMetaDataField.Factory(Of Contact)(Function(x) x.Name)
fld.Description = "Override row desc 3"
.ExcelRowMetaDataList.Add(3, fld)
```
