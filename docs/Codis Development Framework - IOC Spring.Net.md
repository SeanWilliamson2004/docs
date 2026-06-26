---
title: Codis Development Framework - IOC Spring.Net
tags: []
description: Spring.net Spring.net was adopted early in V3 development primarily because
  it offered the prospect of simplifying our S1000 DAO code. The S1000…
created: '2017-01-16'
modified: '2020-04-03'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Codis%20Development%20Framework%20-%20IOC%20Spring-Net.aspx
---

# Spring.net

Spring.net was adopted early in V3 development primarily because it offered the prospect of simplifying our S1000 DAO code.  The S1000 database schema reflexs the product's long history, and tables often designed in a strange way that needs to be wrapped to form a more sensible logical layer to be used by the business rule layer.

It then became natural to adopt other areas of spring, including its IOC functionality.  Support for Spring has faded and other IOC providers have emerged as better offerings.  In particular, Spring's XML configuration is error prone.  However, it remains in place in our S1000 code but has had to be removed from our S200 code: [https://codislimited.sharepoint.com/sites/Wiki/Pages/Sage%20200%20Cloud%20Excelerator%20Architecture%20and%20Coding%20Guidelines.aspx.](https://codislimited.sharepoint.com/sites/Wiki/Pages/Sage%20200%20Cloud%20Excelerator%20Architecture%20and%20Coding%20Guidelines.aspx.)

We use the Spring.net framework in our API framework. The main parts we will be using are:

- IOC/Dependency injection
- Data access middleware for ADO
- The Cache Aspect library
- The Validation framework
- Spring Services for WCF

Spring provide substantial documentation describing these technologies, and the motivations for using them, so this will not be discussed any detail in this document.

## IOC/Dependency Injection

### Overview

This should not be confused with external (assembly) dependency management.  IOC is concerned with internal dependencies between objects.

To use Spring IOC all objects that a class depends on should be public properties of that class. If these objects are defined in the IOC configuration, then when an object is created by the IOC container, all the objects, and dependencies those objects have, will be initialized with instances of the dependent objects.

The benefits of using this technology are:

- The data access middleware works best when DAOs are instantiated using IOC.
- It provides us with a standard definition of how we should structure our code as far as coding dependencies between objects.
- If the client of an object uses an interface rather than the concrete class, and the object itself is instantiated by Spring, then it is possible to change the object used by the class by changing the configuration.
- Once the configuration is set up, and the properties are defined, the business layer and DAL code is simplified.

### Container Configuration

The container is configured to determine which objects are created to resolve dependencies. This configuration is in XML and can be contained in multiple locations of different types, including XML files and embedded resources. How and where the container is configured is the biggest area of concern for me, and there may be something of a learning process as to the best practices. There are a few key points to consider:

· The level at which the container should be used. All code in the framework and APIs should have dependencies as external properties, but this does not mean that they have to be aware of the container. In fact, they shouldn’t be unless they have to be, and the container should only be used to create objects at the highest level

· The container configuration determines which business rules are applied. The possibility that these can be amended is a beneficial feature if the configuration is held securely, server side, but a potential security hole if available client side. As such, client side products such as standard Excelerator must use embedded resources as the base configuration, whilst server side services can use XML files as their base configuration. The base configuration is the bootstrap that loads other configuration resources. Standard configuration files should be embedded and always used by the client based products, and used by default by the server side products.

Currently, I am proposing:

1\. WCF Services – Base configuration in the web.config or app.config (for standalone services). Use Spring.Services to create objects. I have yet to try this approach.

2\. The container will be configured in xml files that will be included using app.config and web.config files. There should be:

- A standard sageconfig.xml in the vb.net directory. For debug and testing purposes, this file can be used in that location. This file will define the connection objects.
- A standard module object configuration file embedded into each module.

Object Definition Pitfalls If your constructor includes any data access, the object must be marked ‘lazy\-init\=”true”’ in the container definition. Otherwise, the object will be created before the connection is opened.

## Example

  


ExceleratorBase has a number of properties.  Here is one:       Public Property ExcelMetaData As ExcelMetaData That is not set to anything in the code anywhere.  It is set by the spring container and we use the container to provide our objects.  It sets it based on configuration we give it. For that property, there is a line in a configuration file ObjectConfiguration.xml in Codis.Excelerator project.The line is:       
```
<object name="ExcelMetaData" type="Codis.Excelerator.MetaData.ExcelMetaData, Codis.Excelerator" />

```

  


 So if we load that configuration file when creating the container, classes that inherit ExceleratorBase will have their ExcelMetaData property set to a singleton instance of Codis.Excelerator.MetaData.ExcelMetaDataThis particular object will not change and you will use that configuration. However, that class Codis.Excelerator.MetaData.ExcelMetaData has properties:  
  
These also need to be set.These are both set on a per\-module basis.  If you look at ObjectConfiguration in Codis.Excelerator.NLJournals2 it has the line:

####
