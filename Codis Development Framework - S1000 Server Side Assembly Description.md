---
title: Codis Development Framework - S1000 Server Side Assembly Description
tags:
- Development
- Framework
description: 'Overview The Excelerator framework extends the base framework. Like
  the base framework, it''s assemblies can be divided into: • Those that would be…'
created: '2017-01-24'
modified: '2017-01-24'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Codis%20Development%20Framework%20-%20S1000%20Server%20Side%20Assembly%20Description.aspx
---

## Overview

The Excelerator framework extends the base framework. Like the base framework, it's assemblies can be divided into: 

•       Those that would be server side in an EE architecture 

•       Those that would be client side in an EE architecture 

•       Those that would be both client and server side 

Although this distinction is not important for standard Excelerator, the framework is built to accommodate the EE architecture. Assemblies that are pure client or both client and server are built using the .net Framework 4 Client. Assemblies that are pure server side are built using the .net Framework 4 Server. 

**Codis.API.Framework** Core functionality to be used by server side API modules in both standard and Enterprise solutions. 

**Codis.API.Types** Types used by Codis.API.Framework that might be required client side. 

**Codis.SageEnterprise.Common** Sage 1000 specific functionality that is common to all Sage 1000 Server side assemblies 

**Codis.SageEnterprise.Finance.Common.Type** Functionality that is common to Sage 1000 Finance Module server side assemblies 

**Codis.SageEnterprise.Finance.Common** Type definitions that is common to Sage 1000 Finance Module assemblies \- server and client side 

**Codis.SageEnterprise.****Module** Module API to be used by server side API modules in both standard and Enterprise solutions. 

**Codis.SageEnterprise.Finance.Types** Types used by the Codis.SageEnterprise.(Finance Module) assemblies that might be required client side. 

## Enterprise Assemblies

**Codis.Common.Data** CodisMaster database Data Access Objects 

**Codis.Common** A wrapper around some DAOs and some DAOs. 

**Codis.Framework** Core Enterprise functionality 

**Codis.Framework.COM** Core Enterprise functionality required for supporting legacy COM components, including licencing.
