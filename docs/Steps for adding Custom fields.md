---
title: Steps for adding Custom fields.
tags: []
description: Overview This document describes how to customise Excelerator using the
  Excelerator plugin framework. The plugin framework scans for assemblies in…
created: '2021-06-08'
modified: '2021-06-08'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Steps%20for%20adding%20custom%20fields.aspx
---

# Overview

This document describes how to customise Excelerator using the Excelerator plugin framework.  The plugin framework scans for assemblies in the folder \<??\> looking for assemblies that contain classes that implement certain pre\-defined classes or interfaces.  The framework then loads these assemblies and call given hookin points during processing, allowing the behaviour of Excelerator to be modified.  


It is helpful to follow predefined standards for nomenclature and source code control.  Store all work in a new Git repository in Azure Devops named: \<??\>

Excelerator is divided into client\-server architecture even in a pure client deployment.   Data is moved in DTOs (data transfer objects) between Excel, the client layer, the server layer and into Sage.   DTOs are structured according to the business entity being used.  For instances, the sales order Excelerator will use main DTO that has a list of sales order header DTOs (order no, customer etc) and each of those has a list sales order details DTOs.  Custom data can be added in soft lists to each of these DTOs.  


You will need to create two projects.   


The steps are:  


1. Create the Client Side Plugin
2. Create the Server Side Plugin
3. Create the data base object
4. Deploy the plugins and set the plugin path on each client.

# The Client Side Plugin

Create the client side project with naming convention (Codis.S200\. \<Project Name\>. \<Module Name\>.Customization either in VB.NET or C\-Sharp.  This project must be signed using Codis.snk and it should contain:  
1. All Browse classes.
2. Your client side plugin class.  This class is used to define the Excelerator ranges

Your client side plugin class must derive from Codis.Excelerator.Shared.ExCustomisationStartupBase class.    

The ExCustomisationStartupBase class has abstract properties and methods that have to be implemented by you:

1. **AssemblyTypes**: List of factory classes that this plug\-in links to. For example, to link to sales order excelerator use: "Codis.Excelerator.Sage200\.Standard.SalesOrder.Factory"
2. **InternalInitialise**: This method is passed the excelerator object that the plugin is linked to.  You can use the excelerator object to wire\-up events or get the objects like "SpreadSheetIOAPI".
3. **AddCustomMetadata**: This method can be used to add the excel metadata and API metadata before loading ExcelMetaData object

And overridable methods:  


1. **BeforeDownloading**: This method is invoked before downloading items like Sales order, Quotation… This method should be called from actual module like Sales order's Excelerator class.
2. **AfterDownloading**: This method is invoked after fetching data from the Server API.


> 

# The Server Side Plugin

Create a new project with naming convention (Codis.S200\. \<Project Name\>. \<Module Name\>. Server.Customization either in VB.Net or C\-Sharp. This project must be signed using the Codis.snk.

The project must include your plugin API class which must be derived from Codis.Server.Plugins.ServerPluginBase class. This base class has abstract properties that must be implemented by you:

- **ModuleNames As List(Of String)**.:Use this property to identify the relevant server\-side api. Eg.. for value "SalesOrder", it will link to SalesOrderServerAPI. This module name must be the same as module name define in the AddinDef file.

  
It also has overridable Methods :  
- Run : This is the first method called and called just once when the server object instance is created. Override this method to initiate any additional objects.
- InternalDeleteStart : This method is used to write code for before deleting record.
- InternalDeleteEnd : This method is used to write code for deleting record
- InternalSaveStart : This method is used to write code for before saving record.
- InternalSaveEnd  : This method is used to write code for saving record.
- **InternalValidationStart** : This method is called before the Codis validation routines are run.  It is passed one parameter of type ValidationArgument which has a property 

ValidationObject which is the main DTO object being validated.  You would typically run validation on the object that needs to be carried out before the main validation.  See Validation below.
- **InternalValidationEnd** :This method is called before the Codis validation routines are run.  It is passed one parameter of type ValidationArgument which has a property 

ValidationObject which is the main DTO object being validated.  You would typically run validation on the object that needs to be carried out before the main validation.  See Validation below.

## Validation

Validation should be carried out by validation classes that inherit from Codis.Server.Plugins ValidationBase.  Business rule validation failures should call the method AddMessage(msgText), passing a helpful message.

  


# Sage Database object

 Create data base object (Persistent classes / schema) using SageObjectStoreBuilder.exe". These are persistent classes are used when required object is not in API.  


# Deploy the Plugins and Set the plugin path

  


1. Create an output folder with naming convention \<ProjectName\+'output'\> on any drive. Under this folder create another folder 'Customization'. The output of the above two projects should go into 'Customization' folder.
2. In Excelerator, goto Select Modules option and then go to Display Settings. Then set PluginPath to the output folder.

Note : For reference please check projects in MJFrench or OneSys repositories.
