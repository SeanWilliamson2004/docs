---
title: Sage 200 Cloud Excelerator Architecture and Coding Guidelines
tags:
- Development
- Sage 200
- Excelerator
- Sage 200 Extra Online
description: This page describes the framework architecture and coding techniques
  that should be used for developing Sage 200 Cloud Excelerators. It is intended…
created: '2017-01-28'
modified: '2017-02-27'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Sage%20200%20Cloud%20Excelerator%20Architecture%20and%20Coding%20Guidelines.aspx
---

**This page describes the framework architecture and coding techniques that should be used for developing Sage 200 Cloud Excelerators. It is intended for developers only.** 

# Overview

From V3\.1, Excelerator will be supporting the Sage 200 Extra Online solution.   

Sage 200 offers a simple means of porting your application using their objects that reside on both the client and the server.  Sage components understand whether they are client or server side and communicate with each other.  However, this architecture results in poor performance as heavy weight Sage objects have to be frequently  serialised and transfered over the cloud.  For instance, in a validation routine, each time data is cross referenced, Sage objects have to be serialised and passed over the cloud.

To optimise performance, a new architecture had to be developed.  This architecture should work for both Sage 200 Extra Online and Sage 200 On\-Premise.  

An architecture was chosen that sends light\-weight Data Transfer Objects (DTOs) from client side components to Codis objects that reside on the Sage cloud server. These light\-weight DTOs are the DTOs that our Excelerator layer works with. 

Note that in an on\-premise deployment, all components reside on the client.

# Coding Guidelines

Sage have stringent security restrictions on assemblies that are deployed to their Cloud server. Many commonly used .net coding techniques are not allowed, including reflection, attributes that inherit from System.Attribute garbage collections, late binding and WCF service attributes. Spring Assemblies or any other injection engine that we've tried have also been excluded. This in turn means that our Spring based validation engine cannot be used. To accommodate this, we deploy as little as we have to server side and the code that is deployed has to be refactored or written to fit in with these restrictions. 

Assemblies can be validated as being able to be deployed server side using a validation facility provided by Sage. 

### Disallowed Code

The following are not allowed: 

1. References to System.Reflection
2. Late binding
3. Garbage collection
4. Spring
5. Any other IOC container manager that we've tried, so no injection is possible
6. File system access
7. Log4net
8. Collections (Lists are ok)
9. Licencing components

### References to System.Reflection

Generally, there aren't many uses of reflection in the functionality that has to go server side other than the injection engine. Where it is used in code, you will have to find another way of coding the functionality. 

### Late binding

The errors thrown by the Sage validation are not very helpful. Setting project warning configurations to disallow Late Binding and "Implicit type, object assumed" will help a lot with these issues. 

![](images/Development_Development_Wiki_Images_ProjectWarningConfiguration.jpg) 

### Garbage Collection

Remove this from all server side code. It can be done client side, where it will still work for standard type deployments and client side objects. 

### Spring

- Injection is covered below.
- For validation, the [New Validation Engine](New Validation Engine.md) has to be used.
- Message mapping is now done client side.

### Injection

We can no longer use injection. Public properties that would be inject should be expanded to have no longer be automatic variables. (Use Resharper Ctrl R E) They should then have code added to initialise the private variable to the default concrete class. Note that the property is decorated with the IgnoreDataMember attribute. Without this, Sage will attempt to serialize the properties type, which can result in errors. 



```xml
<IgnoreDataMember>
   Public Property NLJournalValidatorGroup As DTOValidatorGroup
       Get
           If _nLJournalValidatorGroup Is Nothing Then
               _nLJournalValidatorGroup = New NLJournalValidatorGroup
           End If
           Return _nLJournalValidatorGroup
       End Get
       Set(value As DTOValidatorGroup)
           _nLJournalValidatorGroup = value
       End Set
   End Property
```

### File system access

Generally, this is not required server side. 

### Logging and Log4Net

The ILog type is still available. This can be included and any logging should check if this is nothing first. The Sage Online notes suggest that it is possible to use log4net, so this area requires further investigation. 

### Collections

