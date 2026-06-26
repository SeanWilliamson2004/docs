---
title: Excelerator Development
tags: []
description: Overview Excelerator software has to implement a number of different
  configurations. See Codis Software Deployment Configurations.aspx . It also…
created: '2020-03-30'
modified: '2020-04-01'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Excelerator%20Development.aspx
---

# Overview

Excelerator software has to implement a number of different configurations.   See [Codis Software Deployment Configurations.aspx](Excelerator Deployment Configurations.md).   It also implements multiple modules\- each module relating to a particular accounting function.  See also: [Development History of Excelerator.aspx](Development History of Excelerator.md).  


To do this the software has to seperate into layers:  


- Client only layer
- Client\-Server bridge (Sage 200 only)
- Server

  
There are assemblies that are consumed by all layers that are types that are passed between the layers.  Typically these are serialisable data transport objects (DTOs) and service interface definitions.  These have common elements across modules and products.  


Each layer has common code that is consumed across products and modules.  


The client components use the DTO to define the Excelerator ranges.  Information is extracted from attributes on the DTO properties and combined with Excelerator specific information defined at the client level.  This means that the framework can generate a DTO that can then be passed directly to the server side for validation and then to Data Access Objects (DAOs).  


All S1000 components and Sage 200 client side components use [Codis Development Framework \- IOC Spring\-Net.aspx](Codis Development Framework - IOC Spring.Net.md) to manage most of the objects.  

S200 uses an API from Sage to access data.  This API does apply business rules but lacks some functionality meaning that there still is some need for business rules to be applied in the Codis S200 code.  


S1000 did not provide a suitable API.  Our Codis APIs have to apply all business rules and they have to access databases directly.  S1000 uses a part of the Spring\-net framework to help build code to access the databases.  


S1000 and S200 use Spring\-Net AOP to apply policies to certain objects.  For instance, some service require authentication and access opened to the underlying APIs or DAOs.  AOP allows these policies to be implemented externally via a configuration file.  This varied for different configurations of our products.  For instance, a call to the service can be made either directly to an assembly or to a WCF service.    


# Module Structure

A basic S1000 Excelerator modules has three projects:

## Codis.Excelerator.\<Module Name\>

This holds the client side code.  It references the Excelerator framework projects and its types.  It does not reference the Codis.SageEnterprise.\<Module Name\> project.  


It should contain a "Excelerator" class that inherits from Codis.Excelerator.Core.ExceleratorBase class, or one its subclasses.  The Excelerator class is responsible for coordinating Excelerator operations such as Save, Download and Browse.  Before most operations it must define the Excelerator Ranges.  (These are then cached).  Operations usually involve interactions with Excel via the framework, and interactions with Server services.  


Interactions with the sheet are via the Ranges.   Excelerator Ranges are areas on a worksheet marked as relevant to Excelerator. These ranges are usually defined based on a DTO.  There are framework methods to simplify interactions with the Ranges on a worksheet based on a DTO and the Excel application object.  For instance, values in Excelerator Ranges for an entire worksheet can be loaded using a single call to the framework.  


Interactions with services are via calls to interface methods defined in the types module.   The concrete implementation of the interface is provided by IOC implemented by the Spring framework.  This is done by another project.  The Standard configuration project Codis.Excelerator.SageEnterprise.Standard will provide the Codis.SageEnterprise.\<module name\> API class.  This project will directly reference the Codis.SageEnterprise.\<module name\> project, but the Codis.Excelerator\<Module Name\> project will not.  The Enterprise configuration project Codis.Excelerator.Enterprise.Clients provides a proxy class (to a WCF service) as the concrete implementation.    


This way a single Codis.Excelerator.\<Module Name\> project can be used in both Standard and Enterprise configurations.  


This project will also contain a class that provides Excelerator related metadata to compliment the metadata provided by the Codis.SageEnterprise.\<Module Name\>.  This information is combined to make the Ranges definition.  


## Codis.SageEnterprise.\<Module Name\>

This holds server side code.  It references the Server side projects and its types.  It will contain an API class that inherits Codis.API.Framework.BusinessAPI class and it will implement a service Interface that inherits from Codis.API.Types.Interfaces.IBusinessAPI.  


This project will also implement a validation subsystem for the module.  This will be invoked from the API class and will typically consist of a number of validation classes that are run as a group.  Each class will receive a DTO and will ideally apply a single business rule and define behaviour for validation behaviour.  (In reality there are validation classes that define multiple rules as some rules are difficult to separate.)  


There should also be a class that provides metadata about the DTO.  This is extracted server side to allow it to be used in different clients.  There are classes within the server side framework that will automatically extract information from the DTO and its attributes.  


## Codis.SageEnterprise\<Module Name\>.Types

This holds the DTOs and the service interface definitions.  Typically types are included in a common Types level project such as Codis.SageEnterprise.Finance.Types  


DTOs are basic classes that define data that is entered in the Excelerator.   This normally reflects a logical business view of the data as Excel allows an open definition of data input that is limited to 2 dimensions.  DTO must inherit the Codis.DTO.Base.BusinessDTO class (or one its subclasses).   Data can be hierarchical and there are based classes in the framework that allow that relationship to be defined by having lists of classes within a class.  If these are correctly defined, the Excelerator framework will recognise this when reading or putting data to the Excel worksheet.    


## Codis.Excelerator.\<Module Name\>.Standard

In addition to the three projects above, for a standard (fat client solution) an Excelerator.Standard project will be required.  This will define an IOC container for the module that defines the concrete classes to be used that are unique to Standard configuration.  


There are also AddinDef.xml files in this project \- one for each module.  These define the Ribbon menus that appear in Excel and how the menu options hook into the Excelerator class.  These are content files that should be copied to the output as they are deployed.  


# Getting the Excelerator Ribbon to Appear

Each Excelerator product must be registered as an addin in Excel and this registration points to a location.  Each product is registered separately so each product can only run from one location.  Because of this if developing Excelerator, DO NOT INSTALL EXCELERATOR.  If it is installed, uninstall it.  You want to version you build to be the one that is registered.  


For Sage 1000: Build the Codis.Sage1000\.Standard.WixInstaller.sln solution with the solution configuration "Debug" selected.  Once it is built go to Sage1000\\V3\\Excelerator\\Codis.Excelerator.Sage1000\.Standard.Addin\\bin\\Debug.  There should be a ADXRegister.bat file in there.  Run it.    


For Sage 200: Build the Codis.Sage200\.WithInstallers.sln solution.  The solution configuration you use depends on the version of Sage 200 you are working with.  As development PCs tend to have the latest, use SPE2019Debug.  Go to the folder Sage200\\Excelerator\\Codis.Excelerator.Sage200\.Standard.Addin\\bin\\SPE2019Debug.  There should be a ADXRegister.bat file in there.  Run it.  

As Support can tell you, getting the registration to work can be a challenge and there are a number of problems and solution detailed here: [https://codislimited.sharepoint.com/sites/Wiki/Pages/Excelerator%20Client%20Installation%20and%20Setup%20Guide.aspx](Excelerator Installation Troubleshooting.md).  Generally, we don't get these issues on our development machines.
