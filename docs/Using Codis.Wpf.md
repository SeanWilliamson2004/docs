---
title: Using Codis.Wpf
tags:
- Development
description: The Codis.Wpf library was created to try to get Excelerator User interactions
  to look as consistent as possible. It provides a number of components…
created: '2020-06-04'
modified: '2020-06-12'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Using%20Codis-Wpf.aspx
---

The Codis.Wpf library was created to try to get Excelerator User interactions to look as consistent as possible.  

It provides a number of components and styles to use in any Excelerator UI.  All work with viewmodels that match the class and have a matching inheritance tree.  

- CodisFormBase \- a base form that draws a custom menu bar that can be used for all forms.  A caption can be displayed in the menu bar.
- CodisButtonForm \- a base form that inherits CodisFormBase that adds a button bar with buttons to the bottom of the form and a grid to add content to.    Closes the form if a button is pressed.
- CodisDialog \- a base form for dialogs that inherits CodisButtonForm.  Displays two rows of text ("instructions") and creates a third row to put extra detail if needed.   The areas are not shown if the text on the viewmodel is nothing.
- MessageDialog \- a form for displaying general messages that inherits CodisDialog.  It adds a detail text area to the two other text area which is only displayed if a "Show Details" button is clicked, which is only available if the Detail text on the viewmodel is not nothing.
- WarningDialog \- a form for displaying validation messages that inherits CodisDialog.  It adds a list of options to two text areas that is displayed if the OptionList on the viewmodel is not nothing.
- ButtonFormWithValidation \- inherits CodisButtonForm and adds a framework for creating a user control that is displayed on the form, calling a validation method when the OK button is clicked.

Most forms to convert to the standard format should inherit CodisButtonForm, unless they follow the format of text lines then hidden detail.  CodisButtonForm imposes a standard menu bar, border and buttons.   Content should be in a UserControl.  This can be added to the form by creating a new form that inherits CodisButtonForm, overriding AddFormContent then adding the user control to the ButtonFormGrid.  SetViewModel can be overridden to set DataContext of the UserControl.   Override the OnButtonClick event to handle the Save etc.  

```
Public Class CRMSettingsForm

    Inherits CodisButtonForm(Of CRMSettingViewModel)



    Private _crmSettingControl As CRMSettingControl

    Protected Overrides Sub AddFormContent(contentBorder As Border)

        MyBase.AddFormContent(contentBorder)

        _crmSettingControl = New CRMSettingControl



        ButtonFormGrid.Children.Add(_crmSettingControl)

    End Sub



    Protected Overrides Sub SetViewModel(viewModel As CRMSettingViewModel)

        MyBase.SetViewModel(viewModel)

        DataContext = viewModel

        _crmSettingControl.DataContext = viewModel

        _crmSettingControl.txtPassword.Password = viewModel.Password

    End Sub



    Protected Overrides Sub OnButtonClick(sender As Object, e As RoutedEventArgs)

        SetButtonResult(CType(sender, Button))

        If CType(e.Source, Button).Name = "btnOK" Then

            CType(DataContext, CRMSettingViewModel).Password = _crmSettingControl.txtPassword.Password

        End If

        Me.Close()

    End Sub


```

All the forms encourage the use of a viewmodel by having their controls bind to them.   For instance, CodisButtonForm uses CodisButtonFormViewModel which just holds a caption.  Ideally, you should expand this viewmodel by inheriting it, but this may make conversion slow.  Your new form can self\-initialise the view model and not use it other than for the controls in the base form.    

## Using the forms

The new forms all use WPF resources that have to be loaded.  There is not a WPF application context available in the Excelerator addin to load the resources into, so that have to be loaded into each window that uses them.  To facilitate this, there is the WPFControlServer class in Codis.Wpf.  Its GetControl method will create a new instance of the type required and set its resources.  The resources are loaded once per instance of this class.   It also exposes the resources if needed directly.  
To simplify the use of this class there is a shared class CustomMessage.  This has an shared instance of WPFControlServer meaning that the resources should only be loaded once per session.  (This combination was the only way I could get it to work.)   It also has some helper methods, including one to replace the old style CustomMessage invocation that is used all over the code base.  
So this will work:  

```
Dim postedDownload = CustomMessage.WpfControlServer.getControl(of DownloadPostedForm) 


```

## Using the Buttons in other forms

The CodisOKButton and CodisCancelButton can be used in any form but the following code must be added to the code behind for the Accent style to work...  

```
    Public Overrides Sub OnApplyTemplate()

        MyBase.OnApplyTemplate()

        Dim accentBrush = TryCast(TryFindResource("AccentColorBrush"), SolidColorBrush)

        If accentBrush IsNot Nothing Then accentBrush.Color.CreateAccentColors(Me.Resources)

    End Sub


```