The collection type is not whitelisted. 

### Change the project MyType

This can be done by directly editing the project file. (Unload the project, then right\-click edit). In the XML below, change the MyType property to "Test"



```xml
<Project ToolsVersion="4.0" DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
   <PropertyGroup>
     <Configuration Condition=" '$(Configuration)' == '' ">Debug</Configuration>
     <Platform Condition=" '$(Platform)' == '' ">AnyCPU</Platform>
     ...
     <MyType>Windows</MyType>
 ...
   </PropertyGroup>
```

# Architecture

## Overview

![](images/Development_Development_Wiki_Images_Sage200Architecture.jpg) 

In this architecture, DTOs are populated and passed once to server side components where validation and CRUD operations take place on one go without to and fro traffic across the cloud

## Cloud Server Side Assemblies

#### **Codis.Sage200\.\<Module\>.Server**

These assemblies are deployed client and server side.   If running in a cloud deployment, it's methods are invoked client side but internal code within the assembly will dispatch a call to the server side web service.

This layer provides validation and CRUD and browse data retrieval services in a service class. Generally, the service methods only receive and return light\-weight DTOs or basic types.  Service Methods should mirror those on the client side equivalent assembly API (see below). 

The service classes must inherit from Sage.ObjectStore.MetaDataObject. This will cause any public methods to be published as web services. It will also cause any public properties to have its parameters or return types serialised unless they are marked with the attribute. 

## Codis.Sage200\.module.Server.Types

These assemblies hold DTO types that have to pass from the client to the server and have to be deployed client side as well. 

DTOs have to be serializable by the serializer used by Sage. This seem to require some particular rules that don't apply to the default WCF serializer. 

- Collection or list types must be decorated with the CollectionDataContract attribute and include a default constructor.



```xml
<CollectionDataContract()>
 Public Class NLJournalDetailDTOList
     Inherits BusinessListBase(Of NLJournalDetailDTO)
     Public Sub New(parent As NLJournalDTO)
         SetParent(parent)
     End Sub
     Public Sub New()

     End Sub
 End Class
```

#### Underlying Assemblies

The following assemblies are also deployed server side: 

**Codis.DTO.Base** \- holds DTO base types common to Sage 1000 Excelerator, moved from Codis.API.Types. 

**Codis.Sage200\.Server.Types** \- Server side Sage 200 types needed across all modules 

**Codis.Sage200\.Views**

## Client Side Assemblies

#### **Codis.Sage200Enterprise.\<Module\>**

Note: the "Sage200Enterprise" name is historical and makes little sense in the cloud architecture.

These assemblies are only 

This assembly holds: 

- An API class
- Metadata providers

The API class wraps the server side services methods and according to whether the On\-premise or cloud version of Sage is being used, either directly calls the method or calls it via the Sage dispatcher which calls the cloud version of the method.



```xml
If Sage.ObjectStore.ClientPortal.Portal.IsActive Then
       Return CType(Sage.ObjectStore.ClientPortal.Portal.CallMethod(NlJournalAPIServer, "Validate", {batchDTO}), IList(Of ErrorMessageDTO))
   Else
       NlJournalAPIServer.Validate(batchDTO)
   End If
```

Note: This is a simplified version of the portal call to illustrate the switch.  The full code could be:



```vbnet
Public Overrides Function Validate(batchDTO As MainBusinessDTO) As IList(Of ErrorMessageDTO)
    ..
    Dim result As IList(Of ErrorMessageDTO)
    If SageDetailsProvider.IsSageOnline Then
#If CompilerSageVersion >= 2013 Then
        result = RunAsync(batchDTO, "ValidateAsync", Nothing)
#End If
    Else
        result = BusinessServerAPI.Validate(batchDTO)
    End If
    MapMessagesInList(result)
    Return result
End Function
```

RunAsync invokes the CallMethodAsync method on the portal and awaits and then handles the response. RunAsync is entirely conditional on the CompilerSageVersion precompiler condition, as it makes calls to the Sage API that are not available in Sage 2011\.

The API class should also: 

- Check licences
- Map returned messages ids and parameters into full messages.
