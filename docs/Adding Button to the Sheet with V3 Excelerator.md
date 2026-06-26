---
title: Adding Button to the Sheet with V3 Excelerator
tags:
- V3
- Consultancy
- Development
description: Adding Buttons on the Spreadsheet Buttons to invoke menu items It is
  possible to add buttons to a spreadsheet that invoke Excelerator menu options.…
created: '2017-07-20'
modified: '2025-06-05'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Adding%20Button%20to%20the%20Sheet%20with%20V3%20Excelerator.aspx
---

# Adding Buttons on the Spreadsheet

## Buttons to invoke menu items

It is possible to add buttons to a spreadsheet that invoke Excelerator menu options.   
The button must be linked to VBA code.   
  
Example of VBA code:  



```
Sub RunCBPaymentsSave()


 Dim addin As COMAddIn
 Dim adxModule As Object

 Set addin = Application.COMAddIns.Item("Codis.Excelerator.Standard.SharedAddin.AddinModule")
 Set adxModule = addin.Object

 Call adxModule.InvokeMenuOption("Codis.Excelerator.Standard", _
 "CB Payments", "SaveBatch")


end sub

```

  
Apart from any custom functionality you might want to add, the lines of code other than the line starting with "Call adxModule.InvokeMenuOption..." will be consistent for any menu option. The parameters sent to InvokeMenuOption will vary depending on the menu option you wish to run. These parameters are:

- containerAssembly: name of the assembly used to specify the application e.g "Codis.Excelerator.Standard"
- moduleCaption:The caption for the module whose method you wish to invoke eg. "CB Payments"
- methodName:The method name for that module e.g "SaveBatch"

## Invoking other Excelerator methods


```
Sub ValidateCustomers()
    Set exObj = CreateObject("Codis_Excelerator_Sage200_SharedAddin.AddinModule")
    Set custSheet = Worksheets("Multiple")
    ' Comment in to activate non-interactive mode
'    exObj.InvokeExceleratorMethod "Codis.Excelerator.Sage200.Standard.Customers.Factory", "set_NonInteractiveMode", True
    
    Dim valResult
    Set valResult = exObj.InvokeExceleratorMethod("Codis.Excelerator.Sage200.Standard.Customers.Factory", "ValidateBatch")
    
    

End Sub

```

  


   


  


 In this example, two methods are called.  

The first one is a Subroutine without parameters or a return value.  The method is called "DownloadCustomer"

The second is a function that returns a string and takes one parameter "CustomerDTO.AccountReference".   If two parameter or more are required, they can be added at the end of the InvokeExceleratorMethod  


## Using Methods that Return Lists of Values

Due to limitations on the types that can be passed from managed code (Excelerator) to unmanaged code (VBA) the generic functionality above does not work with the standard validation and save methods.

To deal with this we've introduced special invocation methods for the main Save and Validation methods.  (Available from version 3\.2\.80\).  



```
Set exObj = CreateObject("Codis_Excelerator_Sage200_SharedAddin.AddinModule")
    Set custSheet = Worksheets("Worksheet")
   
    custSheet.Activate

    Dim errCol
    Set errCol = exObj.InvokeValidationMethod("Codis.Excelerator.Sage200.Standard.Customers.Factory", "ValidateBatch")
    Dim var2
    If errCol.Count > 0 Then
        Set var2 = errCol(1)
        MsgBox (var2.MessageId & ":" & var2.Description)
    End If

For a save:

    Dim errCol
    Set errCol = exObj.InvokeSaveMethod("Codis.Excelerator.Sage200.Standard.Customers.Factory", "SaveBatch")
    Dim var2
    If errCol.Count > 0 Then
        Set var2 = errCol(1)
        MsgBox (var2.MessageId & ":" & var2.Description)
    End If

```
